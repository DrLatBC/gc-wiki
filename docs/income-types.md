# Income Types

There are five income types in Galactic Conquest: Tax, Commercial, Agriculture, Industry, and Mining. Each is associated with an infrastructure type that players research and build on their colonies.

Players can mix income types but should focus on one. The optimal meta for all income types is to put **5 levels into Housing research first**, then dump all remaining research into the chosen income type. This minimizes the land wasted on Housing buildings while maintaining enough population to staff other infrastructure.

Each race has a base income modifier per income type. Research levels multiply on top of that base at **+10% per level** for most income types (+8% for Commercial CG production, +40% for Mining minerals).

> Formulas below are simplified for readability. For the canonical, full-fidelity versions — including raw-material costs, resource-limited fallbacks, batched-turn handling, and the empire-wide vs per-colony distinction — see the **[Formulas](formulas.md)** page.

## Tax (Housing)

Tax income converts population into credits. Population is fed by Food (required) and Consumer Goods (optional income boost).

**Formula:** `((Population / 2) + (Population × Loyalty / 5000)) × Race Tax Modifier × Turns`

- Loyalty maxes at 5,000 and is trivial to raise for most races (costs a small number of turns)
- At 5,000 loyalty the loyalty term equals the base population term — effectively doubling tax income
- Guardians **cannot raise loyalty** — an intentional nerf since Tax is their only viable income path

## Commercial

Commercial produces a flat **empire-wide** credit income (summed across every commercial building on every colony) plus per-colony Consumer Goods. The credit half is the most stable income type in the game — no market dependency, no resource inputs — but generally the weakest at equivalent research.

**Empire credit income:**
`(Total Commercial + (Total Commercial × Research × 0.1)) × 5 × Race Commercial Modifier × Turns`

**Per-colony CG production** *(requires Commercial ≥ 5 and Commercial Research ≥ 5; consumes 2 Raw Materials per building per turn)*:
`Commercial × ((Research × 0.08) + 1) × Race Commercial Modifier × Turns`

- Credits do not rely on the market or any resource inputs
- CG production does require Raw Materials and falls back to a reduced output when RM runs low
- Commercial also grants a synergy bonus to Agriculture food output when ≥5 Commercial and ≥5 Commercial Research are present

## Agriculture

Agriculture produces equal quantities of Food and Raw Materials. Food is the central resource of the economy, making Agriculture extremely valuable when demand is high.

**Formula (each output):**
`Agriculture × ((Research × 0.1) + 1) × (Planet Agriculture Mod / 100) × Race Agriculture Modifier × Turns`

- Food and Raw Materials are produced at the **same rate** — the same number of each per turn
- Income is entirely market-dependent — if no one is buying food, income collapses
- Raw Materials produced as a byproduct feed Industry players

## Industry

Industry consumes Raw Materials and produces Consumer Goods sold on the player market.

**Formula (full production, requires `Raw Materials ≥ Industry × Turns`):**
`Industry × ((Research × 0.1) + 1) × Race Industry Modifier × Turns`

- **Cost:** 1 Raw Material per industry building per turn
- If Raw Materials run out mid-cycle, output is based on what was available
- Doubly market-dependent — must buy inputs (RM) and sell outputs (CG)

## Mining

Mining produces ship minerals (the primary income source) and ore (a deposit-capped byproduct).

**Minerals (the main output, `sqrt`-scaled):**

```
Minerals = 1 + sqrt(
    Mining × (Planets × 0.3)
    × (1 + 0.4 × Research)
    × (Planet Mining Mod / 100)
    × Race Mineral Modifier
) × Turns
```

**Ore (linear, capped by colony deposit):**
`Mining × (1 + Research × 0.1) × (Planet Mining Mod / 100) × Turns`

- Minerals scale with **planet count in the colony** — wider clusters mean more minerals
- Square-root scaling means stacking Mining buildings has sharp diminishing returns vs. linear ore output
- Research applies a +40% scalar inside the sqrt for minerals, but only +10% for ore
- Ore production stops when the colony's ore deposit runs out

## Viable Income by Race

Listed best to worst within each race:

| Race | Viable Income Types |
|------|-------------------|
| Guardian | Tax |
| Aspha Miner | Tax, Mining, Industry |
| Marauder | Agriculture, Commercial |
| Terran | Agriculture, Commercial, Industry |
| Collective | Agriculture, Tax |
| Viral | Tax, Commercial, Agriculture |

Income viability is determined purely by racial income modifiers — there is no hidden complexity beyond the numbers.
