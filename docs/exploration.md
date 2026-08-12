# Exploration

Exploration is how you grow your colony list before you start fighting for it. Every empire begins with one homeworld and acquires the rest of its planets — keepers and junk alike — through the Explore action. Past the soft cap, further growth means combat.

> See [Colonies & Clustering](colonies.md) for what to do with the planets you find. See [Planet Types](planets.md) for the per-type modifiers and base land ranges.

## The Loop

```
[scouts] → [explore] → [classify] → [plunder junk] → [cluster keepers] → repeat
```

You feed the loop until you've turned ~50 underlying planets into clusters (typically two C2s, ten C1s, or a single C3 if you go that far) buried under a border of junk. After that, exploration is largely done.

## Scouts

Most races have a Scout-class ship. What actually drives exploration is your total fleet **Scanning power** — it determines how fast a single discovery completes, whether that scanning comes from dedicated scouts or from regular ships. The Explore page reports `Turns required to finish exploration with your current fleet` based on this.

> **Marauder and Collective have no Scout-class ship — but they can still explore.** Their scanning power comes from regular combat ships, which carry scanner values like anything else in the fleet. The catch is [Damage Protection](battle-mechanics.md#damage-protection-dp): scouts don't break DP, but offensive ships do. So these two races effectively explore **out of DP** — the only way to explore while under DP is to already hold the scanner ships when the DP period begins.

The strategic target is **`turns_required = 1`** — one discovery per turn allocated. As your empire grows the per-discovery difficulty climbs and `turns_required` creeps up; that's the signal to buy more scouts.

Scout fleets have no combat value (a pure-scout fleet auto-loses any battle), so they exist only to enable exploration. **Disband them once you're done exploring** — upkeep on a parked scout fleet bleeds credits indefinitely.

## The Explore Action

One submission of the Explore form, with `turns_required` turns allocated, yields **one discovery**. Each discovery lands at the **top of the colony list** (the outermost, most-exposed position).

### Costs

The Explore action itself **deducts no credits** — its direct cost is **turns**. What scales with empire size is the *scanning requirement* per discovery:

```
explore_requirement = 5000 × 1.2 ^ (planet_count - 1)
```

This is the exploration-points needed for the next discovery (source: `res_researchstart = 5000`, `res_researchincrease = 1.2`, i.e. compounding +20% difficulty). It drives the **turn** cost via your fleet's scanning power:

```
turns_required = ceil((explore_requirement − current_explore_points) / fleet_scanning_power)
```

As the empire grows the requirement compounds, so each discovery needs more scan points → more turns, unless you add scouts. The strategic target is `turns_required = 1`; buy more scouts to hold it there.

**Credits do enter indirectly** — exploring requires a scout fleet, and scouts cost credits to build and carry ongoing upkeep. So "exploring is free" is only true per-attempt; the scanning power that keeps `turns_required` low is paid for in ships.

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

The land value rolled by Explore is **not** simply the base land range listed on [Planet Types](planets.md). Explore first rolls a **uniform random value across the planet type's full range**, then applies multipliers on top:

```
useable_land = floor( round( randrange(land_min, land_max) × 1.25 ) × (1 + randrange(1, 20) / 100) )
```

So each roll starts somewhere in `[land_min, land_max]` (not at the max), then gets a flat **×1.25**, then a uniform **0.01–0.20** bonus (the `randrange(1,20)/100` term). The bonus multiplier is universal because every account has premium. Net effect: any given roll is `1.2625× – 1.50×` of *whatever* base value was rolled — so the *best possible* roll is `land_max × 1.50`, but a typical roll is much lower.

**Example (maximum possible).** A Barren with a base land ceiling of 935 can roll at most:

```
935 × 1.25 × 1.20 = 1,402.5 useable land
```

A typical Barren rolls well below this, since the base is random across its range. This multiplier applies to every planet type, U-classes included — a U.Large with a 10,000 base ceiling can reach ~15,000 at the top end. (There is also a rare "special" multiplier that can push a roll *above* the 1.50× ceiling — the "S-class" mega-roll referenced on [Colonies](colonies.md).)

> All land ranges on [Planet Types](planets.md) are **base values**. Add 25–50% on top to see what's actually possible from an Explore.

## Classification

A keeper is a planet worth a colony slot. Everything else gets plundered.

```
keep   = clusterable type AND useable_land ≥ 1050
spaz   = U.Spazial AND you don't already hold one
junk   = everything else
```

The 1050 threshold reflects the practical floor for a 100k+ land C3 built from explored keepers (125 × 800+ land each, with headroom). Higher thresholds (1200+) yield bigger clusters but slow exploration significantly.

### Why U-Class Is Junk for Clustering

U-class planets cannot be clustered. Each U.Large, U.Eden, U.Fertile, or U.Rich consumes a full colony slot for a single planet — the same slot that could hold a C2 (25 underlying planets) or C3 (125). Even a 15k-land U.Large is a slot waste against the cluster strategy.

The exception is **U.Spazial**: keep exactly one for artifact digging (see [Artifacts & Digging](artifacts.md)). Plunder any further U.Spazials you roll.

Players who specialize in non-cluster income paths (a U.Eden tax build, a U.Fertile food economy) value U-class planets differently — but for the standard cluster-and-bury strategy, they're junk.

> This is **explore-phase** guidance. Once you have gordos in hand, a U-class colony can be grown into a U-Class Colony Cluster and the calculation changes — see [Colonies → Clusters vs U-Class](colonies.md#clusters-vs-u-class-spending-your-colony-slots).

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

Fresh discoveries land at the top of the colony list — the outermost, most-attackable position. An attacker can take the outermost 3 colonies in a single hit (see [Colonies & Clustering](colonies.md#colony-list-defense)).

The bury rule: **always keep ≥3 junk planets above any cluster**. If a fresh keeper or a freshly-formed cluster ends up at positions 0–2, immediately explore enough junk discoveries to push it back under cover. C2s and C3s especially must never sit in the outermost 3 — they represent dozens of underlying planets each.

### The Post-Cluster Burst

When you cluster the innermost 5 C0s of an empire whose other slots are all higher-tier clusters, the new C1 lands at the **outermost** position. The defense is to bank turns *before* clustering so you can immediately burst-explore 3+ junk discoveries on top of the new C1.

Rule of thumb: bank **4× the burst cost** in turns before initiating a cluster that will surface (so 12 turns at `turns_required = 1`, 24 turns at `turns_required = 2`).
