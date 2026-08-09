# Ships

The full ship stat reference is maintained as a public spreadsheet:
**[Vigi's GC Shiplist](https://docs.google.com/spreadsheets/d/13_0zDPWB9EX1YwlMKWCjfOeG9KYjIC8uHS6Z1B8kVAg/edit?gid=1753353631#gid=1753353631)**

This page explains how to read and apply those stats.

## Ship Classes

Each race has a unique shiplist of ~15 race-specific ships plus access to ~20 neutral ships. Ship research unlocks the full list and takes less than a day — it has minimal long-term impact. The real depth is in composition.

| Race | Ship Prefix |
|------|------------|
| Terran | T., P. |
| Aspha Miner | M., A. |
| Guardian | G. |
| Marauder | D. |
| Viral | V., B. |
| Collective | C. |
| Neutral | F., Strafez, Light, C. Class |

Viral can reverse engineer 3 ships from the Terran, Marauder, and Aspha Miner lists (excluding P., D., and G. class ships). This selection can be changed every month. This allows for supreme flexability and tailoring your ship list against your opponent specifically. Need to fight a lot of guards? Load up on missile boats, pesky marus bothering you? Grab gar/epi and go nuts. 

### Ultimate Weapon (UW) Ships

UW ships appear in the shiplist but have 0 build rate — they cannot be constructed. They are historical relics from an earlier era of the game that were removed for balance reasons. All remaining UW ships in active fleets have been hunted down and destroyed by players. They are trophies only.

## Key Stats

### Power Rating (PR)

PR determines stack order in battle and is used to calculate valid attack targets. It has **no direct impact on combat outcome**. Two ships with identical weapon/hull ratios but different PR values are equally effective — the lower PR ship simply builds in larger quantities for the same turn cost.

The stats that actually matter in combat are: **Range, Weapon, Hull, weapon types, and shield values.**

### Range

Determines firing order within a stack exchange. Higher range fires first. On a tie, the defender fires first.

Range is one of the most impactful stats in the game — firing before your opponent means they return fire with fewer surviving ships.

### Weapon & Hull

Raw damage output and damage capacity per ship. The ratios that matter most:

- **Weapon/PR ratio** — damage efficiency relative to stack size
- **Hull/PR ratio** — survivability relative to stack size

A ship with a high hull/PR ratio is hard to kill relative to its stack position. A ship with a high weapon/PR ratio deals disproportionate damage. Understanding these ratios is the foundation of fleet building.

### Weapon Types

Each ship's weapon value is split across one or more of 4 types:

- Energy
- Kinetic  
- Missile
- Chemical

Weapon type only matters in relation to the target's shields.

### Shield Values

Each ship has a shield value (positive or negative percentage) against each weapon type. Shield values are damage modifiers on incoming attacks of that type:

- **Positive shield** — reduces incoming damage by that percentage. A 99% shield effectively nullifies that weapon type entirely.
- **Negative shield** — increases incoming damage. A -99% shield doubles incoming damage.

Defense is asymmetrical — a hard counter (high positive shield) is vastly more powerful than a hard vulnerability (high negative shield). A well-matched fleet can defeat a numerically superior opponent entirely on the basis of weapon/shield matchups.

### Net Shield

The sum of all shield values. A useful quick reference for overall defensive profile, but misleading in isolation — a ship with 0 net shield could have +99% energy and -99% kinetic, making it a lethal counter to kinetic ships and a free kill for energy ships.

### No Retal (NR) & No Def (ND)

Govern return fire eligibility (see [Battle Mechanics](battle-mechanics.md)):

| Flag | Effect |
|------|--------|
| NR = YES | This ship cannot be returned fire against |
| ND = YES | This ship cannot return fire when attacked |

### Cap Chance

When a ship with a cap chance destroys enemy ships, it salvages this percentage of the kills and adds them to its own fleet immediately. For example, a 75% cap chance on 100 kills recovers 75 ships. Salvaged ships are available for use in subsequent attacks.

**Viral (V-class):** Captured ships are reverse engineered and kept permanently as part of the Viral fleet, allowing virals to choose their own shiplist. 

**Collective:** Captured ships can be used or disbanded. Collective does not reverse engineer — they take and use enemy ships directly. 

### Build Rate & PR Built Per Turn

How fast a ship can be constructed. Build rate is the primary pacing mechanic for combat — the real turn cost of fighting is building ships, not the 5-turn attack cost.

### Upkeep

Credits paid per turn to maintain ships. Upkeep varies by race — the spreadsheet includes separate upkeep columns for Viral and Collective whose racial modifiers differ significantly.

**How upkeep is calculated.** A ship's upkeep is *computed from its stats*, not read from a stored value. The derivation:

```
base   = (power × build_turns) / 10
weapon = total_weapons × (1 + (weapon_types − 1) / 10) × range^1.5
armor  = (hull × 5) × (2 + total_shields)
upkeep = base × (weapon + armor) × race_upkeep_mod
```

- `total_weapons` = sum of the ship's weapon values; `weapon_types` = how many of the 4 weapon types it uses (ships splitting damage across multiple types cost more).
- `total_shields` = sum of the four shield values.
- Then traits adjust it: **÷1.5** if the ship has *no* return-fire and *no* long-range, **×1.5** for long-range, and starbases get an extra **×1.2**.
- `race_upkeep_mod` scales the whole result — cheapest to priciest: **Guardian `0.8` < Marauder `1.9` < Collective `3.3` < Viral `7` < Terran `8` < Aspha Miner `10.1`** (per 1,000,000). This is why the same neutral ship costs a Guardian a fraction of what it costs an Aspha.
- A handful of ships are hardcoded to **0 upkeep**.

See [Formulas → Ship Upkeep](formulas.md#ship-upkeep) for the same formula in the economy context. The takeaway for play: idle scout fleets bleed credits every turn for zero benefit — **disband them when you're done exploring**.

### Mineral Costs

Ship construction consumes ship minerals (Terran Metal, Red Crystal, White Crystal, Rutile, Composite, Strafez Organism). Mineral availability on the market is a real constraint for active combat players.

## Neutral Ships

Neutral ships are available to all races. Upkeep varies per race. Key neutral ship groups:

- **Strafez variants** — specialized ships with unique roles (fodder, runners, queens, kings)
- **C. Class** — Collective-prefixed but usable by all
- **F. Class** — general purpose neutrals
- **Light fighter-drone** — cheap fighter option

## Starbases

Starbases are defensive ships. Building starbases does **not** break Damage Protection, unlike offensive ships.

## Fill Fleet

"Fill fleet" bulk-builds a batch of **dummies** — cheap 1-ship stacks used to fill all 10 battle stacks (see [Battle Mechanics → Always send 10 stacks](battle-mechanics.md#always-send-10-stacks-dummies)). Rather than building them one at a time, it stocks them in a single action. High-PR players keep **20+** dummies pre-built so an intense fight doesn't cost ~10 turns refilling them mid-battle.
