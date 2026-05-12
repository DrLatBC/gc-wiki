# Missions

The NPC mission system is a guided progression track that rewards players for hitting empire milestones. Each mission has a fixed goal (economy, planet count, power rating, infrastructure tech, or specific planet types) and a fixed reward (loyalty, credits, colonies, ships, tech levels, or research-cost reductions).

Only **three races** have a mission track. The remaining races can be played normally but receive no guided progression or mission rewards.

| Race | Has Missions | Track |
|---|---|---|
| [Terran](terran.md) | Yes | Act 1 (9 missions) + Act 2 (9 missions) |
| [Aspha Miner](aspha-miner.md) | Yes | Act 1 (9 missions) + Act 2 (9 missions) |
| [Guardian](guardian.md) | Yes | Act 1 (9 missions) + Act 2 (9 missions) |
| Marauder | No | — |
| Viral | No | — |
| Collective | No | — |

## Recommended strategy

**Max your loyalty up to the 5,000 soft cap first, then use missions to push past it.**

Loyalty is normally hard-capped on the way up by diminishing returns at the 5,000 soft cap — natural loyalty-building (governors, infrastructure, time) hits a wall there. Mission rewards, however, are **flat additions** applied directly via SQL: the script just runs `loyalty = loyalty + N` with no cap check. That means a +250-loyalty mission landing on a colony already sitting at 5,000 pushes it to 5,250 — territory you can't reach by any other means.

The Act 2 tracks alone hand out **+50, +100, +150, +250** stackable loyalty grants. If you trigger those while every colony is parked at 5,000, you walk away with empire-wide loyalty well above the cap and the income gains that come with it.

Practical playthrough order:

1. **Grind every colony up to the 5,000 soft cap first** — through governors, infrastructure, and time — before triggering any high-loyalty mission completion.
2. **Save the big loyalty missions for last.** The +100, +150, +250 grants in Act 2 are worth the most when they land on already-maxed colonies. Triggering them with low underlying loyalty wastes the headroom.
3. Time the credit-burning "building" missions (see costs below) for when your reserves are well above the threshold — completing them with exactly the threshold leaves your treasury at zero.

## Structure

Every race's track follows the same two-act format:

- **Act 1 — Foundations.** Mostly economic and exploration milestones (income/turn, planet count, infrastructure tech, first power-rating thresholds). Rewards are mostly loyalty boosts, small credit/ore grants, and free colonies.
- **Act 2 — Empire.** Larger goals (50–200 planets, 200K–800K PR, specific planet types). Rewards scale up with bigger loyalty grants, multiple free colonies, and unique race-specific ship grants or build unlocks. Each track's final mission grants the same global perk: **infrastructure research cost cut to 1/10** for the rest of the game.

## Reward types

| Reward | Effect |
|---|---|
| Loyalty | Flat loyalty added to every colony you own (+20 → +250 depending on mission tier) |
| Credits | One-shot credit grant |
| Ore | One-shot ore grant (Guardian Act 1 m_1 only) |
| Free colonies | Auto-triggers exploration successes — 1 to 3 new planets joining your empire |
| Infra tech levels | +2 or +5 levels to a specific infrastructure technology, equivalent to skipping that much research |
| Ship grants | Free units of a race-unique ship (Guardian's Kal-Zul Destroyer K-Class, Aspha's alien class-G ships) |
| Build unlock | Ability to construct a race-unique ship type from then on (Aspha Act 2 m_1) |
| Research-cost reduction | Final mission only — `resstart` and `resreq` divided by 10, permanently slashing all infrastructure research costs |

## Costs

Some "building" missions in each track (Government Control Center, Asphalt Temple/Arch, Guardian Obelisk, Kal-Zul Ships) **deduct credits on completion** equal to the credit-reserve threshold required. If you complete the mission with exactly the threshold amount, you finish with zero credits. Hit the goal with margin.

Notable cost-burning missions:

| Race | Mission | Credit cost |
|---|---|---|
| Terran | Act 1 m_5 (Government Control Center) | 5,000,000 |
| Terran | Act 2 m_1 (Financial crisis) | 50,000,000 |
| Guardian | Act 1 m_8 (Kal-Zul Ships) | 25,000,000 |
| Guardian | Act 2 m_7 (Guardian Obelisk) | 200,000,000 |
| Aspha | Act 1 m_4 (Asphalt Temple) | 500,000 |
| Aspha | Act 1 m_6 (Asphalt Arch) | 8,000,000 |
| Aspha | Act 1 m_8 (Great Asphalt Arch) | 40,000,000 |
| Aspha | Act 2 m_1 (Construction cost) | 40,000,000 |

## Race tracks

- [Terran Missions](terran.md) — Commercial / Industry / Agriculture empire builder. No ship rewards; pure economy & colony progression.
- [Aspha Miner Missions](aspha-miner.md) — Industry / Mining / Tax. Grants alien class-G ships and unlocks the ability to build them in Act 2.
- [Guardian Missions](guardian.md) — Housing-driven energy empire. Grants Kal-Zul Destroyer K-Class ships and includes a one-off Gas-planet credit windfall.
