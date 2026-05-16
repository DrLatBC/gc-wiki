# Production & Economy Formulas

Canonical reference for colony output, population, and economic calculations. These formulas were pulled directly from the game source by an admin.

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
minerals = 1 + sqrt(
    mining × (numplanets × 0.3)
    × (1 + 0.4 × mining_research)
    × (planet_mining_mod / 100)
    × race_mineral_mod
) × turns
```

**Effect of research:** +40% per mining research level (scalar inside the sqrt).
**Colony breadth matters:** More planets in the colony increases mineral output.
**Diminishing returns:** Square root means high mining values produce sharply diminishing returns vs. linear ore output.

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
```

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

**If `raw_materials ≥ industry × turns` (full production):**

```
consumer_goods = floor(
    ((industry × turns) + (industry × turns × industry_research × 0.1))
    × race_industry_mod
)
raw_materials_consumed = industry × turns
```

**If `raw_materials < industry × turns` (resource-limited):**

```
consumer_goods = floor(
    (raw_materials + (raw_materials × industry_research × 0.1))
    × race_industry_mod
)
raw_materials_consumed = raw_materials  (all remaining)
```

**Effect of research:** +10% consumer goods per industry research level.
**Cost:** 1 raw material per industry building per turn at full production.

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
**Effect of loyalty:** Loyalty acts as a multiplier on population for an additional credit yield. At 5000 loyalty, the loyalty term equals the base population term — effectively doubling tax income. Above 5000, loyalty produces more than the base.
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

After population consumes goods, surplus goods on the colony are auto-sold at **5.5 credits per good**:

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

Concretely: if you have 2,000 total land (200 housing + 1,800 income buildings) at housing research 0, your max pop is `200 × 10 = 2,000`, which exactly matches the 2,000-building total. Fully staffed. If housing isn't sufficient for the total:

```
staffing_ratio = min(1.0, max_population / total_buildings)
```

and every non-housing building's output is multiplied by `staffing_ratio`. Tax credits, goods consumption, food demand, and food bonuses all still scale with `max_population` (the pop you have, whether they're "working" or not).

**Solving for the minimum housing needed** to fully staff a colony of `total_buildings` infrastructure at research level `Hr`:

```
housing_min = ceil(total_buildings / (10 + Hr))
```

This is the source of the "7 housing meta" you'll see referenced — at full housing research investment (Hr ≈ 250+), each housing supports ~260 pop, so even a 2,000-land colony only needs ~8 housing for staffing. The other ~1,992 land slots go to your income building of choice.

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

**Maximum population for Collective:** `max_population × 2` (double the normal cap).

Capped at `max_population × 2`.

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
ship_upkeep_cost = ship_upkeep × turns
```

Where `ship_upkeep` is the per-turn maintenance cost of your fleet.

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
credits = (
    (population × 2,500)
    + ((5,500 × total_infra²) / planet_land)
    + (200,000 × planets_in_colony)
) / 15
× race_plunder_mod
```

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
| Marauder D-class | (not playable) | — |
| Guardian | −99% | 0.01× |
| Viral | −99% | 0.01× |

**Strategic notes:**

- **Marauder + Collective are the only races that meaningfully plunder.** A Marauder hitting a fully-built C3 (high pop + high infra + 125 planets) at +1,900% can pull a credits payout in the billions.
- **Infrastructure scales quadratically** via `total_infra²`. A fully-built colony plunders for vastly more than a sparsely-built one of the same land — the squared term dominates the payout for big builds.
- **Dividing by land** means dense colonies (lots of infra packed onto small land) plunder for more per-infra than spread-out colonies — but small-land planets cap how much infra fits, so in practice land + infra grow together.
- Plunder also removes the colony from your list and converts the planet to a [Dead](planets.md#standard-planets) state.

---

# Resource Caps

Hard ceilings on stored resources. Production beyond these caps is discarded.

| Resource | Cap |
|---|---|
| Credits (positive) | 5,000,000,000,000 (5 trillion) |
| Credits (debt floor) | -200,999,999,999 |
| Raw Materials | 25,000,000,000 (25 billion) |
| Food | 25,000,000,000 (25 billion) |
| Goods | 25,000,000,000 (25 billion) |
| Ore | 2,000,000,000 (2 billion) |
| Each mineral type (1–6) | 2,000,000,000 (2 billion) |

---

# Production Summary

| Building | Primary Output | Secondary Output | Research Bonus | Notes |
|---|---|---|---|---|
| Mining | Ore (linear) | Minerals (sqrt) | +10% ore, +40% minerals | Minerals scale with planet count, ore capped by deposit |
| Agriculture | Food | Raw Materials | +10% each | Both outputs equal |
| Commercial | Consumer Goods | Food bonus + Empire credits | +8% CG, +10% empire credits | Consumes 2 RM per building per turn |
| Industry | Consumer Goods | — | +10% CG | Consumes 1 RM per building per turn |
| Housing | Population cap | — | +1 cap per housing | Cap = (10 + research) × housing; Collective doubles cap |
| Population | Tax Credits | — | — | Loyalty 5000 doubles base income |

---

# Calculation Order

For each turn cycle, the game processes calculations in this order:

**Per colony:**

1. Tax credit income
2. Minerals from mining
3. Industry CG (consumes raw materials)
4. Population goods consumption + auto-conversion to credits
5. Commercial CG (consumes raw materials, conditional)
6. Agriculture food + raw materials
7. Food bonus (conditional)
8. Ore mining
9. Population growth or starvation

**Empire-wide:**

1. Ship upkeep deducted
2. Empire commercial income added
3. Infrastructure maintenance deducted
4. Debt interest applied (if credits < 0)
5. Resource caps enforced
