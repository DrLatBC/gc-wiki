# Planet Types

Each planet type has fixed modifiers for population growth, agriculture, and mining, plus a land-roll range and (where applicable) an ore-deposit range. These modifiers are stored as percentages and feed the per-colony formulas — e.g. a +50% mining planet means `planet_mining_mod = 150` in the formula `mining × … × (planet_mining_mod / 100)`.

> See [Formulas](formulas.md) for how each modifier is applied. See [Colonies & Clustering](colonies.md) for how planets group into clusters.

## Notation

| Term | Meaning |
|---|---|
| **Pop. growth** | `planet_pop_mod` (population growth rate modifier, %) |
| **Agriculture** | `planet_agriculture_mod` (food + raw material output, %) |
| **Mining** | `planet_mining_mod` (ore + mineral output, %) |
| **Land** | Base land roll range — drives infrastructure capacity. Explore inflates this by 1.2625×–1.50× (see [Exploration](exploration.md#the-explore-land-mod)) |
| **Ore** | Initial ore deposit roll range — caps lifetime ore production |
| **No Support** | That income type cannot be produced on this planet |

A baseline planet has all modifiers at 0% (i.e. `100/100 = 1.0×` in the formulas).

## Standard Planets

These are the planets you'll encounter while exploring. All can be clustered.

| Planet | Pop. growth | Agriculture | Mining | Land | Ore |
|---|---|---|---|---|---|
| **Barren** | −50% | No Support | +50% | 50–935 | 150–500 |
| **Balanced** | +20% | 0% | 0% | 185–925 | 750–900 |
| **Forest** | −10% | +100% | −25% | 50–350 | 0–150 |
| **Desert** | −25% | −75% | +100% | 100–250 | 100–350 |
| **Marshy** | −20% | −50% | −50% | 50–150 | 0–150 |
| **Rocky** | −25% | No Support | −90% | 34–121 | 500–3,300 |
| **Icy** | −25% | No Support | −95% | 24–83 | 1,000–4,500 |
| **Oceanic** | −20% | No Support | −50% | 10–50 | — |
| **Gas** | 0% | No Support | No Support | 2–6 | — |

**Best for clustering:** Barren and Balanced have the highest land ceilings and are the only mainstream picks for endgame clusters. Forest can be acceptable on a strong roll.

> **Land values shown are base rolls.** The Explore action applies a `1.25 × (1 + randrange(1,20)/100)` multiplier on top, so post-explore land is 1.2625×–1.50× the listed ceiling. A Barren rolling 935 base can hit 1,402 useable land in practice. See [Exploration](exploration.md#the-explore-land-mod).

## U-Class Planets

U-class planets are rare, special-purpose, and **cannot be clustered**. They are kept for unique bonuses and stay as standalone colonies.

| Planet | Pop. growth | Agriculture | Mining | Land | Notes |
|---|---|---|---|---|---|
| **U.Eden** | +1,000% | −98% | No Support | 500–2,000 | Massive population growth — Tax player paradise |
| **U.Fertile** | −50% | +175% | No Support | 500–2,000 | Best Agriculture planet in the game |
| **U.Large** | −80% | No Support | No Support | 2,000–10,000 | Huge land for raw infrastructure capacity |
| **U.Rich** | −90% | No Support | +150% | 11–28 | 10,000–350,000 ore — by far the richest deposit |
| **U.Spazial** | −90% | No Support | No Support | 1–5 | Best digging planet for artifacts |

Viral and Collective **cannot use U-class planets for income** (infection/assimilation is required, which doesn't apply). They can still use U.Spazial for digging since digging does not require infection.

## Cluster Planet Types

When colonies cluster, the resulting cluster gets its own planet-type modifier on top of the contributing planets. These bonuses stack with the underlying planet rolls.

### Standard Clusters (Terran, Aspha Miner, Guardian, Marauder)

| Cluster | Pop. growth | Agriculture | Mining |
|---|---|---|---|
| Cluster Lvl 1 | +10% | +15% | +10% |
| Cluster Lvl 2 | +20% | +30% | +20% |
| Cluster Lvl 3 | +30% | +45% | +30% |

Cluster bonuses are **additive** to the underlying land — a C3 of 100,000 land gets a +30% pop / +45% agri / +30% mining boost on top of whatever its component planets contribute.

### Collective Clusters (Similare)

Collective uses assimilation. Similare clusters scale up to C5 (the only race with this).

| Cluster | Pop. growth | Agriculture | Mining |
|---|---|---|---|
| Similare C.1 | +20% | −70% | −50% |
| Similare C.2 | +20% | −65% | −55% |
| Similare C.3 | +20% | −60% | −60% |
| Similare C.4 | +20% | −55% | −65% |
| Similare C.5 | +20% | −52% | −70% |

### Viral Clusters (Tainted)

Viral uses infection. Tainted clusters cap at C4.

| Cluster | Pop. growth | Agriculture | Mining |
|---|---|---|---|
| Tainted C.1 | −20% | −20% | −50% |
| Tainted C.2 | −30% | −25% | −55% |
| Tainted C.3 | −40% | −30% | −60% |
| Tainted C.4 | −50% | −35% | −65% |

### Captured Cluster Variants

When Viral or Collective takes an existing cluster from another race, it converts to an Infected (Viral) or Assimilated (Collective) variant with its own modifier set. These retain the original cluster's planet count.

| Cluster | Pop. growth | Agriculture | Mining |
|---|---|---|---|
| Assimilated C1 | 0% | −20% | 0% |
| Assimilated C2 | −5% | −10% | −5% |
| Assimilated C3 | −10% | 0% | −10% |
| Infected C1 | −30% | −10% | −30% |
| Infected C2 | −35% | 0% | −35% |
| Infected C3 | −40% | +10% | −40% |

## Special Planets

| Planet | Pop. growth | Agriculture | Mining | Land | Notes |
|---|---|---|---|---|---|
| **Dead** | −95% | No Support | No Support | 1–5 | Result of plundering a colony |
