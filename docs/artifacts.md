# Artifacts & Digging

Artifacts are special items that can be used offensively, defensively, or for economic gain. They are obtained by digging on colonies and can be combined in the Capsule Lab to produce more powerful artifacts.

## Digging

Digging costs turns and is performed on any colony with excavation. The meta chunk size is **7 turns per dig** — this balances efficiency against the lockout system (see below).

### Lockout System

When you find a specific artifact type within a dig session, that artifact type is locked out for the remainder of the session. For example, if you find a Small Time Capsule on turn 1 of a 7-turn dig, you cannot find another Small Time Capsule for the remaining 6 turns. Smaller chunks mean more opportunities to roll the same artifact type again.

### Factors That Affect Digging

| Factor | Effect |
|--------|--------|
| **Planet Type** | U.Spazial is best for most artifact types. Ocean is best during Uncommon dig time and acceptable otherwise. Gas is the distant 3rd best, but will do in a pinch. |
| **Race** | Some races have positive or negative dig modifiers. |
| **Turns Used** | Chunk size affects results — 7 turns is the meta. |
| **Time of Day** | The biggest factor. See dig times below. |
| **Luck** | Increases artifact find rates. See Luck artifacts. |

### Dig Times (Server Time — Eastern Time)

The dig schedule runs as **four groups per day**, each a 4-hour window, on a 6-hour cadence:

| Group | Window (ET) |
|---|---|
| Group 1 | 18:00 – 22:00 |
| Group 2 | 00:00 – 04:00 |
| Group 3 | 06:00 – 10:00 |
| Group 4 | 12:00 – 16:00 |

(Group numbering matches the in-game `com_dig_times` schedule, which starts the day's groups at the 18:00 window.)

Outside these four windows, **Default Dig** is active (low yields).

Each group is structured as **two waves** separated by an internal Default Dig gap. The pattern below is identical for all four groups — times are offsets from the group's start hour:

| Offset | Type | Duration |
|---|---|---|
| **Wave 1** | | |
| :00 – :30 | Common | 30 min |
| :31 – :45 | **Rare** | 15 min |
| :46 – +1:30 | Common | 45 min |
| +1:31 – +1:35 | **Mixed** | 5 min |
| +1:36 – +2:29 | *Default Dig* | ~55 min |
| **Wave 2** | | |
| +2:30 – +2:45 | Common | 15 min |
| +2:46 – +2:50 | **Mixed** | 5 min |
| +2:51 – +3:00 | Common | 10 min |
| +3:01 – +3:20 | **UnCommon** | 20 min |
| +3:21 – +4:00 | Common | 40 min |

So a full Group 1 (18:00–22:00 ET) plays out as:

| Time (ET) | Type |
|---|---|
| 18:00 – 18:30 | Common |
| 18:31 – 18:45 | **Rare** |
| 18:46 – 19:30 | Common |
| 19:31 – 19:35 | **Mixed** |
| 19:36 – 20:29 | Default Dig |
| 20:30 – 20:45 | Common |
| 20:46 – 20:50 | **Mixed** |
| 20:51 – 21:00 | Common |
| 21:01 – 21:20 | **UnCommon** |
| 21:21 – 22:00 | Common |

**Rare types per group:**

- **Rare:** 15 minutes (Wave 1)
- **UnCommon:** 20 minutes (Wave 2)
- **Mixed:** two 5-minute windows (one per wave)
- Across the day that's 1 hour of Rare, 1h 20m of UnCommon, and 40 minutes of Mixed total

> The current dig type is shown live on every page in-game — there's a dig schedule link in the side panel and at `com_dig_times`. Use it to confirm timing rather than relying on the wiki for exact times if a window is shifted in a patch.

## Artifact Rarity Tiers

From lowest to highest: **Common → Uncommon → Rare → Unique → Special**

Higher tier artifacts are either fused from lower tier components or obtained as rare digs.

### Storage Caps

Each tier has a hard cap on how many you can hold at once. Excess artifacts of a tier at cap are discarded.

| Tier | Cap |
|---|---|
| Common | 255 |
| Uncommon | 125 |
| Rare | 50 |
| Unique | 20 |
| Special | 10 |

The cap is **per-tier**, not per-artifact-type — your total Commons across all Orb types share the 255 ceiling, your total Specials across all Grand types share the 10 ceiling, etc. Plan fusing accordingly: hoarding components past the cap is a loss, so either fuse them up to the next tier or use them before you hit the limit.

## Artifact Effects

### Special (Highest Tier)

| Artifact | Effect | Recipe |
|----------|--------|--------|
| Grand Alimenter | -125,000 to 500,000 Food | Major Afortunado, Minor Afortunado, Minor Estructura, Major Cosecha, Major Alimento |
| Grand Alimento | -20% Food | Major Gordo, Historia, Major Barrera, Major Producto, Regalo |
| Grand Barrera | +50 Kho Shield | Persiana, Major Tierra, Major Barrera, Major Gordo, Regalo |
| Grand Cosecha | +125,000 to 500,000 Food | Major Afortunado, Major Alimento, Minor Estructura, Major Tierra, Major Cosecha |
| Grand Dinero | -10% Credits | Major Cosecha, Major Alimento, Minor Estructura, Minor Requerido, Persiana |
| Grand Estructura | -1,000 Assigned Infrastructure on ALL Systems | Minor Gordo, Minor Estructura, Historia, Minor Afortunado, Major Alimento |
| Grand Gente | -2,500 Population | Major Cosecha, Big Time Capsule, Major Tierra, Small Time Capsule, Major Afortunado |
| Grand Producto | -30% Consumer Goods | Regalo, Major Alimento, Minor Alimento, Regalo, Major Alimento |
| Grand Requerido | -30% Raw Material | Major Gordo, Persiana, Major Tierra, Major Cosecha, Major Barrera |
| Grand Tierra | -25% Ore | Major Alimento, Major Tierra, Major Cosecha, Persiana, Major Gordo |
| Major Gordo | +Land/Planets on one colony (60–100 land per use) — self: **any chosen colony**; enemy: their **outermost border colony**. **Cannot target Homeworlds** (Patch 106). | Big Time Capsule, Major Cosecha, Major Alimento, Major Afortunado, Big Time Capsule |
| Planetary Core | +Planets on a colony (200–2,500, avg ~1,200) | **No fusion recipe (Patch 106)** — obtained via special means only |

### Unique

| Artifact | Effect | Recipe |
|----------|--------|--------|
| Big Time Capsule | +100 Turns | Small Time Capsule, Regalo, Major Producto, Small Time Capsule, Major Barrera |
| Historia | -40 Turns | Minor Suerte, Small Time Capsule, Minor Requerido, Major Suerte, Minor Cosecha |
| Major Afortunado | +100 Luck (Time-Based) | Major Suerte, Minor Requerido, Minor Gente, Minor Alimento, Minor Gente |
| Major Alimento | -12,500 to 50,000 Food | Minor Barrera, Minor Gordo, Minor Barrera, Minor Gordo, Minor Gordo |
| Major Barrera | +20 Kho Shield | Minor Requerido, Minor Gente, Minor Alimento |
| Major Cosecha | +12,500 to 50,000 Food | Minor Gordo, Traicione, Traicione, Minor Gordo, Traicione |
| Major Dinero | -3% Credits | Minor Alimento, Minor Cosecha, Minor Tierra, Amber Dinero, Minor Requerido |
| Major Producto | -1,000,000 to 5,000,000 Consumer Goods | Minor Cosecha, Minor Tierra, Traicione, Minor Gente, Minor Alimento |
| Major Tierra | -1,250 to 5,000 Ore | Minor Cosecha, Minor Tierra, Minor Tierra, Minor Cosecha, Minor Tierra |
| Minor Afortunado | +20 Luck (Time-Based) | Minor Requerido, Major Suerte, Minor Suerte, Minor Gente, Minor Suerte |
| Minor Estructura | -200 Assigned Infrastructure on ALL Systems | Minor Gente, Minor Requerido, Small Time Capsule, Minor Cosecha, Minor Alimento |
| Minor Gordo | +Land/Planets on one colony (20–40 land per use) — self: any chosen colony; enemy: their outermost border colony | Minor Cosecha, Minor Cosecha, Minor Tierra, Minor Alimento, Minor Gente |
| Persiana | +10 Timewarp | Minor Requerido, Small Time Capsule, Minor Gente, Small Time Capsule, Minor Alimento |
| Regalo | +1 to 10 of a Random Artifact | Minor Gordo, Garnet Dinero, Traicione, Minor Alimento, Minor Cosecha |

> Regalos have a 20% chance to fizzle. This can be reduced with Luck artifacts.

### Rare

| Artifact | Effect | Recipe |
|----------|--------|--------|
| Major Suerte | +5 Luck (Turn-Based) | Assimilated Base, Silver Dinero, Bronze Dinero, Gold Dinero, Platinum Dinero |
| Minor Alimento | -250 to 1,000 Food | Opal Dinero, Garnet Dinero, Topaz Dinero, Amber Dinero, Platinum Dinero |
| Minor Barrera | +5 Kho Shield | Cuarto Mapa, Opal Dinero, Cuarto Mapa, Opal Dinero, Silver Dinero |
| Minor Cosecha | +250 to 1,000 Food | Amber Dinero, Garnet Dinero, Topaz Dinero, Opal Dinero, Amethyst Dinero |
| Minor Gente | -150 Population | Garnet Dinero, Platinum Dinero, Platinum Dinero, Gold Dinero, Assimilated Base |
| Minor Requerido | -25,000 to 100,000 Raw Material | Silver Dinero, Organic Base, Gold Dinero, Platinum Dinero, Amber Dinero |
| Minor Suerte | +2 Luck (Turn-Based) | Cuarto Mapa, Organic Base, Silver Dinero, Bronze Dinero, Gold Dinero |
| Minor Tierra | -50 to 200 Ore | Gold Dinero, Silver Dinero, Cuarto Mapa, Silver Dinero, Silver Dinero |
| Small Time Capsule | +10 Turns | Minor Gordo, Minor Barrera, Minor Tierra, Traicione, Minor Cosecha |
| Traicione | -20 Loyalty | Opal Dinero, Amber Dinero, Bronze Dinero, Cuarto Mapa, Amber Dinero |

> Big Time Capsules give 117.6 turns if the recipient is offline when sent.

### Uncommon

| Artifact | Effect | Recipe |
|----------|--------|--------|
| Amber Dinero | -Credits | Yellow Orb, Brown Orb, Purple Orb, Gray Orb, Yellow Orb |
| Amethyst Dinero | -Credits | Energy Pod, Golden Orb, Orange Orb, Green Orb, Brown Orb |
| Assimilated Base | Used for fusing | Dig only — cannot be crafted |
| Bronze Dinero | +Credits | Black Orb, Orange Orb, Green Orb, Blue Orb, Yellow Orb |
| Cuarto Mapa | 25% chance to give 1 random artifact formula | White Orb, Black Orb, Blue Orb, Green Orb, Orange Orb |
| Garnet Dinero | -Credits | Green Orb, Moccasin Orb, Turquoise Orb, Golden Orb, Moccasin Orb |
| Gold Dinero | +Credits | Gray Orb, Pink Orb, Aqua Orb, Turquoise Orb, Plum Orb |
| Opal Dinero | -Credits | Energy Pod, Yellow Orb, Aqua Orb, Blue Orb, Energy Pod |
| Organic Base | Used for fusing | Dig only — cannot be crafted |
| Platinum Dinero | +Credits | Aqua Orb, Plum Orb, Pink Orb, Pink Orb, Aqua Orb |
| Silver Dinero | +Credits | Yellow Orb, White Orb, Gray Orb, Purple Orb, Pink Orb |
| Topaz Dinero | -Credits | Blue Orb, Golden Orb, Orange Orb, Turquoise Orb, Pink Orb |

### Common (Base Dig Rewards)

Common orbs are the raw material of the artifact system. They are used to fuse Uncommon artifacts.

| Artifact | Fuses Into |
|----------|-----------|
| Aqua Orb | Grand Dinero, Grand Gente, Grand Tierra, Grand Tierra |
| Black Orb | Grand Estructura, Grand Alimento, Grand Cosecha, Grand Gente, Grand Tierra |
| Blue Orb | Grand Alimento, Grand Cosecha, Grand Gente, Grand Tierra, Grand Requerido |
| Brown Orb | Grand Alimento, Grand Gente, Grand Tierra, Grand Tierra |
| Energy Pod | Grand Dinero, Grand Alimento, Grand Producto, Grand Barrera, Grand Requerido |
| Golden Orb | Grand Alimento, Grand Alimento, Grand Cosecha, Grand Cosecha |
| Gray Orb | Grand Requerido, Grand Requerido, Grand Barrera, Grand Barrera |
| Green Orb | Grand Cosecha, Grand Gente, Grand Tierra, Grand Requerido, Grand Barrera |
| Moccasin Orb | Major Dinero, Major Dinero, Grand Estructura, Grand Estructura |
| Orange Orb | Grand Gente, Grand Tierra, Grand Requerido, Grand Barrera, Grand Producto |
| Pink Orb | Grand Tierra, Grand Tierra, Grand Requerido, Grand Requerido |
| Plum Orb | Cuarto Mapa, Cuarto Mapa, Bronze Dinero, Bronze Dinero, Bronze Dinero |
| Purple Orb | Grand Requerido, Grand Barrera, Grand Producto, Grand Alimento, Grand Dinero |
| Turquoise Orb | Grand Cosecha, Grand Cosecha, Grand Gente, Grand Gente |
| White Orb | Major Dinero, Grand Estructura, Grand Alimento, Grand Cosecha, Grand Gente |
| Yellow Orb | Grand Tierra, Grand Requerido, Grand Barrera, Grand Producto, Grand Alimento |

## Special Mechanics

### Kho Shield
Blocks both negative **and** positive artifacts. A defensive tool that comes at the cost of also blocking beneficial artifacts sent by allies.

### Luck
Increases the rate of finding artifacts while digging and improves Regalo success rates. Available in both time-based and turn-based variants. Has no effect on combat.

### Timewarp
Applied via Persiana. Gives the target a small chance to "miss" when they attempt an attack — the attack fails and they must refresh the page to try again. The tactical use is applying Timewarp to your enemy's intended targets, creating a brief window to hit the enemy while they are stuck on a failed attack. Split-second timing, but enough to matter in active PvP.

### Gordos & Planetary Fracture (Patch 106)

Patch 106 ("Planetary Fracture") reworked how Minor and Major Gordos behave, after empires used them to artificially inflate land.

> **Use Minors, not Majors, for land.** Pound for pound, Minor Gordos are far more land-efficient. A Minor self-applies for 20–40 land; a Major only 60–100 — but building a Major burns a large fusion tree (~11 Minors' worth of components). Those ~11 Minors applied directly (~220–440 land) grow far more than the single Major. Only fuse up to a Major when you specifically need one large application rather than many small ones — or when a colony has hit the Minor land cap (see below) and only a Major can still grow it.

**Targeting:**

- **On yourself:** a Gordo can be applied to **any chosen colony** in your colony list (previously it affected all systems at once).
- **On another empire:** a Gordo only affects their **outermost border colony** (the topmost in their list).
- **Major Gordo can no longer be used on Homeworld colonies** (Minor Gordo still can).

**Land threshold → planet conversion:** A Gordo now adds **land up to a threshold**; once that threshold is reached, further Gordo value adds **planets** to the colony instead. As a cluster accumulates planets it climbs cluster levels:

- A smaller cluster that gains planets past its level's planet ceiling **converts up to the next cluster size** (e.g. a **C1 gordoed past the 25-planet threshold becomes a C2**).
- **Maximum-level clusters (C3, C.4, C.5)** have a hard threshold at **roughly twice the cluster's base planet count** (so ~250 planets for a 125-planet C3, etc.).

**Land caps (live-tested):** A colony's land can't be gordoed forever — past a cap, the artifact refuses to fire with the message **"Colony too large to gordo!"**. Two things set the cap: the **Gordo tier** (Majors cap higher than Minors, making them the only way to grow past the Minor cutoff) and the colony's **planet count** — a colony still at 1 planet caps far lower than the same type grown into a multi-planet cluster, so a single-planet cap is *not* the type's overall max. Publicly confirmed values so far (**?** = not yet publicly confirmed):

| U-class | 1-planet cap (Minor) | 1-planet cap (Major) | Max cap (Minor) | Max cap (Major) |
|---------|----------------------|----------------------|-----------------|-----------------|
| **U.Eden** | ? | ? | ? | ? |
| **U.Fertile** | ? | ? | 40,000 | 67,625 |
| **U.Large** | ? | 21,495 | ? | ? |
| **U.Rich** | ? | ? | ? | ? |
| **U.Spazial** | ? | 21,495 | ? | ? |

A maxed Fertile holds **50 planets**. For standard clusters, a **maxed C3 caps at 375,000 land**; the lower cluster tiers are not yet publicly confirmed.

**New colony types introduced by the fracture system:**

- **Cluster Base** — a regular single-planet colony that has been gordoed (the pre-C1 gordoed state).
- **U-Class Colony Clusters** — gordoed U-class colonies, now available for **all** U-class types once gordoed past the threshold.

Empires already over the threshold when the patch landed were contacted by the Galactic Council regarding their colony decisions.

> See [Planet Types](planets.md#industry-modifiers) for the per-type modifiers (including the new Industry column added in the same patch).
