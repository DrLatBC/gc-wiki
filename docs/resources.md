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

The market is player-driven. Sellers post resources at a price they choose within dev-set min/max bounds. A secondary safeguard prevents posting prices too far above the current market rate to prevent artificial price spikes.

If no players are selling a resource, buyers are out of luck — with one exception. A **black market** provides an NPC source for Food, CGs, and minerals at above-market prices. The black market is buy-only; there is no NPC buyer of last resort. If demand dries up, sellers are stuck.

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

Mining produces ship minerals sold directly on the market. Commercial infrastructure produces CGs and credits directly without relying on Raw Material in any significant quantity.
