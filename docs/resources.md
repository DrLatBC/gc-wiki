# Resources

Galactic Conquest has 10 resources split into two categories: goods used in the economy and minerals used for ship construction.

## Goods

| Resource | Description |
|----------|-------------|
| **Food** | The central commodity of the player economy. Tax players cannot function without a steady supply — population starves without it. Produced by Agriculture. |
| **Ore** | Used to construct buildings on colonies. Produced by Mining as a bonus. |
| **Raw Material** | Byproduct of food production. Primary input for Industry to produce Consumer Goods. |
| **Consumer Goods (CGs)** | Produced by Industry and Commercial infrastructure. Purchased by Tax players to boost income — desirable but not required for survival. |

## Ship Minerals

Used exclusively for building ships. They have no other purpose.

| Resource | 
|----------|
| Terran Metal |
| Red Crystal |
| White Crystal |
| Rutile |
| Composite |
| Strafez Organism |

## The Market

The market is player-driven. Sellers post resources at a price they choose within dev-set min/max bounds (per-resource). Buyers purchase the cheapest posted listings first.

If no players are selling a resource, buyers are out of luck — with one exception. A **black market** provides an NPC source for **Ore**, **Raw Material**, and the **6 ship minerals** at quantity-scaling prices. It does **not** sell Food or Consumer Goods. On the live (real-time) server, Raw Material is unavailable on the black market — only Ore and the 6 minerals are sold there. The black market is buy-only; there is no NPC buyer of last resort. If demand dries up, sellers are stuck.

Black-market unit prices scale with how much of the resource you already own (so bulk buying gets progressively more expensive):

- **Minerals:** `1,250 × 1.05^(owned ÷ 1,000,000)`, capped at 1,000,000/unit
- **Ore:** `25,000 × 1.1^(owned ÷ 10,000)`, capped at 10,000,000/unit

## Resource Flow

```
Agriculture → Food + Raw Material
     ↓                   ↓
  Market          Industry → Consumer Goods → Market
     ↓                                           ↓
Tax players ←——————————————————————————— Tax players (optional boost)
     ↓
Population growth → Tax income
```

Mining produces ship minerals sold directly on the market. Commercial infrastructure produces CGs (consuming 2 Raw Materials per building per turn) and a flat empire-wide credit stream that has no resource cost.

## Resource Caps

Hard ceilings on stored resources. Production beyond these caps is discarded.

| Resource | Cap |
|----------|-----|
| Credits (positive) | 5,000,000,000,000 (5 trillion) |
| Credits (debt floor) | -200,999,999,999 |
| Raw Materials | 25,000,000,000 (25 billion) |
| Food | 25,000,000,000 (25 billion) |
| Goods | 25,000,000,000 (25 billion) |
| Ore | 2,000,000,000 (2 billion) |
| Each ship mineral (1–6) | 2,000,000,000 (2 billion) |

Going into negative credits triggers compounding 1.5%-per-turn debt interest — see [Formulas](formulas.md#debt-interest).

## Goods → Credits (Population Consumption)

Each colony's population **demands** `(pop ÷ 10) × race_good` goods per turn, drawn from your empire-wide good stockpile. The goods your population **consumes** are what generate income: each consumed good converts to **5.5 credits**. Any **surplus** goods beyond population demand are **kept in your stockpile** (up to the 25-billion cap), not auto-sold.

In other words: you are paid 5.5 credits for every good your population eats — you are *not* paid for leftovers, and leftovers are retained, not dumped. This is the primary mechanism by which produced goods become income — see the full per-colony order in [Formulas](formulas.md#calculation-order).
