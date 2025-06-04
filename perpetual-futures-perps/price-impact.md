---
description: >-
  Price impact mechanism simulates an order book by adding a slippage percentage
  to each order that is proportional to the skew and position size.
---

# Price Impact

## Market Impact Mechanism

The market impact model adjusts execution prices based on the current market skew and the size of the incoming order. In this approach traders pay premiums when expanding market imbalance and receive discounts when helping to balance it. The system ensures that larger directional positions face progressively higher costs, naturally limiting extreme skew accumulation.

### How It Works

When a trader places an order, the oracle price is adjusted based on both the current market skew and the impact of their specific trade. The execution price is calculated using the formula:

$$
p_{ex} = p_{or} \times \left( 1 + \frac{InitialPremium + FinalPremium}{2} \right)
$$

where the premiums are determined by the market skew before and after the trade:

$$
InitialPremium = \frac{InitialSkew}{SkewScale}
$$

$$
FinalPremium = \frac{FinalSkew}{SkewScale}
$$

The initial skew represents the current market imbalance, while the final skew shows the market state after the trade is executed. For position opening, $$FinalSkew = InitialSkew + q$$, and for position closing, $$FinalSkew = InitialSkew - q$$, where $$q$$ is the position size.

The parameter skewSclae is calibtarted to align price slippage in perp trading with that of underlying asset spot trading on external markets under balanced market conditions (zero skew). This ensures appealing trading execution when the market exhibits no directional bias.

### Price Impact Examples

Consider an ETH perpetual market with a SkewScale of 1,000,000 ETH and current oracle price of $2,000:

_Expanding Skew Example_: The market currently has a +50 ETH skew (equivalent to $100,000 at current prices). Alice wants to open a $10,000 long position (5 ETH), further expanding the skew.

* Initial skew: 50 ETH
* Final skew: $$50 + 5 = 55$$ ETH
* Initial premium: $$50 \div 1,000,000 = 0.005%$$
* Final premium: $$55 \div 1,000,000 = 0.0055%$$
* Average premium: $$(0.005 \% + 0.0055 \%) \div 2 = 0.00525 \%$$
* Execution price: $$ $2,000 \times (1 + 0.0000525) = $2,000.105 $$

_Reducing Skew Example_: Bob wants to open a $10,000 short position (5 ETH), helping to balance the market.

* Initial skew: 50 ETH
* Final skew: $$50 - 5 = 45$$ ETH
* Initial premium: $$50 \div 1,000,000 = 0.005%$$
* Final premium: $$45 \div 1,000,000 = 0.0045%$$
* Average premium: $$(0.005 \% + 0.0045 \%) \div 2 = 0.00475 \%$$
* Execution price: $$ $2,000 \times (1 + 0.0000475) = $2,000.095 $$

In this example, Alice pays a small premium of $0.105 per ETH for expanding the skew, while Bob pays a slightly smaller premium of $0.095 per ETH for helping to balance the market. The impact is minimal for small positions relative to the SkewScale but demonstrates how the mechanism rewards market-balancing behavior.

### Market Impact Role

The market impact model provides several key benefits to the ecosystem:

1. **Skew Management**: By making skew expansion more expensive and skew reduction cheaper, the system naturally encourages balanced markets.
2. **LP Protection**: Liquidity providers face reduced directional risk as extreme skew positions become economically prohibitive.
3. **Fair Pricing**: Traders who help balance the market are rewarded with better execution prices, while those who increase risk pay appropriate premiums.
4. **Manipulation Resistance**: Large coordinated attempts to create extreme skew face increasing costs, making price manipulation attacks economically unfeasible.

This market impact mechanism works in conjunction with the funding rate system to create multiple layers of incentives that promote market stability and protect all participants from excessive directional exposure.

