---
description: >-
  The funding rate mechanism is a core component of perpetual futures markets
  that ensures long-term market stability by balancing supply and demand between
  long and short positions.
---

# Funding Rate Mechanism

## Velocity-Based Funding Rate Mechanism

The funding rate mechanism serves as a critical balancing tool designed to maintain market equilibrium by incentivizing traders to take positions that reduce market skew. Unlike traditional static funding models, this system employs a dynamic velocity-based approach that adjusts funding rates based on the persistence and magnitude of directional imbalances in open interest.

### How It Works

The funding rate evolves continuously according to a velocity model where the rate of change is proportional to the current market skew. The daily funding rate is calculated using the formula:

$$
r_t = r_{t-1} + maxFundingVelocity \times pSkew_t \times \frac{timeDelta_t}{secondsInDay}
$$

where the proportional skew $$pSkew_t = skew_t / skewScale$$ represents the current market imbalance relative to the skew scale parameter, clapmed between -1 and 1. The maxFundingVelocity parameter determines how quickly funding rates respond to persistent skew conditions.

The funding rate is subject to a maximum cap of 96% per day (4% per hour) to prevent extreme scenarios while maintaining effectiveness.

### Key Properties

This mechanism exhibits three important characteristics that promote market stability:

* **The funding rate can be either positive or negative.** When positive, long position holders pay funding to short position holders. When negative, short position holders pay funding to long position holders. Importantly, the relationship between skew direction and funding rate is not instantaneous - a positive skew (more longs than shorts) does not immediately result in a positive funding rate, and vice versa. This is because the model adjusts funding rate velocity rather than the rate itself. For example, if the market initially had negative skew and negative funding rates, then shifts to positive skew, the funding rate velocity becomes positive but the actual funding rate may remain negative until sufficient time passes for it to reverse direction.
* **Linear Growth with Persistent Skew**: When market imbalance remains constant over time, the funding rate increases linearly, creating mounting pressure for rebalancing trades.
* **Quadratic Response to Growing Imbalances**: If the skew itself grows linearly, the funding rate accelerates quadratically, providing exponentially stronger incentives to restore balance.
* **Proportional Velocity**: The greater the relative skew compared to its maximum threshold, the faster the funding rate adjusts, ensuring rapid response to significant imbalances.

### Funding Index Calculation

The system maintains a cumulative funding sequence $$F = {F_0, F_1, \ldots, F_t}$$ that tracks the accumulated (USDC-denominated) funding per unit of the underlying asset. This index is updated after each skew-modification event using the recurrent formula:

$$
F_t=F_{t-1}-u_t
$$

where the funding entrance $$u_t$$ represents the funding accrual for the period and is calculated as:

$$
u_t = \frac{p_{or,t}}{p_{or,t}^{USDC}} \times \frac{r_t + r_{t-1}}{2} \times \frac{timeDelta}{secondsInDay}
$$

This formula uses the average of the current and previous funding rates, multiplied by the time elapsed since the last event, and adjusted for the relative price between the underlying asset and USDC. The funding index effectively captures the cumulative funding obligation per unit of asset over time.

### Funding Accrual for Positions

Individual positions accrue funding based on their entry point in the funding sequence and their position size. When a trader opens or modifies a position, the system records the current funding index $$F_{t_0}$$ as their reference point. The unrealized funding payment for any position is then calculated as:

$$
f_t = q \times (F_t - F_{t_0})
$$

### Examples of Funding Accrual

Consider an ETH perpetual market where the funding rate has been positive (favoring shorts) due to long skew:

_Long Position Example_: Alice opens a 10 ETH long position when $$F_{t_0} = 1.5$$. After 24 hours, the funding index has decreased to $$F_t = 1.48$$ due to positive funding rates. Alice's funding payment is: $$f_t = 10 \times (1.48 - 1.5) = -0.2$$ USDC, meaning she owes 0.2 USDC in funding fees to short holders.

_Short Position Example_: Bob opens a 5 ETH short position ($$q = -5$$) at the same time as Alice when $$F_{t_0} = 1.5$$. After 24 hours with $$F_t = 1.48$$, Bob's funding payment is: $$f_t = -5 \times (1.48 - 1.5) = 0.1$$ USDC, meaning he receives 0.1 USDC in funding payments from long holders.

