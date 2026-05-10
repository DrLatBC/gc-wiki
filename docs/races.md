# Races

There are 6 playable races in Galactic Conquest. Race choice determines your base income modifiers, shiplist, clustering mechanic, colony cap, and several unique mechanical rules. It is the most impactful decision a new player makes.

> Three additional non-playable races exist in the game data — KalZul, Berserkers, and Dark Marauders. These are NPC-only and cannot be selected.

## Race Modifiers

All economic modifiers are stored as percentages added to a 1.0× baseline. Convert to a multiplier with `1 + (value / 100)` — e.g. +220% = 3.2× and −95% = 0.05×. These modifiers feed directly into the formulas on the [Formulas](formulas.md) page.

| Race | Tax (Pop) | Agri | Commercial | Industry | Goods Demand | Maintenance | Plunder | Minerals |
|---|---|---|---|---|---|---|---|---|
| Terran | +0% | +20% | +20% | +220% | +350% | +0% | −50% | +0% |
| Aspha Miner | +220% | −50% | −95% | +350% | +0% | −20% | −95% | +2,900% |
| Guardian | −85% | −95% | −99% | −99% | −90% | −25% | −99% | −99% |
| Marauder | −95% | −50% | −95% | −50% | +0% | −95% | +1,900% | −95% |
| Viral | +20% | −20% | −5% | −50% | +100% | +0% | −99% | +0% |
| Collective | −50% | +50% | −95% | −90% | −95% | +0% | +1,100% | −50% |

| Column | Formula variable | Affects |
|---|---|---|
| Tax (Pop) | `race_tax_mod` | Per-population credit yield |
| Agri | `race_agriculture_mod` | Food + Raw Materials output |
| Commercial | `race_commercial_mod` | Empire commercial credits, Commercial CG output |
| Industry | `race_industry_mod` | Industry CG output |
| Goods Demand | `race_good_mod` | Population goods consumption (more consumed → more 5.5/good auto-conversion income) |
| Maintenance | `race_maintenance_mod` | Empire infrastructure upkeep cost |
| Plunder | — | Bonus credits when plundering colonies (no income-cycle effect) |
| Minerals | `race_mineral_mod` | Minerals from mining |

> **Goods Demand quirk:** Counter-intuitively, *higher* goods demand is *better* for income. Population consumes goods, surplus is auto-sold at 5.5 credits/good — so Terran's +350% is the engine behind their tax-with-CGs power, not a penalty.

## Difficulty & Colony Caps

| Race | Difficulty | Max Colonies | Exploration | Missions |
|---|---|---|---|---|
| Terran | Easy | 15 | Yes | Yes |
| Aspha Miner | Easy | 12 | Yes | Yes |
| Guardian | Hard | 10 | Yes | Yes |
| Marauder | Medium | 12 | No | No |
| Viral | Hard | 12 | Yes | No |
| Collective | Hard | 13 | No | No |

## Terran

- **Viable income:** Agriculture, Commercial, Industry
- **Cannot lose their homeworld** — the only race besides Aspha Miner with this protection
- Standard clustering (C1/C2/C3)
- A well-rounded race with strong market-based income options

## Aspha Miner

- **Viable income:** Tax, Mining, Industry
- **Cannot lose their homeworld** — same protection as Terran
- Standard clustering (C1/C2/C3)
- Tax income is capable of producing more credits than any other race/income combination if Food and CGs are available on the market
- Mining is the easiest low-effort income path — requires little active management

## Guardian

- **Viable income:** Tax only
- **Does not consume Food** — population requires no food supply
- **Cannot raise Loyalty** — an intentional nerf. Loyalty directly multiplies Tax income, so Guardians are permanently capped below their theoretical maximum
- Can die if all planets are lost
- Standard clustering (C1/C2/C3)
- PR is determined by infrastructure and ships only, not population

## Marauder

- **Viable income:** Agriculture, Commercial
- **Cannot explore** — all land must be acquired through combat against NPCs or other players
- Standard clustering (C1/C2/C3)
- Can die if all planets are lost
- D-class ships cannot be reverse engineered by Viral

## Viral

- **Viable income:** Tax, Commercial, Agriculture
- Can die if all planets are lost
- Uses **infection** instead of standard clustering
- Cluster sizes use 4 planets per level instead of 5 (Tainted C1–C4)
- Can also infect clusters taken from other races, retaining their original planet count
- Cannot use U-class planets for income (infection required), but can dig on U.Spazial
- **Reverse engineering:** Viral selects 3 ships from the Marauder, Terran, and Aspha Miner shiplists to add to its own. This selection can be changed approximately weekly. P-class, D-class, and G-class ships are excluded from selection
- Viral's native shiplist is weak — flexibility via reverse engineering is their core identity and the tradeoff for their lower income ceiling

## Collective

- **Viable income:** Agriculture, Tax
- Can die if all planets are lost
- Uses **assimilation** instead of standard clustering
- Cluster sizes use 4 planets per level (Similare C1–C5) — the only race with C5 (256 planets)
- **Cannot explore** — all land must be acquired through combat against NPCs or other players
- Can assimilate clusters taken from other races
- Cannot use U-class planets for income, but can dig on U.Spazial
- NPC farming is a viable and indefinite land source, making Collective's aggression requirement manageable even at low player counts
