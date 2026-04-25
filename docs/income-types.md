# Income Types

There are five income types in Galactic Conquest: Tax, Commercial, Agriculture, Industry, and Mining. Each is associated with an infrastructure type that players research and build on their colonies.

Players can mix income types but should focus on one. The optimal meta for all income types is to put **5 levels into Housing research first**, then dump all remaining research into the chosen income type. This minimizes the land wasted on Housing buildings while maintaining enough population to staff other infrastructure.

Each race has a base income modifier per income type. Research levels multiply on top of that base at **+10% per level**. At level 100 that's a 1,000% increase; at the cap of 250 (after 5 housing) it's a 2,500% increase.

## Tax (Housing)

Tax income converts population into credits. Population is fed by Food (required) and Consumer Goods (optional income boost).

**Formula:** `((Population × (Loyalty / 5000)) + (Population / 2)) × Race Tax Modifier`

- Loyalty maxes at 5,000 and is trivial to raise for most races (costs a small number of turns)
- Guardians **cannot raise loyalty** — an intentional nerf since Tax is their only viable income path
- High base PR is the main drawback — Tax players are large targets

## Commercial

Commercial produces credits and a small amount of Consumer Goods directly, with no market dependency. It is the most stable income type but generally the weakest.

**Formula:** `(Commercial × ((Research × 0.5) + 5)) × Race Commercial Modifier`

**CG production:** `(Commercial × ((Research × 0.08) + 1)) × Race Commercial Modifier`

- Does not rely on the market
- Generally considered worse than market-dependent income types at equivalent research levels

## Agriculture

Agriculture produces vast quantities of Food and Raw Materials, sold on the player market. Food is the central resource of the economy making Agriculture extremely valuable when demand is high.

**Formula:** `((Agriculture × ((Research × 0.1) + 1)) × Race Agriculture Modifier) × Planet Agriculture Modifier`

- Income is entirely market-dependent — if no one is buying food, income collapses
- Raw Materials produced as a byproduct feed Industry players

## Industry

Industry consumes Raw Materials and produces Consumer Goods sold on the player market.

**Formula:** `(Industry × ((Research × 0.1) + 1)) × Race Industry Modifier`

- Requires a steady supply of Raw Materials from Agriculture players
- Doubly market-dependent — must buy inputs and sell outputs

## Mining

Mining produces ship minerals sold on the player market, with a small bonus to Ore production.

**Formula:** `(Planets in Colony × ((0.13 × Research) + 1)) × Race Mining Modifier`

- Ore bonus is a fun side effect, not a meaningful income source
- Planet count in the formula is coded in strict cluster increments: 1, 5, 25, or 125 (see [Colonies](colonies.md))
- Infected/Assimilated clusters always count as 1 planet in this formula

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
