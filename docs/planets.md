# Planet Types

Each planet type has fixed modifiers for population growth, agriculture, and mining, plus a land-roll range and (where applicable) an ore-deposit range. These modifiers are stored as percentages and feed the per-colony formulas — e.g. a +50% mining planet means `planet_mining_mod = 150` in the formula `mining × … × (planet_mining_mod / 100)`.

> See [Formulas](formulas.md) for how each modifier is applied. See [Colonies & Clustering](colonies.md) for how planets group into clusters.

## Notation

| Term | Meaning |
|---|---|
| **Pop. growth** | `planet_pop_mod` (population growth rate modifier, %) |
| **Agriculture** | `planet_agriculture_mod` (food + raw material output, %) |
| **Mining** | `planet_mining_mod` (ore + mineral output, %) |
| **Industry** | `planet_industry_mod` (consumer-goods output, %) — **added in Patch 106** |
| **Land** | Base land roll range — drives infrastructure capacity. Explore inflates this by 1.2625×–1.50× (see [Exploration](exploration.md#the-explore-land-mod)) |
| **Ore** | Initial ore deposit roll range — caps lifetime ore production |
| **No Support** | That income type cannot be produced on this planet |

A baseline planet has all modifiers at 0% (i.e. `100/100 = 1.0×` in the formulas).

## Industry Modifiers

**Added in Patch 106.** Every colony type now carries an **Industry modifier** that scales consumer-goods output in the [Industry formula](formulas.md#consumer-goods-from-industry) (`industry × … × planet_industry_mod / 100`). The values are folded into the per-type tables below as a new **Industry** column. **Any type not assigned a value has +0% Industry** (no modifier) — e.g. Balanced and Forest.

Highlights: Barren **+50%**, U.Large **+75%**, Cluster Lvl 3 **+30%**, U.Eden / U.Fertile **+25%** — against Gas / U.Rich / U.Spazial **−90%** and Dead **−95%**. Two captured tiers (**Assimilated C0 −30%**, **Infected C0 −20%**) appear only in the [Captured Cluster Variants](#captured-cluster-variants) table.

## Standard Planets

These are the planets you'll encounter while exploring. All can be clustered **except Dead** (see note below).

| Planet | Pop. growth | Agriculture | Mining | Industry | Land | Ore |
|---|---|---|---|---|---|---|
| **Barren** | −50% | No Support | +50% | +50% | 50–935 | 150–500 |
| **Balanced** | +20% | 0% | 0% | 0% | 185–925 | 750–900 |
| **Forest** | −10% | +100% | −25% | 0% | 50–350 | 0–150 |
| **Desert** | −25% | −75% | +100% | −25% | 100–250 | 100–350 |
| **Marshy** | −20% | −50% | −50% | −20% | 50–150 | 0–150 |
| **Rocky** | −25% | No Support | −90% | −20% | 34–121 | 500–3,300 |
| **Icy** | −25% | No Support | −95% | −25% | 24–83 | 1,000–4,500 |
| **Oceanic** | −20% | No Support | −50% | −20% | 10–50 | — |
| **Gas** | 0% | No Support | No Support | −90% | 2–6 | — |
| **Dead** | −95% | No Support | No Support | −95% | 1–5 | — |

**Best for clustering:** Barren and Balanced have the highest land ceilings and are the only mainstream picks for endgame clusters. Forest can be acceptable on a strong roll.

> **Note on Dead:** Dead is a rare roll (it comes from the same uncommon roll table as the U-class planets, not the normal explore pool) and **cannot be clustered, infected, or assimilated**. With 1–5 land it's pure junk — plunder it. It's listed here only for completeness.

> **Land values shown are base rolls.** The Explore action applies a `1.25 × (1 + randrange(1,20)/100)` multiplier on top, so post-explore land is 1.2625×–1.50× the listed ceiling. A Barren rolling 935 base can hit 1,402 useable land in practice. See [Exploration](exploration.md#the-explore-land-mod).

## U-Class Planets

U-class planets are rare, special-purpose, and **cannot be clustered**. They are kept for unique bonuses and stay as standalone colonies.

| Planet | Pop. growth | Agriculture | Mining | Industry | Land | Notes |
|---|---|---|---|---|---|---|
| **U.Eden** | +1,000% | −98% | No Support | +25% | 500–2,000 | Massive population growth — Tax player paradise |
| **U.Fertile** | −50% | +175% | No Support | +25% | 500–2,000 | Best Agriculture planet in the game |
| **U.Large** | −80% | No Support | No Support | +75% | 2,000–10,000 | Huge land for raw infrastructure capacity |
| **U.Rich** | −90% | No Support | +150% | −90% | 11–28 | 10,000–350,000 ore — by far the richest deposit |
| **U.Spazial** | −90% | No Support | No Support | −90% | 1–5 | Best digging planet for artifacts |

Viral and Collective **cannot use U-class planets for income** (infection/assimilation is required, which doesn't apply). They can still use U.Spazial for digging since digging does not require infection.

## Cluster Planet Types

When colonies cluster, the component colonies are **merged into a single colony** whose planet type becomes the cluster type — and that cluster's modifier is the **only** type modifier that then applies. The component planets' individual type modifiers do **not** carry over (the originals are consumed by the merge). What *is* preserved is their **land and infrastructure**, which are summed into the new cluster.

### Standard Clusters (Terran, Aspha Miner, Guardian, Marauder)

| Cluster | Pop. growth | Agriculture | Mining | Industry |
|---|---|---|---|---|
| Cluster Lvl 1 | +10% | +15% | +10% | +10% |
| Cluster Lvl 2 | +20% | +30% | +20% | +20% |
| Cluster Lvl 3 | +30% | +45% | +30% | +30% |

Land and infrastructure are **additive** (summed from the components), while the cluster's pop/agri/mining modifier **replaces** the component planet modifiers. So a C3 with 100,000 summed land applies a flat +30% pop / +45% agri / +30% mining to that whole colony.

### Collective Clusters (Similare)

Collective uses assimilation. A Similare C1 is **a single assimilated planet** — not a 5-planet group like standard clusters. Each tier above multiplies by 4:

| Tier | Underlying planets |
|---|---|
| Similare C1 | 1 |
| Similare C2 | 4 |
| Similare C3 | 16 |
| Similare C4 | 64 |
| Similare C5 | 256 |

Collective is the only race with access to C5.

| Cluster | Pop. growth | Agriculture | Mining | Industry |
|---|---|---|---|---|
| Similare C.1 | +20% | −70% | −50% | −70% |
| Similare C.2 | +20% | −65% | −55% | −65% |
| Similare C.3 | +20% | −60% | −60% | −60% |
| Similare C.4 | +20% | −55% | −65% | −55% |
| Similare C.5 | +20% | −52% | −70% | −52% |

### Viral Clusters (Tainted)

Viral uses infection. A Tainted C1 is **a single infected planet** — not a 5-planet group like standard clusters. Each tier above multiplies by 4, capped at C4:

| Tier | Underlying planets |
|---|---|
| Tainted C1 | 1 |
| Tainted C2 | 4 |
| Tainted C3 | 16 |
| Tainted C4 | 64 |

| Cluster | Pop. growth | Agriculture | Mining | Industry |
|---|---|---|---|---|
| Tainted C.1 | −20% | −20% | −50% | −20% |
| Tainted C.2 | −30% | −25% | −55% | −25% |
| Tainted C.3 | −40% | −30% | −60% | −30% |
| Tainted C.4 | −50% | −35% | −65% | −35% |

### Captured Cluster Variants

When Viral or Collective takes an existing cluster from another race, it converts to an Infected (Viral) or Assimilated (Collective) variant with its own modifier set. These retain the original cluster's planet count. As of **Patch 106**, captured colonies display their own colony prefix: **A.XXXX** (Assimilated) and **T.XXXX** (Tainted/Infected).

| Cluster | Pop. growth | Agriculture | Mining | Industry |
|---|---|---|---|---|
| Assimilated C0 | *(base)* | *(base)* | *(base)* | −30% |
| Assimilated C1 | 0% | −20% | 0% | −20% |
| Assimilated C2 | −5% | −10% | −5% | −10% |
| Assimilated C3 | −10% | 0% | −10% | 0% |
| Infected C0 | *(base)* | *(base)* | *(base)* | −20% |
| Infected C1 | −30% | −10% | −30% | −10% |
| Infected C2 | −35% | 0% | −35% | 0% |
| Infected C3 | −40% | +10% | −40% | +10% |

> **C0 tiers** (Assimilated C0, Infected C0) are the freshly-captured *single* colony before it's clustered up. Their pop/agri/mining modifiers **inherit the captured base planet** (*(base)* above — confirmed by devs), while Patch 106 assigns them a fixed Industry penalty (Assimilated C0 −30%, Infected C0 −20%). Assimilated C3 and Infected C2 carry **+0% Industry** (no value listed in the patch).

### Gordo Colony Types (Patch 106)

The Planetary Fracture system (see [Artifacts → Gordos & Planetary Fracture](artifacts.md#gordos-planetary-fracture-patch-106)) introduced two new gordoed colony types. Once a Gordo fills a colony's land past its threshold, the colony begins gaining planets and takes on one of these types:

| Type | What it is | Modifiers |
|---|---|---|
| **Cluster Base** | A regular single-planet colony that has been gordoed (the pre-C1 gordoed state) | **Inherits the base planet's modifiers** |
| **U-Class Cluster** | A U-class colony gordoed past the threshold — available for **all** U-class types | **Inherits the base U-class planet's modifiers** |

> **Gordoing doesn't change a colony's percentage modifiers** (confirmed by devs) — it only adds land and planets while keeping the underlying planet type's pop/agri/mining/industry mods. A gordoed **U.Large** keeps U.Large's mods; a grown **U.Fertile** keeps its +175% agriculture no matter how many planets it holds (a 125-planet Fertile gets the same agri bonus as a 1-planet Fertile). This makes Gordos the way to scale a U-class colony's land and planet count *without* losing its signature bonus — and notably lets U.Fertile / U.Eden be grown far past their old single-planet ceiling.

