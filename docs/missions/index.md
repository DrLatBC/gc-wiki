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

**Claim loyalty missions as soon as you qualify — the reward is a permanent cap increase, not a one-time top-up.**

**5,000 is your base personal loyalty cap.** Normal loyalty (the passive climb that runs while you hold Consumer Goods; see [Income Types → Tax](../income-types.md#tax-housing)) climbs to that ceiling and stops. Loyalty-reward missions **raise the ceiling itself**: as of **Patch 106** the personal cap is "5,000 base, with bonuses adding on for missions you've completed," so a +250-loyalty mission lifts your cap to 5,250 and leaves it there. The Act 2 tracks alone hand out **+50, +100, +150, +250**, and they stack.

This replaced the older behaviour, where completing a mission dumped a one-time lump of loyalty onto the colonies you happened to own at that moment. The practical consequences are the reverse of what that used to imply:

- **You cannot waste a loyalty reward by claiming it early.** Your current loyalty is irrelevant to the reward — the extra ceiling is banked permanently, and colonies climb into it afterwards on their own.
- **Earlier is strictly better.** The cap raise is permanent but the growth toward it is per-turn, so claiming sooner gives your colonies longer to fill the new headroom.

Practical playthrough order:

1. **Complete loyalty missions the moment you meet their goals.** There is no reason to hold one back.
2. **Keep Consumer Goods in stock.** A raised cap only pays off while that passive climb is actually running underneath it.
3. Time the credit-burning "building" missions (see costs below) for when your reserves are well above the threshold — completing them with exactly the threshold leaves your treasury at zero.

## Structure

Every race's track follows the same two-act format:

- **Act 1 — Foundations.** Mostly economic and exploration milestones (income/turn, planet count, infrastructure tech, first power-rating thresholds). Rewards are mostly loyalty-cap raises, small credit/ore grants, and free colonies.
- **Act 2 — Empire.** Larger goals (50–200 planets, 200K–800K PR, specific planet types). Rewards scale up with bigger loyalty-cap raises, multiple free colonies, and unique race-specific ship grants. Each track's final mission grants the same temporary perk: **infrastructure research cost cut to 1/10**, which stays worthwhile for roughly the next 13 research levels — that is how long 20%-per-level growth takes to climb back to where the cost started.

## Reward types

| Reward | Effect |
|---|---|
| Loyalty | **Permanent increase to your personal loyalty cap** (+20 → +250 depending on mission tier), stacking on top of the 5,000 base — not a one-time top-up of current loyalty |
| Credits | One-shot credit grant |
| Ore | One-shot ore grant (Guardian Act 1 m_1 only) |
| Free colonies | Auto-triggers exploration successes — 1 to 3 new planets joining your empire |
| Infra tech levels | +2 or +5 levels to a specific infrastructure technology, equivalent to skipping that much research |
| Ship grants | Free units of a race-unique ship (Guardian's Kal-Zul Destroyer K-Class, Aspha's alien G.Livid). These gift ships **cannot be built** — what the missions award is all you ever get |
| Research-cost reduction | Final mission only — `resstart` and `resreq` divided by 10. Temporary buff: roughly the next 13 research levels are discounted before normal cost growth restores parity |

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
- [Aspha Miner Missions](aspha-miner.md) — Industry / Mining / Tax. Grants 27 alien G.Livid across the track.
- [Guardian Missions](guardian.md) — Housing-driven energy empire. Grants Kal-Zul Destroyer K-Class ships and includes a one-off Gas-planet credit windfall.
