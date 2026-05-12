# Battle Mechanics

Combat in Galactic Conquest is predictive, not reactive. Battles are resolved algorithmically based on fleet composition and stance. Understanding the rules engine is the foundation of competitive play.

## Attacking

Attacking costs **5 turns**. The real turn cost of combat is ship construction — the attack itself is trivial.

### Attack Range

| Situation | Range |
|-----------|-------|
| Punch up (attack stronger player) | Up to 2× your PR |
| Punch down (attack weaker player) | Down to your PR ÷ 1.3 |
| Fed war punch down | Down to your PR ÷ 1.5 |

Fed war only widens the punch-down floor. The 2× punch-up ceiling is universal.

### Battle Outcomes

The attacker must kill at least 10% of the defender's ship PR to win any colonies. Outcome is determined by damage dealt:

| Defender Ship PR Killed | Colonies Taken |
|------------------------|---------------|
| ≥10% | 1 |
| ≥20% | 2 |
| ≥40% | 3 |

The winner is the side that loses the least PR. Exception: if all ships in the 10 active stacks are destroyed, the other side wins regardless of PR lost.

### Counter Attacks

If attacked, you can counter-attack from any PR difference — no range restriction. Counters expire approximately 1 week after being received. Cannot be used to enslave.

## Stacks

Ships are organized into stacks. Each ship type occupies one stack — duplicate ship types merge into a single stack automatically.

- Maximum of **10 stacks** enter battle. Additional stacks beyond 10 are ignored.
- In round 1, stacks are ordered **highest PR to lowest PR** (top to bottom).
- Each stack is paired with the opposing stack at the same position.

## Battle Rounds

### Round 1

1. Each stack is paired with the opposing stack at the same position.
2. The stack with higher **Range** fires first. Ties go to the **defender**.
3. Kills are calculated (see Combat Formula below).
4. Surviving units of the receiving stack fire back (subject to ND/NR rules).
5. Unpaired stacks (when one side has more stacks) **flank** — firing at a random surviving enemy stack.

## Battle Rounds

Battles last exactly **2 rounds**.

### Round 1

1. Each stack is paired with the opposing stack at the same position.
2. The stack with higher **Range** fires first. Ties go to the **defender**.
3. Kills are calculated (see Combat Formula below).
4. Surviving units of the receiving stack fire back (subject to ND/NR rules).
5. Unpaired stacks (when one side has more stacks) **flank** — firing at a random surviving enemy stack.

### Between Rounds

Destroyed stacks are removed. Surviving stacks collapse upward to fill gaps and are re-paired by surviving stack number (not PR). Ships that were paired in round 1 may now be unpaired and able to flank in round 2.

### Round 2

Same sequence as round 1 using the restacked order. Ships that couldn't flank in round 1 may now flank if their opposing stack was destroyed.

## Combat Formula

### Kills Calculation

```
Kills = (Firing Units × Weapon × Stance Modifier × Shield Modifier) ÷ Target Hull
```

- Damage is dealt in **whole ship kills only** — no partial damage carries over.
- Shield modifiers apply per weapon type independently (see Shields below).

### Stance Modifiers

| Stance | Attacker Efficiency | Defender Efficiency |
|--------|--------------------|--------------------|
| Careful | -50% | -50% |
| Normal | -5% | 0% |
| Aggressive | +75% | +99% |

The attacker efficiency modifier applies to **all attacker damage throughout the entire battle**, including return fire.

## Weapon & Shield Types

There are 4 weapon types and 4 corresponding shield types:

- Energy
- Kinetic
- Missile
- Chemical

Each ship has weapon values split across one or more types, and shield values (positive or negative) against each type.

### Shield Interaction

Shield values are percentage modifiers on incoming damage of that type:

- **Positive shield** reduces incoming damage. A 99% shield reduces damage by 99% — effectively nullifying that weapon type.
- **Negative shield** increases incoming damage. A -99% shield doubles incoming damage.

Defense is asymmetrical — a hard counter (99% shield) is vastly more powerful than a hard vulnerability (-99% shield). A perfect counter can win from an impossibly low PR disadvantage if weapon types align.

## Return Fire (RF) & No Defense (ND)

When a stack is fired upon, it may fire back **before** taking its normal turn. This return fire deals **50% of the ship's weapon value**, after stance modifiers are applied.

Return fire is governed by two flags per ship:

| Flag | Effect |
|------|--------|
| **No Retal (NR) = YES** | This ship cannot be returned fire against |
| **No Def (ND) = YES** | This ship cannot return fire when attacked |

Return fire rules apply identically to direct stack engagements and flanks.

### Return Fire Sequence (per stack exchange)

1. Higher range fires (attacker penalty applied if attacker)
2. If target has NR=NO **and** attacker has ND=NO → target returns fire at 50% penalized weapon value
3. Surviving units take their normal combat turn
4. If fired upon, return fire triggers again under same conditions

## Flanking

When one side has more stacks than the other, unpaired stacks **flank** — they fire at a random surviving enemy stack. Flanking follows all normal combat rules including return fire, ND, and NR.

## Power Rating (PR)

PR determines stack order and attack range. It has **no direct impact on combat outcome**. A ship with 50 PR and a ship with 500 PR are equally effective if their hull/weapon ratios are proportional — the lower PR ship simply builds in larger quantities for the same turn cost.

PR is composed of infrastructure and ships. Population does **not** contribute to PR.

PR refreshes only on specific actions (logging in, attacking, building ships, etc.). Building infrastructure does not trigger a refresh, so PR can jump unexpectedly on the next refresh.

## Damage Protection (DP)

DP is granted when a defender loses 40% or more of their fleet in a single engagement while defending. It can also trigger after losing colonies.

- Maximum colonies lost in one DP period: **4** (typically as 1+3 or 2+2 across multiple attacks)
- Losing 3 in one period is the practical norm; 4 is possible but rare
- DP is lifted when: the timer expires, the player builds offensive ships, or the player attacks
- Scouts and Starbases do not break DP

## Newbie Protection (NP)

Players below **5,000 PR** cannot be attacked. Crossing 5,000 PR removes NP permanently for that session.

## Attack Stances

### Normal
Standard attack. -5% attacker efficiency, defender at 100%.

### Careful
Both sides at -50% efficiency. Favors high hull ships that are hard to kill. Rarely wins more than 1-2 colonies. Avoid using with high range or high attack ships.

### Aggressive
+75% attacker efficiency, +99% defender efficiency. Best used with high range ships to maximize first-strike damage before the defender can respond. High risk — certain ship matchups will destroy an aggressive attacker before they can deal meaningful damage.

## PR formula

((Planet Infra * (5+(land/250000))) + (Planet Count * 1000)) + fleet power

## Further reading

- [Exule's Game Guide](https://gcc.wrindustries.com/hef.cfm?&5639&f=hef_detail&hi=6223&ch=101) — 2008 legacy combat reference, periodically updated. Predates several engine changes, so verify against current game behavior before relying on specific numbers.
