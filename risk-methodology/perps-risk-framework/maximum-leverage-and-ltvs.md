---
description: >-
  This section details how maximum leverage and LTVs are calculated using
  extreme-loss methodology to ensure adequate margin coverage against potential
  losses.
---

# Maximum Leverage & LTVs

Parameter Calibration Rationale&#x20;

Initial margin should adequately cover potential extreme losses for a perp position within a defined risk horizon (liquidation horizon). This provides a suitable buffer against significant potential price fluctuations between the liquidation and bankruptcy levels in the probabilistic sense ensuring coverage in most historical scenarios.

### Calculation

To set initial margin requirements and maximum leverage for each market we use the well-known extreme-loss approach widely used in traditional finance. The fundamental principle of this approach is:

$$
\% InitialMargin \geq \% ExtremePotentialLosses
$$

The extreme potential loss in the position value is primarily represented by the unrealized price PnL on the leveraged perp position, which is calculated as follows:

$$
UPnL = q \cdot (p - p_{0}) = q \cdot p_{0} \cdot r
$$

where $$q$$ is the position size (positive for longs and negative for shorts), $$p_{0}$$ is the entry price of the underlying asset, $$p = (1 + r) \cdot p_{0}$$ is the market price at the current time, and $$r$$ is the percentage price change over the risk horizon $$h$$.

**Note.** Here we do not account for other potential risk factors like funding fees or the price impact, though these could influence unrealized PnL. The conservative 12-hour window is intended to capture significant price fluctuations, which should also encompass the effects of volatility in other risk factors.

To determine potential extreme losses from unfavorable price movements, the CVaR risk metric is used with a risk horizon $$h$$. The horizon represents the period during which a position should be liquidated. Even if the position isn't immediately liquidated when the margin reaches the liquidation level, a buffer remains. This buffer ensures that extreme price changes during this period are unlikely to result in bankruptcy. We conservatively set the risk horizon to 12 hours to account for potential chain halts that could interrupt liquidations. Note that liquidations typically occur much faster (especially for USDC-margined accounts).

The extreme potential price movements are determined as follows:

for longs: $$R_{L} = CVaR_{r}(1\%, h)$$

for shorts: $$R_{S} = CVaR_{r}(99\%, h)$$

Assuming equal leverage for long and short positions, the maximum is taken for a conservative approach:

$$
R = \max(|R_{L}|, |R_{S}|)
$$

We calculate the CVaR metric for each market using a historical simulation approach based on 1 year of historical data of 12-hour simple overlapping price returns.

The % initial margin in then determined as follows:

$$
\% InitialMargin = R
$$

Maintenance margin is calculated similarly, but using less conservative CVaR levels (5% and 95%):

$$
\% MaintenanceMargin = R_{m}
$$

### Max Leverage

Maximum Leverage is calculated as the reciprocal of the initial margin:

$$
MaxLeverageModel = \frac{1}{\% InitialMargin} = \frac{1}{1 - MaxLTV}
$$

### Max Leverage Caps

For each asset, we first apply our main [Mars Risk Framework](https://github.com/mars-protocol/mips/blob/main/Mars-Risk-Framework.md) to determine its quality category depending on the volatility and liquidity. The following maximum leverage caps are then applied based on the asset quality:

| Quality Category | MaxLeverageCap |
| ---------------- | -------------- |
| Very Good        | 10             |
| Good             | 7              |
| Medium           | 5              |
| Bad              | 3              |

The final maximum leverage is then determined as follows:

$$
MaxL = \min(MaxLeverageModel, MaxLeverageCap)
$$

The risk parameters for a single perp position used in the Health Factor (HF) calculation are determined as follows:

### Max LTV

$$
MaxLTV = \text{round}((1 - \frac{1}{MaxL}) \cdot 100, 0)
$$

### Liquidation LTV

$$
LiqLTV = MaxLTV + SM
$$

where $$SM$$ is a margin of safety determned as follows:

$$
modelSM = \text{round}((InitialMargin - MaintenanceMargin) \cdot 100, 0)
$$

$$
SM = \text{clamp}(modelSM, SM_{\max}, SM_{\min})
$$

### Input Data

| Data Item | Description                                     | Source    | Period/Frequency          | Processing |
| --------- | ----------------------------------------------- | --------- | ------------------------- | ---------- |
| $$p$$     | Historical oracle price of the underlying asset | Coingecko | 1h over the past 365 days | -          |

### Key Parameters

* Risk horizon: $$h = 12h$$
* Confidence level: for initial margin $$\alpha = 1%$$, for maintenance margin $$\alpha = 3%$$
* Safety Margin Bounds: $$SM_{\min} = 2$$, $$SM_{\max} = 5$$

### Key Assumptions

* Funding rates and price impact are ignored.
* The 12h risk horizon is assumed.

### Special Cases

For brand-new assets and assets with limited data history (less than 30 days), the maximum leverage is set to the maximum leverage cap for the "bad" quality category:

$$MaxL = 3$$

The following risk parameters are finally used:

$$MaxLTV = 66%$$

$$LiqLTV = 70%$$
