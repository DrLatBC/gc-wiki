# Colonies & Clustering

## What is a Colony?

A colony is a group of planets under a single entry in your empire list. Each race is allowed a maximum number of colonies, with some races designed to hold more land than others.

## Planets

Planets have a land value that determines how useful they are for infrastructure and clustering. Land is the only stat that matters for clustering — planet type is irrelevant.

### Land Ranges

- **Floor:** 1 land
- **Ceiling:** ~1,500 land (requires an extremely rare "S-class" roll on top of an already high roll — never plan around this)
- **Target for clustering:** 1,000+ land
- **Acceptable:** 800+ land
- **Discard:** anything below 800

### Planet Types

Most planet types are irrelevant to income and clustering. The exceptions:

| Type | Notes |
|------|-------|
| **Barren** | Highest possible land mass. Most likely to push 1,000+ land. Primary clustering target. |
| **Balanced** | Can reach 850–900 with a good roll. Acceptable clustering candidate. |
| **U.Spazial** | Best planet for artifact digging. Seek out 2-land copies specifically. |
| **U.Large** | 5,000–10,000+ land. Excellent for infrastructure but cannot be clustered. |
| **U.Fertile** | Very high food/agriculture output. Cannot be clustered. |
| **U.Eden** | Bonus to population growth. Useful for Tax players. Cannot be clustered. |
| **U.Rich** | High ore content but very low land. Generally not worth keeping. |

U-class planets cannot be clustered but are kept for their unique bonuses. Viral and Collective cannot use U-class planets for income (infection/assimilation is required) but can use U.Spazial for digging since digging does not require infection.

> Full numeric reference for all 30+ planet types — including population growth, agriculture, and mining modifiers, plus cluster-type modifiers — lives on the [Planet Types](planets.md) page.

## Exploring

Players start by exploring to build up their planet count. Exploration requires Scouts — expensive ships that improve scanning power.

- Players can explore approximately **55–60 planets** before exploration becomes impractical
- Bad planets should be destroyed (via plunder) and replaced with better rolls
- Only planets you keep count toward your total
- After ~60 planets, further growth requires combat

## Clustering

Clusters are groups of colonies merged into a single, larger colony entry. Clustering requires researching the cluster project first.

### Standard Clustering (all races except Viral and Collective)

| Cluster Level | Planets | Notes |
|--------------|---------|-------|
| C1 | 5 | Base cluster |
| C2 | 25 (5 × C1) | |
| C3 | 125 (5 × C2) | Endgame target |

Land is purely additive. A C3 made of 125 planets averaging 800 land each = 100,000 land exactly.

- **Solid C3:** ~100,000 land
- **Large C3:** ~130,000 land (requires being very selective with planet rolls)

### Viral & Collective Clustering

Viral and Collective use infection/assimilation instead of standard clustering and use **4 planets per cluster** instead of 5.

| Cluster Level | Viral (Tainted) | Collective (Similare) |
|--------------|-----------------|----------------------|
| C1 | 1 planet | 1 planet |
| C2 | 4 planets | 4 planets |
| C3 | 16 planets | 16 planets |
| C4 | 64 planets | 64 planets |
| C5 | N/A | 256 planets |

Collective is the only race with access to C5, allowing for massive land totals. Viral's cluster cap is significantly smaller.

Viral and Collective can also infect/assimilate clusters taken from other races. These retain their original planet count (5, 25, or 125) and can be further clustered with matching infected/assimilated clusters.

> **Note:** Unassign Agriculture and Industry infrastructure before infecting a cluster — these cannot be unassigned after infection.

## Colony List & Defense

Your colony list order determines what you lose when attacked. Attackers always take the **outermost (topmost) colonies** first.

- New colonies (explored or won in battle) always appear at the **top** of the list
- Clustering consumes the 5 deepest eligible colonies and places the result where the deepest one was

The standard defensive setup uses **junk colonies as ablative armor** to protect clustered assets:

```
Junk
Junk
Junk
Junk
Junk
Junk
Junk
Junk
Junk
U.Spazial
C3
```

List order cannot be manually rearranged — it must be managed indirectly through acquiring, destroying, and clustering colonies strategically.

### How Many Colonies Can You Lose Per Attack?

| PR Killed | Colonies Lost |
|-----------|--------------|
| ≥10% of defender's ship PR | 1 |
| ≥20% of defender's ship PR | 2 |
| ≥40% of defender's ship PR | 3 |

A maximum of **4 colonies** can be lost in a single Damage Protection period (typically as a 1+3 or 2+2 split across multiple attacks). Losing 3 in one period is the practical norm; 4 is possible but rare.

## Population

Population is the workforce of a colony — it produces tax credits, consumes food and goods, and is capped by Housing buildings and Housing research.

**Maximum population:**
`Max Pop = (10 + Housing Research) × Housing`

Each level of Housing Research adds 1 to the population multiplier per Housing building. Collective doubles this cap (`Max Pop × 2`).

**Growth** requires `food ≥ floor(population / 10) × turns` (Guardian colonies are exempt — they don't consume food and cannot starve). When fed and below cap:

```
new_population = population + floor(
    (floor(population × (2 × planet_pop_mod / 100) / 100) + 1) × turns
)
```

**Starvation** triggers when food runs short for non-Guardian colonies:

- 15% population loss (`floor(population × 0.85)`)
- 10 loyalty loss (down to a minimum of 0)

See the [Formulas](formulas.md) page for the canonical versions of all population calculations.

## Plundering

Plundering is the only way to destroy a colony. It converts the colony's value into a one-time credit payout and removes it from your empire. Players use plunder to:

- Discard low-value planets during the exploration phase
- Deny captured colonies to other players (scorched earth)
- Manage colony list order indirectly
