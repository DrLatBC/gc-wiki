# Production & Economy Formulas

Canonical reference for colony output, population, and economic calculations. These are the verified, authoritative production and economy formulas.

> **Note on `turns`:** Most production runs as a batched cycle. `turns` represents the number of turns processed in a single cycle. `floor()` truncates to a whole number; `ceil()` rounds up. All output values are integers.

## Variable Glossary

| Variable | Meaning |
|---|---|
| `mining` | Mining buildings on the colony |
| `agriculture` | Agriculture buildings on the colony |
| `commercial` | Commercial buildings on the colony |
| `industry` | Industry buildings on the colony |
| `housing` | Housing buildings on the colony |
| `population` | Population on the colony |
| `loyalty` | Loyalty of the colony |
| `numplanets` | Planets in the colony |
| `turns` | Turns used in this production cycle |
| `housing_research` | Housing research level |
| `commercial_research` | Commercial research level |
| `industry_research` | Industry research level |
| `agriculture_research` | Agriculture research level |
| `mining_research` | Mining research level |
| `planet_mining_mod` | Planet-type mining modifier (%) |
| `planet_agriculture_mod` | Planet-type agriculture modifier (%) |
| `planet_pop_mod` | Planet-type population growth modifier (%) |
| `race_agriculture_mod` | Race agriculture modifier |
| `race_commercial_mod` | Race commercial modifier |
| `race_industry_mod` | Race industry modifier |
| `race_mineral_mod` | Race mineral modifier |
| `race_tax_mod` | Race tax modifier |
| `race_good_mod` | Race goods consumption modifier |
| `race_maintenance_mod` | Race maintenance cost modifier |
| `raw_materials` | Player's raw materials in storage |

---

# Colony-Level Production

## Ore Mining

```
ore = floor(
    (mining × turns) × (1 + mining_research × 0.1) × (planet_mining_mod / 100)
)
```

Capped by ore deposit on the colony — production stops when the deposit runs out.

**Effect of research:** +10% ore per mining research level.

---

## Minerals from Mining

```
minerals = ceiling(sqrt(
    mining × (numplanets × 0.3)
    × (1 + 0.4 × mining_research)
    × (planet_mining_mod / 100)
    × race_mineral_mod
)) × turns
```

The per-turn gain is the square root **rounded up to a whole unit each turn** (`ceiling`), then accumulated across turns.

**Effect of research:** +40% per mining research level (scalar inside the sqrt).
**Colony breadth matters:** More planets in the colony increases mineral output.
**Diminishing returns:** Square root means high mining values produce sharply diminishing returns vs. linear ore output.
**Ceiling:** This is always rounded up.

---

## Food from Agriculture

```
food = floor(
    agriculture × (1 + agriculture_research × 0.1)
    × (planet_agriculture_mod / 100)
    × race_agriculture_mod
) × turns
```

**Effect of research:** +10% food per agriculture research level.

---

## Raw Materials from Agriculture

```
raw_materials = floor(
    agriculture × (1 + agriculture_research × 0.1)
    × (planet_agriculture_mod / 100)
    × race_agriculture_mod
) × turns
```

**Note:** Agriculture buildings produce both food and raw materials at the same rate. Same inputs, same output value.

---

## Food Bonus (Commercial × Agriculture synergy)

Fires **after** Food from Agriculture, only when:

```
commercial_research ≥ 5  AND  commercial ≥ 5  AND  agriculture ≥ 1
    AND  race ≠ Marauder  AND  race ≠ Collective
```

> Marauder and Collective are **excluded** from this synergy bonus even if they otherwise meet the conditions.

```
bonus_food = floor(
    base_food × (1 + ((commercial_research / 100) + (commercial / 10000)) / 5 + 0.001)
    - base_food
)
```

Where `base_food` is the food produced by the Food from Agriculture formula above.

**Effect:** Commercial buildings provide a percentage uplift on agricultural food output. Scales with commercial research and commercial building count.

---

## Consumer Goods from Industry

Industry consumes raw materials to produce consumer goods. If raw materials run out mid-production, output is based on what was available.

**Production (full):**

```
goods_base = (industry × turns) + (industry × turns × industry_research × 0.1)
           = industry × turns × (1 + industry_research × 0.1)

consumer_goods         = round(goods_base × (planet_industry_mod / 100) × race_industry_mod)
raw_materials_consumed =       goods_base × (planet_industry_mod / 100) × race_industry_mod × 0.3
```

`planet_industry_mod` is the colony's planet/cluster **Industry modifier — added in Patch 106** (see [Planet Types → Industry Modifiers](planets.md#industry-modifiers)). Colony types with no listed modifier use `100` (×1.0). Note Industry rounds to nearest (`round()`), **not** `floor()` like most other outputs.

**Effect of research:** +10% consumer goods per industry research level.

**Cost (changed in Patch 106):** Industry consumes raw materials equal to **exactly 30% of the consumer goods it produces** — the same `goods_base × planet_mod × race_mod` value (before rounding) multiplied by `0.3` — replacing the old flat "1 raw material per industry building per turn." Example: 5,000,000 goods → 1,500,000 raw materials. The patch notes this works out to roughly 6% of net income with goods priced at 5, and ~10% with goods at 3. If raw materials run short mid-cycle, output is capped to what the available RM can support.

---

## Consumer Goods from Commercial

Fires **after** Industry CG production. Conditional on:

```
commercial_research ≥ 5  AND  commercial ≥ 5  AND  raw_materials ≥ 2
```

**If `raw_materials ≥ commercial × 2 × turns` (full production):**

```
consumer_goods = floor(
    commercial × ((commercial_research × 0.08) + 1)
    × race_commercial_mod
) × turns
raw_materials_consumed = commercial × 2 × turns
```

**If `raw_materials < commercial × 2 × turns` (resource-limited):**

```
consumer_goods = floor(raw_materials / 2)
raw_materials_consumed = raw_materials  (all remaining)
```

**Effect of research:** +8% consumer goods per commercial research level.
**Cost:** 2 raw materials per commercial building per turn at full production.

---

## Tax Credit Income

```
credits = ((population / 2) + (population × loyalty / 5000)) × race_tax_mod × turns
```

**Effect of population:** Each population unit contributes a flat 0.5 credits per turn baseline.
**Effect of loyalty:** Loyalty adds `population × (loyalty / 5000)` on top of the `population / 2` base term. The loyalty term equals the base term at **2,500** loyalty (where tax income exactly doubles). At **5,000** loyalty the loyalty term equals `population` — twice the base — so total tax reaches `1.5 × population`, **triple** the zero-loyalty income. As of **Patch 106**, 5,000 is the *base* personal cap, **not** an absolute ceiling: completing loyalty-reward missions raises your cap above 5,000, and the `loyalty / 5000` term keeps scaling linearly past 1.5 × population. Guardians have a base cap of **2,500** (raised by their loyalty missions — all of Act 1 = +500 → 3,000). See [Loyalty (raising)](#loyalty-raising) for how loyalty now accrues.
**Effect of race:** Race tax modifier scales the entire result.

---

## Population Goods Consumption (per colony)

Each colony consumes goods proportional to its population:

```
goods_consumed = floor(population / 10 × race_good_mod) × turns
```

This is subtracted from the colony's contribution to your goods total.

---

## Goods → Credits Auto-Conversion (per colony)

The goods your population **consumes** convert to credits at **5.5 each**. Surplus goods beyond population demand are **retained in your stockpile**, not sold:

**If `available_goods ≥ goods_consumed`:**

```
credits += ceil(goods_consumed × 5.5)
goods -= goods_consumed
```

**If `available_goods < goods_consumed`:**

```
credits += ceil(available_goods × 5.5)
goods = 0
```

This is the primary mechanism by which produced goods become income. Calculated per colony — empire-wide totals are the sum across all colonies.

---

# Population Mechanics

## Maximum Population

```
max_population = (10 + housing_research) × housing
```

**Effect of research:** Each housing research level adds 1 to the population multiplier per housing building.

---

## Staffing — Pop Required to Fill Land

**Every building on a colony consumes 1 population to operate** — housing buildings included. Housing buildings *provide* `(10 + housing_research)` population each, so they're net-positive (one pop occupies the housing itself, the rest is free for staffing other buildings). Non-housing buildings consume 1 pop with no provision.

Concretely: if you have 2,000 total land (200 housing + 1,800 income buildings) at housing research 0, your max pop is `200 × 10 = 2,000`, which exactly matches the 2,000-building total. Fully staffed.

This is enforced at **build time**, not as a runtime output penalty. The game tracks available labor per colony:

```
available_labor = population − housing − commercial − industry − agriculture − mining
```

A build is **rejected** if the new buildings would require more labor than you have (`build_amount > available_labor` → "not enough labor"). In other words, you can **never** be understaffed — you simply cannot construct a building unless you have a free population unit to operate it. There is no fractional output scaling; an understaffed colony state doesn't exist. The practical consequence is exactly the one above: to fill `total_buildings` worth of land you must first have the population to operate it, and population comes only from housing.

**Solving for the minimum housing needed** to fully staff a colony of `total_buildings` infrastructure at research level `Hr`:

```
housing_min = ceil(total_buildings / (10 + Hr))
```

This is the source of the **"7 housing meta"** you'll see referenced — the 7 is a **housing research level**, not a building count. At `Hr = 7` each housing supports 17 pop, so housing only ever occupies `1 / (10 + Hr)` of your land — about **6%**. A 255-land colony needs 15 housing; a 2,000-land colony needs 118. Everything else goes to your income building of choice.

The reason to keep it *low* is the 255-level research cap: every level spent on housing is a level not spent on the income line that actually multiplies your output. Pushing housing research higher has sharply diminishing returns — going from `Hr = 7` to `Hr = 20` only frees up another ~3% of your land, which is a poor trade for 13 levels.

For Collective, `pop_per_housing` is doubled (Collective's racial 2× cap), so `housing_min = ceil(total / ((10 + Hr) × 2))`.

---

## Population Growth (Normal Races)

Requires sufficient food to feed the colony. Each colony consumes:

```
food_required = floor(population / 10) × turns
```

If `food ≥ food_required` AND `population < max_population`:

```
new_population = population + floor(
    (floor(population × (2 × planet_pop_mod / 100) / 100) + 1) × turns
)
```

Capped at `max_population`.

---

## Population Growth (Guardian Race)

**Guardian colonies do not consume food and cannot starve.**

Growth uses the same formula as normal races, but without the food check:

```
new_population = population + floor(
    (floor(population × (2 × planet_pop_mod / 100) / 100) + 1) × turns
)
```

Capped at `max_population`, the same ceiling as every other race.

---

## Starvation (Normal Races Only)

Triggered when `food < food_required`. Guardian race is immune.

```
new_population = floor(population × 0.85)
new_loyalty = max(loyalty - 10, 0)
```

**Effect:** 15% population loss and 10 loyalty loss per starvation event. Loyalty cannot go below 0.

---

# Empire-Wide Calculations

These run once per turn cycle, summed across all your colonies.

## Empire Commercial Income

```
total_commercial = sum of commercial buildings across all your colonies

commercial_income = (total_commercial + (total_commercial × commercial_research × 0.1))
                    × 5
                    × race_commercial_mod
                    × turns
```

A flat empire-level credit income from your total commercial buildings. Separate from per-colony Consumer Goods production.

**Effect of research:** +10% per commercial research level.

---

## Power Rating (PR)

Your empire's Power Rating — the number the combat damage-% thresholds, rankings, and NPC scaling are all measured against. Recalculated from your colonies and fleet:

```
PR = total_infrastructure × (5 + (total_land / 250000))
   + (total_planets × 1000)
   + total_fleet_power
```

| Term | Meaning |
|---|---|
| `total_infrastructure` | Every building you own — `housing + commercial + mining + agriculture + industry` summed across all colonies. Since each building occupies one land, this is effectively **the land you have actually built on** |
| `total_land` | **All the land you own**, across every colony — built on or not |
| `total_planets` | Planets summed across all colonies |
| `total_fleet_power` | Power summed across every ship in your fleet |

The two land-ish terms are easy to mix up: the multiplicand is your **built** land, while the figure inside the multiplier is your **total** land. A practical consequence is that **empty land still raises PR** — unbuilt land contributes nothing on its own, but it lifts the multiplier applied to everything you have built.

**Small-empire variant:** if the value above comes out below **5,000**, a legacy formula is used instead:
`total_infrastructure + (total_planets × 1000) + (population / 5) + total_fleet_power`.

Note that **fleet power dominates** PR for combat-focused empires (it's added 1:1), while land contributes through the `total_land / 250000` term — every 250,000 land you own adds +1 to the multiplier on each point of infrastructure.

---

## Maintenance & Upkeep

Total empire upkeep is deducted from credits each turn cycle.

### Infrastructure Maintenance

```
total_infrastructure = sum of (housing + commercial + industry + agriculture + mining)
                       across all your colonies

maintenance_cost = total_infrastructure × race_maintenance_mod × turns
```

### Ship Upkeep

```
ship_upkeep_cost = fleet_upkeep × turns
```

Where `fleet_upkeep` is the summed per-turn upkeep of every ship you own. Per-ship upkeep is **computed from the ship's stats**, not a fixed stored value. The core derivation:

```
base   = (ship_power × ship_build_turns) / 10
weapon = total_weapons × (1 + (weapon_types − 1) / 10) × range^1.5
armor  = (hull × 5) × (2 + total_shields)
upkeep = base × (weapon + armor) × race_upkeep_mod
```

Then adjusted by combat traits: ÷1.5 if the ship has no return-fire and no long-range, ×1.5 for long-range (and starbases get an extra ×1.2). The race upkeep modifier scales the whole thing (Guardian cheapest at `0.8/1,000,000`, A.Miner priciest at `10.1/1,000,000`; Terran `8`, Viral `7`, Collective `3.3`, Marauder `1.9`).

See [Ships](ships.md) for the per-ship breakdown and how this drives "disband idle scouts" advice. *(A handful of ships have no upkeep at all.)*

### Total Deduction

```
credits -= maintenance_cost + ship_upkeep_cost
```

---

## Debt Interest

Triggers only when `credits < 0` after all income and expenses are processed.

```
debt_interest = (|credits| × 0.015) × (1.015 ^ (turns - 1)) × turns
credits -= debt_interest
```

**Effect:** 1.5% per-turn compounding interest on negative credit balances. The `1.015 ^ (turns - 1)` term means longer turn batches compound the debt interest, so going deep into debt during high-turn cycles is significantly more punishing than spreading the same turns across multiple short cycles.

---

## Plunder Payout

One-time credit payout when destroying a colony. See [Colonies → Plundering](colonies.md#plundering) for the strategic role.

```
credits = fix(
    (
        (population × 2,500)
        + ((5,500 × total_infra²) / planet_land)
        + (750,000 × planets_in_colony)
    ) / 15
    × race_plunder_mod
)
```

The entire expression is float math, truncated toward zero (`fix`) **exactly once** — at the very end, after the race multiplier. None of the intermediate terms (including the `total_infra²` term) are rounded on their own.

| Variable | Meaning |
|---|---|
| `population` | Population on the colony at the moment of plunder |
| `total_infra` | Sum of all buildings on the colony (housing + commercial + industry + agri + mining) — **squared** in the formula |
| `planet_land` | Land value of the colony |
| `planets_in_colony` | Planets in the colony (1 / 5 / 25 / 125 for C0–C3 standard clusters) |
| `race_plunder_mod` | Race plunder modifier (see [Races → Modifiers](races.md#race-modifiers)) |

**Race plunder modifier values:**

| Race | Mod | Multiplier |
|---|---|---|
| Marauder | **+1,900%** | 20× |
| Collective | **+1,100%** | 12× |
| Terran | −50% | 0.5× |
| A.Miner | −95% | 0.05× |
| Guardian | −99% | 0.01× |
| Viral | −99% | 0.01× |

**Strategic notes:**

- **Marauder + Collective are the only races that meaningfully plunder.** A Marauder hitting a fully-built C3 (high pop + high infra + 125 planets) at +1,900% can pull a credits payout in the billions.
- **Infrastructure scales quadratically** via `total_infra²`. A fully-built colony plunders for vastly more than a sparsely-built one of the same land — the squared term dominates the payout for big builds.
- **Dividing by land** means dense colonies (lots of infra packed onto small land) plunder for more per-infra than spread-out colonies — but small-land planets cap how much infra fits, so in practice land + infra grow together.
- Plunder also removes the colony from your list and converts the planet to a [Dead](planets.md#standard-planets) state.

---

# Action Costs

## Infrastructure Research Cost (turns per level)

Infrastructure research is bought with turns, 1 turn = 1 unit of progress toward the current level's requirement. Each completed level makes the **next** level cost more:

```
next_level_cost = max( floor(current_level_cost × 1.20), current_level_cost + 1 )
```

So each level costs **~20% more turns than the previous** (with a +1 floor so it always rises). A brand-new research line starts at **2 turns** for level 1. The cost is then clamped by level band:

| Level band | Cap (turns per level) |
|---|---|
| ≤ 100 | 750 |
| 101+ | 2,500 |

Starting at 2 and compounding 20%, a line hits the 750 cap at **level 34** — level 33 is the last one below it, at 644 turns. Every level from 34 to 100 then costs a flat 750, and from 101 onward a flat 2,500. This is the grind referenced on the [Turns](turns.md) page.

> **Your total infrastructure research is capped at 255 levels**, summed across all five types. You choose how to spread those levels between Housing, Commercial, Industry, Agriculture, and Mining — which is why the income meta parks Housing at a low level and pours the rest into one income line.

---

## Loyalty (raising)

**Reworked in Patch 106.** The old manual "reward loyalty" action — which cost both turns *and* credits (`population × 2 × turns_spent^1.5`) — has been **removed entirely**. Loyalty now rises **passively**:

- As long as you are **holding Consumer Goods**, every colony's loyalty climbs on its own toward your personal cap. No action to take, nothing to spend.
- There is **no credit cost and no turn cost** — keeping CGs in stock is the whole requirement.
- If you run out of Consumer Goods, loyalty stops climbing.

**Personal cap** = race base + loyalty-reward mission bonuses:

| Race | Base cap | With loyalty missions |
|---|---|---|
| Guardian | 2,500 | +500 for all of Act 1 → 3,000 (climbs further with later loyalty missions) |
| All other races | 5,000 | raised **above** 5,000 by completed loyalty-reward missions |

**Guardians can now raise loyalty** (up to their 2,500 base, before missions) — this reverses the pre-106 hard block. See [Tax Credit Income](#tax-credit-income) for what loyalty is worth.

---

# Resource Caps

Hard ceilings on stored resources. Production beyond these caps is discarded.

| Resource | Cap |
|---|---|
| Credits (positive) | 50,000,000,000,000 (50 trillion) |
| Credits (debt floor) | -200,999,999,999 |
| Raw Materials | 100,000,000,000 (100 billion) |
| Food | 100,000,000,000 (100 billion) |
| Goods | 100,000,000,000 (100 billion) |
| Ore | 10,000,000,000 (10 billion) |
| Each mineral type (1–6) | 10,000,000,000 (10 billion) |

> **Patch 106** (June 2026) raised these: Credits 5T → 50T; Food / Goods / Raw Materials 25B → 100B; Ore and each mineral 2B → 10B. Debt floor unchanged.

---

# Production Summary

| Building | Primary Output | Secondary Output | Research Bonus | Notes |
|---|---|---|---|---|
| Mining | Ore (linear) | Minerals (sqrt) | +10% ore, +40% minerals | Minerals scale with planet count, ore capped by deposit |
| Agriculture | Food | Raw Materials | +10% each | Both outputs equal |
| Commercial | Consumer Goods | Food bonus + Empire credits | +8% CG, +10% empire credits | Consumes 2 RM per building per turn |
| Industry | Consumer Goods | — | +10% CG | Consumes 30% of CG output as RM (Patch 106); planet Industry modifier applies; rounds with round() not floor() |
| Housing | Population cap | — | +1 cap per housing | Cap = (10 + research) × housing; Collective doubles cap |
| Population | Tax Credits | — | — | Loyalty 2500 doubles income; 5000 triples it (base cap, raised above 5000 by missions) |

---

# Calculation Order

For each turn cycle, the game processes calculations in this order:

**Per colony:**

1. Tax credit income
2. Minerals from mining
3. Industry CG (consumes raw materials)
4. Population goods demand calculated (capped at available goods)
5. Commercial CG (consumes raw materials, conditional) — produced into the goods pool
6. Goods → credits auto-conversion (consumed goods × 5.5; runs *after* Commercial CG)
7. Agriculture food + raw materials
8. Food bonus (conditional)
9. Ore mining
10. Population growth or starvation

**Empire-wide:**

1. Ship upkeep deducted
2. Empire commercial income added
3. Infrastructure maintenance deducted
4. Debt interest applied (if credits < 0)
5. Resource caps enforced
