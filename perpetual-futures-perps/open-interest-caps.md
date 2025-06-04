---
description: >-
  Open Interest and Skew caps are risk management mechanisms that set maximum
  limits on total position sizes and market imbalances to protect liquidity
  providers from excessive directional exposure.
---

# Open Interest Caps

Open Interest and Skew caps are essential risk management tools that limit the vault's exposure to directional market movements and prevent excessive concentration in any single direction. These caps protect liquidity providers from taking on too much counterparty risk while ensuring the protocol maintains balanced and sustainable market conditions. By implementing both absolute position limits and relative skew constraints, the system creates multiple layers of protection against market manipulation and extreme exposure scenarios.

### Open Interest Caps

Open Interest (OI) caps set maximum limits on the total notional value of positions that can be held on each side of the market. These caps are denominated in USD to provide consistent risk limits regardless of the underlying asset's price fluctuations.

Each market enforces separate caps for long and short positions. The total dollar value of all long positions cannot exceed the maximum OI limit, and the same applies to short positions. These constraints are only checked when traders attempt to increase their position size, meaning existing positions can be closed regardless of the current OI levels.

### Skew Caps

Skew caps limit the maximum net imbalance between long and short positions, preventing the vault from taking on excessive directional exposure. The skew represents the difference between total long and short open interest and can be either positive (more longs) or negative (more shorts).

The protocol enforces a maximum absolute skew limit, measured in USD terms. This means the net difference between long and short positions cannot exceed a predetermined threshold in either direction.

The skew cap operates as a "soft" limit with the following rules:

* **Skew Expansion**: When the current skew is at maximum, traders cannot open position that expand the skew.
* **Skew Reduction**: Positions that help balance the market are always permitted.
* **Position Closure**: Users and liquidators can always close positions regardless of skew constraints.

### Exceeding OI Limits

In certain situations, the current open interest may exceed the maximum OI limits due to:

1. **Price Appreciation**: As the underlying asset price increases, the dollar value of existing positions grows, potentially pushing total OI above the limit.
2. **Governance Changes**: When governance reduces the MaxOI risk parameter, existing positions may suddenly exceed the new lower limit.

When this occurs, the protocol activates an auto-deleveraging mechanism to reduce vault risk exposure. The system automatically closes the most profitable positions first, continuing until the open interest returns to acceptable levels.&#x20;

### Position Modification Constraints

When traders modify their positions, the system validates that the resulting market state remains within all caps. Constraints only apply when traders are increasing their position size in a given direction.&#x20;

### Risk Management Benefit

The combined OI and skew caps provide comprehensive risk management:

1. **Absolute Exposure Limits**: OI caps prevent the vault from taking on unlimited positions in any direction
2. **Directional Risk Control**: Skew caps limit net exposure to price movements
3. **Market Stability**: Caps prevent extreme imbalances that could destabilize the market
4. **LP Protection**: Liquidity providers face bounded counterparty risk
5. **Manipulation Resistance**: Large coordinated attempts to create extreme positions are blocked

These caps work alongside the funding rate and market impact mechanisms to create a multi-layered risk management system that maintains market balance while protecting all participants from excessive exposure.
