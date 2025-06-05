---
description: >-
  This section details how maximum open interest and maximum skew limits are
  determined through multiple risk assessment approaches to protect the vault
  from the counterparty risk.
---

# Open Interest Caps

The maximum OI is determined using an ensemble of approaches, and the minimum result is taken:

1. **Extreme Price Change Approach:** Potential losses over a 6-hour horizon, assuming maximum skew (skew=maxOI) and extreme price movement in the direction of the skew, should not exceed 30% of the vault's total value.
2. **Manipulation Scenario Approach:** In the event of oracle price manipulation with a specific amount of capital, the maximum profit an attacker could extract (if possible) should not exceed a predetermined portion of the vault.
3. **Expert Caps:** Expert-defined maximum OI caps are also applied, such as a percentage of the total market capitalization and/or total market depth.

## Extreme Price Change Approach

### Parameter Calibration Rationale

The primary risk addressed when evaluating maximum open interest (and maximum net open interest) is the vault's counterparty risk. This refers to the net risk assumed by the vault as the counterparty to all trades. To mitigate this risk, we conservatively limit open interest through maximum skew (MaxSkew) and maximum open interest (MaxOI).

The rationale behind calibrating MaxSkew and MaxOI is to ensure that even if a market reaches maximum skew and the price moves sharply in the direction of the skew, the potential loss to the vault remains below a predefined threshold with high probability.

**Example.** With a $250k vault TVL and a $10M maximum net OI for a specific market at maximum skew, a 3% price change in the skew direction could result in a $300k unrealized profit/loss ($10M \* 3%). This scenario highlights a significant bankruptcy risk for the vault when the maximum OI is substantially larger than the vault TVL.

Maximum Open Interest (MaxOI) calibration is crucial due to our soft skew cap. This mechanism limits skew only when opening or increasing positions; closing or decreasing orders are always permitted. Consequently, skew could theoretically exceed the set limits, potentially reaching the MaxOI in a single direction under extreme conditions. We calibrate MaxOI assuming a worst-case scenario where the protocol acts as the sole counterparty for all positions. Once MaxOI is established, the Maximum Skew (MaxSkew) is defined as a fixed percentage (30%) of MaxOI.

Note that in addition to maximum caps, several mechanisms help maintain skew within acceptable boundaries. These include velocity-based funding rates and price market impact. Specifically, when skew reaches and remains at its maximum, or continues to increase, the funding rate rises rapidly, reducing trader profitability. Conversely, both the funding rate and price incentives for reducing skew encourage arbitrageurs to take opposing positions. Typically, this inherent arbitrage activity should regulate the skew, keeping it below the maximum threshold. However, maximum caps are in place for extraordinary scenarios.

### Key Parameters

The following parameters are used in the methodology described below:

* **Gamma** $$\gamma = 30%$$: This represents the maximum potential percentage exposure for the vault. It is the upper limit for potential losses relative to the net TVL that should not be exceeded with a probability of (1 - α). A lower gamma indicates lower exposure, but reduced capital efficiency for the vault.
* **Significance Level** $$\alpha = 1%$$: This is the significance level used for determining the extreme price change.
* **Risk Horizon** $$h = 12h$$: This is the period over which extreme price changes are calibrated. It also represents the time horizon during which the protocol could be exposed to the maximum OI level and can be interpreted as the autodeleverage horizon.
* **Extreme Price Change** $$R$$: This is the extreme percentage price change of the underlying asset that is expected to occur over the risk horizon ($$h$$) with a high confidence level (1 - $$\alpha$$).

MaxOI and MaxSkew are calculated for each market independently. This approach assumes a 0% chance that at least two markets will simultaneously experience maximum skew and extreme price changes in the direction of the skew.

The benefit of this approach is that adding a new market does not affect the risk parameters of existing markets. However, the drawback is that it disregards the risk of simultaneous extreme conditions across multiple markets. This risk increases with the number of listed markets. To mitigate this, other parameters such as the risk horizon and gamma should be chosen conservatively. A more sophisticated model could be considered in the future to account for the probabilities of multiple markets reaching maximum skew concurrently and the correlations between their price changes.

### Notations

* $$V$$ - vault TVL
* $$UPnL$$ - Unrealized PnL for all open positions for a certain market, can be either positive or negative
* $$D$$ - is the vault total Debt
* $$NV = V - D$$ - vault current net TVL
* $$r_{t+h}$$ is the percentage price change of the underlying asset over the period $$[t, t+h]$$
* $$maxOI$$ - maximum dollar one-sided Open Interest, i.e., maximum dollar value of all open positions in one of the directions
* $$K$$ is the current token-denominated skew for the market, can be either positive (if the market is long-skewed) or negative (if the market is short-skewed)
* $$K_{\$}$$ is the current USD-denominated market skew
* $$K_{\max}$$ is the current token-denominated maximum skew for the market

### Potential Loss for a Single Market

Assuming the open interest (OI) in token amounts remains constant over the period $$[t, t+h]$$ (meaning no positions are opened or closed), the unrealized profit and loss (UPnL) for a single market at time $$t+h$$ is:$$UPnLt+h=∑qj(pt+h−pj)=t+h} = \sum q_{j}(p_{t+h} - p_{j}) = p_{t+h} \sum q_{j} - \sum q_{j} p_{j} = p_{t+h} K_{t} - \sum q_{j} p_{j}$$

$$
UPnL_{t+h} = \sum q_{j}(p_{t+h} - p_{j}) = p_{t+h} \sum q_{j} - \sum q_{j} p_{j} = p_{t+h} K_{t} - \sum q_{j} p_{j}
$$

where:

* $$q_{j}$$ is the $$j$$th position size (positive for longs and negative for shorts)
* $$p_{j}$$ is the entering price for the $$j$$th position
* $$K_{t} = \sum q_{j}$$ is the token-denominated market skew at time $$t$$

Let's assume that all N traders entered their positions simultaneously at time $$t$$ using the average opening price across all positions as $$p_{0,t} = \frac{1}{N} \sum p_{j}$$. Then the total unrealized PnL is:$$UPnLt+h=Kt⋅(pt+h−p0)=Kt⋅p0,t⋅rt+h=Kt,$⋅rt+hUPnL_{t+h} = K_{t} \cdot (p_{t+h} - p_{0}) = K_{t} \cdot p_{0,t} \cdot r_{t+h} = K_{t,\$} \cdot r_{t+h}UPnLt+h​=Kt​⋅(pt+h​−p0​)=Kt​⋅p0,t​⋅rt+h​=Kt,$​⋅rt+h​$$

$$UPnLt+h=Kt⋅(pt+h−p0)=Kt⋅p0,t⋅rt+h=Kt,$$

$$⋅rt+hUPnL_{t+h} = K_{t} \cdot (p_{t+h} - p_{0}) = K_{t}$$,&#x20;

$$p_{0,t} \cdot r_{t+h} = K_{t,$} \cdot r_{t+h}UPnLt+h​=Kt​⋅(pt+h​−p0​)=Kt​⋅p0,t​⋅rt+h​=Kt,$$

$$​⋅rt+h​$$

$$
UPnL_{t+h} = K_{t} \cdot (p_{t+h} - p_{0}) = K_{t} \cdot p_{0,t} \cdot r_{t+h} = K_{t,\$} \cdot r_{t+h}
$$

where $$r_{t+h}$$ is the asset price return over the horizon $$h$$.

This UPnL represents the vault potential loss coming from the price change for a period $$[t, t+h]$$ under the static skew assumption.

### MaxOI Calculation

We consider each market to be isolated from other markets and ignore the joint probability of extreme scenarios for at least two markets. Basically, we assume that there is only one perp market.

The maximum open interest (MaxOI) is set to ensure that potential extreme losses for the vault remain below a specific percentage ($\gamma$) of the vault's net Total Value Locked (TVL) with a certain probability. This determination is based on the following conditions:

* The skew is at its maximum value, $K\_{max,$}$
* Extreme price movements occur in the direction of the skew

Let assume the worst-case scenario when all open positions are on the one side of the market and the magnitude of the imbalance and one-sided open interest are the same:

$$
K_{max,\$} = maxOI
$$

In this scenario, the protocol is effectively the sole counterparty to all positions.

We require the following probabilistic equation to hold:

$$
P\{UPnL_{t+h} \geq \gamma \cdot NV_{t}\} = P\{r_{t+h} \cdot maxOI \geq \gamma \cdot NV_{t}\} = \alpha
$$

Solving this equation yields the upper bound for the maximum OI:

$$
maxOI = \frac{\gamma \cdot NV}{R}
$$

where $$R = F_{r}^{-1}(\alpha, h)$$ is the extreme quantile of the asset return distribution.

The parameter $$R$$ is determined using the CVaR risk metric over the chosen horizon:

for longs: $$R_{L} = CVaR_{r}(1\%, h)$$

for shorts: $$R_{S} = CVaR_{r}(99\%, h)$$

To calculate the CVaR metric for each market, we employ a historical simulation method using the previous year's price data. For simplicity, we assume symmetrical price fluctuations and conservatively apply the same magnitude of change in both upward and downward directions:

$$
R = \max(|R_{L}|, |R_{S}|)
$$

### Key Assumptions

* Skew is at maximum for the particular market
* Skew is zero for all other markets or their prices are constant during the risk horizon
* The market price changes significantly in the skew direction for a particular market
* The price market impact is ignored for simplicity
* Closing fees are excluded for conservatism
* Compounding funding payments accumulated over the risk horizon are excluded. Note that in accordance with the $$maxFundingVelocity$$ calibration procedure, when the skew exceeds the critical level, the funding rate velocity reaches its maximum. Consequently, maintaining a position in the skew direction becomes unprofitable over time due to high accumulated funding payments. Therefore, ignoring funding is a conservative approach
* The positions set is static. There are no arbitrageurs, and traders do not close positions to reduce the skew. No changes occur in the market (no positions are opened, closed, or liquidated); thus, the token-denominated skew remains constant during the horizon $$h$$ ($$K = const$$). This represents the worst-case scenario
* The vault TVL is static ($$V = const$$), meaning no liquidity inflows or outflows occur during the horizon $$h$$

### Input Data

| Data Item | Description                                     | Source    | Period/Frequency          | Processing |
| --------- | ----------------------------------------------- | --------- | ------------------------- | ---------- |
| $$NV$$    | The vault dollar TVL net of the debt            | SC        | -                         | -          |
| $$p$$     | Historical oracle price of the underlying asset | Coingecko | 1h over the past 365 days | -          |

### Numerical Example

* Vault TVL $$V$$ = $500k
* Vault Debt $$D$$ = $100k
* Net Vault TVL $$NV = V - D = \$400k$$
* Extreme price change $$R$$ = 40%
* Gamma $$\gamma$$ = 30%

Deriving from the MaxOI formula:

$$
maxOI = \frac{\gamma \cdot (V - D)}{R} = \frac{0.3 \cdot \$400k}{0.4} = \$300k
$$

The potential loss associated with the MaxOI is:

$$
UPnL = R \cdot maxOI = 0.4 \cdot \$300k = \$120k
$$

This represents 30% of the vault's total net TVL:

$$
\frac{UPnL}{V - D} = \frac{\$120k}{\$400k} = 0.3 = 30\%
$$

Based on the historical returns of the underlying asset, there is a 1% probability that the maximum potential loss will surpass 30% of the vault's value within a given risk horizon.

## Manipulation Scenario Approach

### Parameter Calibration Rationale

To mitigate market price manipulation risk, the maximum obtainable profit for an attacker within a specific market must be capped at a defined portion of the vault.

### Price Manipulation Factor

Let a user manipulate the market price: making transactions of large volume $$C$$ the price is shifted by $$\beta\%$$ (e.g. for the JELLY market the price was pumped by $$\beta$$=\~400% using 63% of total market capitalization which was around $15M).

A potential price pump/dump $$\beta$$ depends on two factors:

* **The manipulation capital:** Higher capital used for manipulation can lead to a greater price pump or dump. We conservatively assume a large manipulation capital (as seen in the Mango attack, $20M).
* **The market liquidity (depth):** More liquid markets require greater capital to shift the price. A precise approach would consider the depth from the specific feeds used in the Slinky price oracle for each market. This could involve using the minimum depth across all feeds, the feed with the maximum voting power, or a vote-weighted depth. However, implementing this requires knowledge of the feeds used for each market and the validators' power distribution, making it a potential future enhancement to this methodology.

Based on a simplified method utilizing $$\pm s%$$ global market depth data from leading exchanges and pairs and a linear market impact model, the price manipulation factor can be determined as follows:

$$
\beta = C \cdot \frac{2\%}{\min(Depth_{+s\%,\$}, Depth_{-s\%,\$})}
$$

### Manipulation Scenario

**Position Setup**:

* Attacker opens nearly balanced long and short positions (A and B)
* Net exposure E(A-B) is minimal, appearing neutral
* One position is well-collateralized, the other is minimally collateralized
* With multiple short-long positions, a user can theoretically open positions up to the maximum OI on Mars because the skew will be kept near zero

**Attack Execution**:

* Attacker triggers price jump on one of the exchanges (with thin liquidity)
* A well-collateralized position makes substantial profit
* Under-collateralized position gets liquidated, with losses exceeding its collateral (potentially a bad debt if not liquidated on time)
* The vault absorbs the uncovered losses

Considering a scenario where an attacker establishes a position with a dollar value equal to the maximum open interest (maxOI) and subsequently manipulates the price upwards, the total OI in dollar terms would surpass the maxOI limit. This condition would activate the auto-deleverage mechanism, which would close the most profitable positions. However, for the sake of conservatism, this scenario is not explicitly factored into the methodology for risk parameters estimation.

### MaxOI Calculation

Allow a user to open a position (or a set of positions) with the maximum possible size, equal to the maximum long or short open interest. Since price manipulation strategies are typically short-term, funding payments do not have sufficient time to accumulate and are therefore excluded from consideration. The maximum profit obtainable from price manipulation in either the long or short direction is calculated as follows:

$$
MaxProfit = MaxOI \cdot \beta
$$

The profit should be capped at a specific percentage of the vault's TVL (for instance, 30% or less).

$$
MaxOI \cdot \beta \leq \gamma \cdot NV
$$

The formula above yields the maximum permissible open interest for each market.

$$
MaxOI = \frac{\gamma \cdot NV}{\beta}
$$

where

$$
β = C \cdot \frac{s\%}{\min(Depth_{s\%,\$}, Depth_{-s\%,\$})}​
$$

### Key Assumptions

* A linear price impact model is used
* Manipulation capital is fixed and doesn't depend on the market capitalization and Slinky feed

### Key Parameters

* $$C = \$20M$$ - manipulation capital
* $$\gamma = 30\%$$ - the vault maximum percentage potential exposure

### Input Data

| Data Item              | Description                                                                   | Source    | Period/Frequency | Processing |
| ---------------------- | ----------------------------------------------------------------------------- | --------- | ---------------- | ---------- |
| $$Depth_{\pm 2\%,\$}$$ | $$\pm 2\%$$ Aggregated global market depth across leading exchanges and pairs | Coingecko | 90-day median    | -          |
| $$NV$$                 | The vault dollar TVL net of debt                                              | SC        | -                | -          |

### Numerical Example

Consider a JELLY market:

* Market Cap = $20M
* Depth (5%) = $200K
* Manipulation capital=$16M (63% of market cap)

$$
\beta = C \cdot \frac{5\%}{Depth_{\pm 5\%,\$}} = \$16M \cdot \frac{0.05}{\$0.2M} = \$16M \cdot \frac{0.05}{\$200K} = 4 = 400\%
$$

The maximum open interest permitted is:

$$
MaxOI = \frac{\gamma \cdot V}{\beta} = \frac{0.3 \cdot \$500K}{4} = \frac{\$150K}{4} = \$37.5k
$$

## Expert Caps

The final model's MaxOI is subject to the following expert-defined upper limits:

| Quality Category | Multiplier to Global Depth |
| ---------------- | -------------------------- |
| Very Good        | 5                          |
| Good             | 5                          |
| Medium           | 3                          |
| Bad              | 3                          |
| Very Bad         | 3                          |

The final cap is determined as the minimum between the caps derived using Approach 1 and Approach 2 capped with the expert-based limits.

The MaxSkew is capped at 30% of MaxOI. Final parameters are rounded to a specific power of 10 depending on number' magnitude.
