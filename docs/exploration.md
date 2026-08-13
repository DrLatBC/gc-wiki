# Exploration

Exploration is how you grow your colony list before you start fighting for it. Every empire begins with one homeworld and acquires the rest of its planets — keepers and junk alike — through the Explore action. Past the soft cap, further growth means combat.

> See [Colonies & Clustering](colonies.md) for what to do with the planets you find. See [Planet Types](planets.md) for the per-type modifiers and base land ranges.

## The Loop

Exploration is a cycle you repeat until your colony list is built:

1. **Build scanning power** so discoveries come in fast.
2. **Explore** to find a planet.
3. **Judge it** — is it worth a colony slot?
4. **Plunder the junk** to free the slot again.
5. **Cluster the keepers** once you have five of them.

You run this until roughly 50 underlying planets have been folded into clusters — typically two C2s, ten C1s, or a single C3 if you go that far — all buried under a border of junk. After that, exploration is largely done.

## Scanning Power

Exploration runs on your fleet's **scanning power**. Most races build dedicated **Scouts** for this; the Explore page shows how many turns your next discovery will take with the fleet you currently have.

**You want that number at 1** — one turn per discovery. As your empire grows each discovery gets harder and that number creeps upward. When it does, build more scouts to bring it back down.

> **Marauder and Collective have no Scout-class ship — but they can still explore.** Their scanning power comes from regular combat ships, which carry scanner values like anything else in the fleet. The catch is [Damage Protection](battle-mechanics.md#damage-protection-dp): scouts don't break DP, but offensive ships do. So these two races effectively explore **out of DP** — the only way to explore while under DP is to already hold the scanner ships when the DP period begins.

Scouts have no combat value — a fleet of nothing but scouts loses any battle automatically. They exist purely to enable exploration, so **disband them once you're done exploring**. A parked scout fleet bleeds upkeep every turn for no benefit.

## The Explore Action

One Explore attempt yields **one discovery**, and each new colony lands at the **top of your colony list** — the outermost, most exposed position.

### What It Costs

Exploring deducts **no credits**. Its direct cost is **turns**.

What makes it expensive over time is that every planet you already own raises the bar for the next one. The scanning points your next discovery requires:

```
scan required = 5,000 × 1.2 ^ (planets owned − 1)
```

That's a compounding **+20% per planet**. Your fleet's scanning power is what pays it off, and the turn cost is simply how long that takes:

```
turns = (scan required − scan already banked) ÷ fleet scanning power    [rounded up]
```

So as the requirement compounds, each discovery eats more turns unless you keep adding scouts. "Exploring is free" is only true per attempt — the real cost is the scout fleet, in credits to build and upkeep to hold.

### What You Find

The result page reports:

| Field | Meaning |
|---|---|
| Name | Cosmetic prefix (E.NNNN, S.NNNN, etc.) |
| Planet type | Balanced, Barren, Forest, …, U.Large, U.Spazial, … |
| Useable land | The only number that matters for keep/discard |
| Available ore | Initial ore deposit |
| Mineral produced | The ship-mineral type this planet's mining yields |

## Why Land Beats the Listed Ranges

The land you actually get is better than the base ranges on [Planet Types](planets.md). Exploring rolls a value somewhere inside the type's range — **not** at the top of it — then multiplies it:

```
useable land = base roll × 1.25 × (1.01 to 1.20)
```

A flat 25% bonus, plus a random 1–20% on top. So any roll lands at **1.2625× to 1.50×** whatever base value came up, and every account gets this.

A great planet therefore needs two things to go right: a high roll inside the range, *and* a high bonus on top. A Barren whose base range tops out at 935 can reach roughly **1,400 useable land** at the absolute maximum, but a typical Barren lands well below that.

This applies to every planet type — a U.Large can reach around 15,000. Rarely, a "special" roll pushes a planet past even the normal bonus ceiling; that's the **S-class** mega-roll mentioned on [Colonies](colonies.md).

> All land ranges on [Planet Types](planets.md) are **base values**. Add 25–50% to see what an Explore can actually produce.

## Which Planets to Keep

A keeper is a planet worth spending a colony slot on. Everything else gets plundered.

- **Keep** any clusterable planet with roughly **1,050+ useable land**.
- **Keep exactly one U.Spazial** for artifact digging.
- **Plunder everything else.**

That ~1,050 floor is what a 100k+ land C3 needs when built from explored keepers — 125 planets averaging 800+ land each, with room to spare. Holding out for 1,200+ builds bigger clusters but slows exploration considerably.

### Why U-Class Is Junk for Clustering

U-class planets cannot be clustered. Each U.Large, U.Eden, U.Fertile, or U.Rich eats a full colony slot for a single planet — the same slot that could hold a C2 (25 underlying planets) or a C3 (125). Even a 15,000-land U.Large is a poor trade against the cluster strategy.

The exception is **U.Spazial**: keep exactly one for artifact digging (see [Artifacts & Digging](artifacts.md)). Plunder any others you roll.

Players building non-cluster income paths — a U.Eden tax build, a U.Fertile food economy — value U-class planets differently. But for the standard cluster-and-bury strategy, they're junk.

> This is **explore-phase** guidance. Once you have gordos in hand, a U-class colony can be grown into a U-Class Colony Cluster and the calculation changes — see [Colonies → Clusters vs U-Class](colonies.md#clusters-vs-u-class-spending-your-colony-slots).

## The Soft Cap

Most empires plateau at **~55–60 underlying planets** before the turn cost per discovery makes further exploring uneconomical. The typical finished shape for a 15-slot race:

- 2 × C2 — 50 underlying planets across two slots
- ~13 junk colonies acting as ablative armor

Past that point, the only way to grow is to take colonies from other players in combat.

## Plunder for Slot Management

Plunder is the only way to remove a colony from your list. It costs **5 turns** per colony regardless of how many you batch, and returns nothing — its purpose is freeing slots, not income.

Use it to:

1. Discard junk discoveries that didn't clear the keeper threshold.
2. Remove duplicate U-class planets — a second U.Spazial, or any non-Spazial U-class on a cluster build.
3. Shape your colony list for clustering — see [Colonies & Clustering](colonies.md#plundering) for the list-position mechanics.

### The Cluster-Plunder Shortcut

Plundering five junk planets one at a time costs 25 turns. Clustering them into a single junk C1 first (which costs nothing) and plundering that C1 instead frees the same five slots for **5 turns rather than 25**.

This only works when the innermost five colonies of that tier are *all* junk — clustering always takes the innermost five and you can't pick which. See [Colonies & Clustering](colonies.md#clustering) for the cluster mechanic.

## Defending What You Find

Fresh discoveries arrive at the top of your colony list, which is the most attackable position. An attacker can take your outermost three colonies in a single hit (see [Colonies & Clustering](colonies.md#colony-list-defense)).

**The bury rule: always keep at least three junk planets above any cluster.** If a keeper or a newly formed cluster ends up in the outermost three, explore junk immediately to push it back under cover. C2s and C3s especially must never sit that exposed — each one represents dozens of underlying planets.

### The Post-Cluster Burst

When you cluster the innermost five plain colonies of an empire whose other slots are all higher-tier clusters, the new C1 appears at the **outermost** position — fully exposed the moment it forms.

The defense is to bank turns *before* you cluster, so you can immediately explore three or more junk planets on top of it. Bank about **four times** what that burst will cost: roughly 12 turns when discoveries take 1 turn each, 24 when they take 2.
