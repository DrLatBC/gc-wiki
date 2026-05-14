# Exploration

Exploration is how you grow your colony list before you start fighting for it. Every empire begins with one homeworld and acquires the rest of its planets — keepers and junk alike — through the Explore action. Past the soft cap, further growth means combat.

> See [Colonies & Clustering](colonies.md) for what to do with the planets you find. See [Planet Types](planets.md) for the per-type modifiers and base land ranges.

## The Loop

```
[scouts] → [explore] → [classify] → [plunder junk] → [cluster keepers] → repeat
```

You feed the loop until you've turned ~50 underlying planets into clusters (typically two C2s, ten C1s, or a single C3 if you go that far) buried under a border of junk. After that, exploration is largely done.

## Scouts

Every race has a Scout-class ship. You need a fleet of them to explore — total fleet **Scanning power** drives how fast a single discovery completes. The Explore page reports `Turns required to finish exploration with your current fleet` based on this.

The strategic target is **`turns_required = 1`** — one discovery per turn allocated. As your empire grows the per-discovery difficulty climbs and `turns_required` creeps up; that's the signal to buy more scouts.

Scout fleets have no combat value (a pure-scout fleet auto-loses any battle), so they exist only to enable exploration. **Disband them once you're done exploring** — upkeep on a parked scout fleet bleeds credits indefinitely.

## The Explore Action

One submission of the Explore form, with `turns_required` turns allocated, yields **one discovery**. Each discovery lands at the **top of the colony list** (the outermost, most-exposed position).

### Costs

```
explore_credit_cost = 5000 × 1.2 ^ (planet_count - 1)
```

Cost compounds as the empire grows. Early discoveries are nearly free; late discoveries cost meaningfully more credits per attempt.

Turn cost is whatever `turns_required` reads at the time of the explore — buy scouts to keep this at 1.

### What You Find

The result page reports:

| Field | Meaning |
|---|---|
| Name | Cosmetic prefix (E.NNNN, S.NNNN, etc.) |
| Planet type | Balanced, Barren, Forest, …, U.Large, U.Spazial, … |
| Useable land | The only number that matters for keep/discard |
| Available ore | Initial ore deposit |
| Mineral produced | The ship-mineral type this planet's mining yields |

## The Explore Land Mod

The land value rolled by Explore is **not** the base land range listed on [Planet Types](planets.md). Explore applies a multiplier on top:

```
useable_land = base_max_land × 1.25 × (1 + randrange(1, 20) / 100)
```

The `randrange(1, 20)/100` term is a uniform 0.01–0.20 bonus. The total multiplier is **1.2625× to 1.50×** the base max land roll.

**Example.** A Barren has a base land ceiling of 935. Maximum possible explore roll:

```
935 × 1.25 × 1.20 = 1,402.5 useable land
```

This applies to every planet type, U-classes included. A U.Large with a 10,000 base ceiling can roll up to ~15,000 useable land post-mod.

> All land ranges on [Planet Types](planets.md) are **base values**. Add 25–50% on top to see what's actually possible from an Explore.

## Classification

A keeper is a planet worth a colony slot. Everything else gets plundered.

```
keep   = clusterable type AND useable_land ≥ 1050
spaz   = U.Spazial AND you don't already hold one
junk   = everything else
```

The 1050 threshold reflects the practical floor for a 100k+ land C3 (125 keepers × 800+ land each, with headroom). Higher thresholds (1200+) yield bigger clusters but slow exploration significantly.

### Why U-Class Is Junk for Clustering

U-class planets cannot be clustered. Each U.Large, U.Eden, U.Fertile, or U.Rich consumes a full colony slot for a single planet — the same slot that could hold a C2 (25 underlying planets) or C3 (125). Even a 15k-land U.Large is a slot waste against the cluster strategy.

The exception is **U.Spazial**: keep exactly one for artifact digging (see [Artifacts & Digging](artifacts.md)). Plunder any further U.Spazials you roll.

Players who specialize in non-cluster income paths (a U.Eden tax build, a U.Fertile food economy) value U-class planets differently — but for the standard cluster-and-bury strategy, they're junk.

## The Soft Cap

Most empires plateau at **~55–60 underlying planets** of exploration before the per-discovery turn and credit costs make further exploring uneconomical. The typical "done" shape for a 15-slot race:

- 2 × C2 (50 underlying planets across 2 slots)
- ~13 × junk C0s as ablative armor

Past the soft cap, the only way to grow is to take colonies from other players in combat.

## Plunder for Slot Management

Plunder is the only way to remove a colony from your list. Each plunder costs **5 turns** per colony, regardless of batch size, and gives nothing back — its purpose is freeing slots, not income.

Use it to:

1. Discard junk discoveries that didn't clear the keeper threshold.
2. Remove duplicate U-class planets (a second U.Spazial, any non-Spazial U-class on a cluster build).
3. Shape the colony list for clustering — see [Colonies & Clustering](colonies.md#plundering) for the list-position mechanics.

### The Cluster-Plunder Shortcut

Plundering 5 individual junk planets costs 25 turns. Clustering them into a single junk C1 first (0 turns) and then plundering the C1 (5 turns) frees the same 5 slots for **5 turns instead of 25**.

This only works when the innermost 5 colonies of the relevant tier are *all* junk — clustering takes the innermost 5, you can't choose which. See [Colonies & Clustering](colonies.md#clustering) for the cluster mechanic.

## Defensive Considerations

Fresh discoveries land at the top of the colony list — the outermost, most-attackable position. An attacker can take the outermost 3 colonies in a single hit (see [Colonies & Clustering](colonies.md#colony-list--defense)).

The bury rule: **always keep ≥3 junk planets above any cluster**. If a fresh keeper or a freshly-formed cluster ends up at positions 0–2, immediately explore enough junk discoveries to push it back under cover. C2s and C3s especially must never sit in the outermost 3 — they represent dozens of underlying planets each.

### The Post-Cluster Burst

When you cluster the innermost 5 C0s of an empire whose other slots are all higher-tier clusters, the new C1 lands at the **outermost** position. The defense is to bank turns *before* clustering so you can immediately burst-explore 3+ junk discoveries on top of the new C1.

Rule of thumb: bank **4× the burst cost** in turns before initiating a cluster that will surface (so 12 turns at `turns_required = 1`, 24 turns at `turns_required = 2`).
