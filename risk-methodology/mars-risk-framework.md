---
description: >-
  This document describes a proposed risk framework for Mars, which serves two
  main purposes
---

# Mars Risk Framework

1. To qualitatively assess the riskiness of protocols and assets to be added to the platform (including the Red Bank and Mars credit accounts).
2. To determine the risk parameters for assets to be added to Mars. Initially, this framework will cover two types of assets: single asset tokens and LP tokens.

The proposed framework enables different assets and LP tokens to be objectively compared and assessed by standardizing how risk is measured and parameters are determined. This framework will be explored in detail in the following sections. The first section will explore the qualitative assessment process to whitelist protocols and assets to be used in the Red Bank or through Mars credit accounts. The second section will describe the quantitative process to assess the riskiness of single assets. Finally, in the last section the methodology to determine the risk parameters for single assets and LP tokens is covered.

The Mars Risk Framework is intended to be a non-binding resource to guide deliberation by Mars governance. The ultimate decision of whether to whitelist a protocol or asset rests solely in the hands of the Martian Council.

### 1. DeFi Protocol and Assets Whitelisting Process

The following criteria are suggested as an initial filter for whitelisting protocols and single assets within Mars. Assets or protocols that don’t meet the minimum requirements described below should not be incorporated into the protocol.

#### Integrating a certain protocol

**Technical risk:**

<table><thead><tr><th valign="top">Metric</th><th valign="top">Minimum Requirements</th><th valign="top">Ideal Requirements</th></tr></thead><tbody><tr><td valign="top">Time Since Launch</td><td valign="top">-</td><td valign="top">> 1 Year</td></tr><tr><td valign="top">Custom Public Audit</td><td valign="top">At least 1 custom audit made public</td><td valign="top">Several custom audits performed by high quality auditors made public</td></tr><tr><td valign="top">Recent Audit</td><td valign="top"></td><td valign="top">Audit within the last 12 months or no code changes since last audit</td></tr><tr><td valign="top">Quality of Smart Contracts</td><td valign="top">Well documented. Extensive test coverage.</td><td valign="top">Written with best practices. Very well documented. Extensive test coverage. Easy to read. Simple logic. Battle tested code.</td></tr><tr><td valign="top">No Ciritical Vulnerabilities</td><td valign="top">No vulnerabilities have been exploited</td><td valign="top">No vulnerabilities have been exploited</td></tr><tr><td valign="top">Bug Bounty Program</td><td valign="top">Bug Bounty program</td><td valign="top">Bug Bounty program (min. 0.25% of TVL)</td></tr></tbody></table>

**Centralization risk:**

<table><thead><tr><th valign="top">Metric</th><th valign="top">Minimum Requirements</th><th valign="top">Ideal Requirements</th></tr></thead><tbody><tr><td valign="top">Owner* Decentralization<br><br><sub><em>* Owner account call privileged functions</em></sub></td><td valign="top">Multisig with majority of the signers being reputable, accountable, not otherwise affiliated with one another and incentive-aligned with relevant stakeholders</td><td valign="top">No owner - Controlled by DAO with safe processes in place</td></tr><tr><td valign="top">Admin** Decentralization<br><br><sub><em>** Admin account can upgrade contracts</em></sub></td><td valign="top">Multisig with majority of the signers being reputable, accountable, not otherwise affiliated with one another and incentive-aligned with relevant stakeholders</td><td valign="top">No admin keys - Controlled by DAO with safe processes in place</td></tr><tr><td valign="top">Other permissioned addresses</td><td valign="top">Multisig with majority of the signers being reputable, accountable, not otherwise affiliated with one another and incentive-aligned with relevant stakeholders</td><td valign="top">No admin keys - Controlled by DAO with safe processes in place</td></tr></tbody></table>

_Note: assets and protocols controlled by unaccountable, affiliated, and/or centralized entities should not be accepted into Mars._

#### Enabling assets as collateral and/or for other interactions

**Oracle risk:**

<table><thead><tr><th valign="top">Metric</th><th valign="top">Minimum Requirements</th><th valign="top">Ideal Requirements</th></tr></thead><tbody><tr><td valign="top">Oracle Risk</td><td valign="top"><p>Robust oracle, understood as:<br></p><ul><li>Costly to manipulate: the oracle should be costly to manipulate given the potential profit of the attack.</li><li>Accurate: the price reported by the oracle should be as close as possible to the real spot price of the asset.</li><li>Decentralized: the methodology for determining the price is well understood and transparent. No single entity has control over the process and/or the outcome</li></ul></td><td valign="top"></td></tr></tbody></table>

_Note: given the oracle's critical importance for the platform, assets without robust oracles should not be accepted into Mars._

**Technical risk:**

<table><thead><tr><th valign="top">Metric</th><th valign="top">Minimum Requirements</th><th valign="top">Ideal Requirements</th></tr></thead><tbody><tr><td valign="top">Time Since Launch</td><td valign="top">-</td><td valign="top">> 1 Year</td></tr><tr><td valign="top">Custom Public Audit</td><td valign="top">At least 1 custom audit made public</td><td valign="top">Several custom audits performed by high quality auditors made public</td></tr><tr><td valign="top">Recent Audit</td><td valign="top"></td><td valign="top">Audit within the last 12 months or no code changes since last audit</td></tr><tr><td valign="top">Quality of Smart Contracts</td><td valign="top">Well documented. Extensive test coverage.</td><td valign="top">Written with best practices. Very well documented. Extensive test coverage. Easy to read. Simple logic. Battle tested code.</td></tr><tr><td valign="top">No Ciritical Vulnerabilities</td><td valign="top">No vulnerabilities have been exploited</td><td valign="top">No vulnerabilities have been exploited</td></tr><tr><td valign="top">Bug Bounty Program</td><td valign="top">Bug Bounty program</td><td valign="top">Bug Bounty program (min. 0.25% of TVL)</td></tr></tbody></table>

**Centralization risk:**

<table><thead><tr><th valign="top">Metric</th><th valign="top">Minimum Requirements</th><th valign="top">Ideal Requirements</th></tr></thead><tbody><tr><td valign="top">Owner* Decentralization<br><br><sub><em>* Owner account call privileged functions</em></sub></td><td valign="top">Multisig with majority of the signers being reputable, accountable, not otherwise affiliated with one another and incentive-aligned with relevant stakeholders</td><td valign="top">No owner - Controlled by DAO with safe processes in place</td></tr><tr><td valign="top">Admin** Decentralization<br><br><sub><em>** Admin account can upgrade contracts</em></sub></td><td valign="top">Multisig with majority of the signers being reputable, accountable, not otherwise affiliated with one another and incentive-aligned with relevant stakeholders</td><td valign="top">No admin keys - Controlled by DAO with safe processes in place</td></tr><tr><td valign="top">Other permissioned addresses</td><td valign="top">Multisig with majority of the signers being reputable, accountable, not otherwise affiliated with one another and incentive-aligned with relevant stakeholders</td><td valign="top">No admin keys - Controlled by DAO with safe processes in place</td></tr></tbody></table>

_Note: for bridged assets, both the bridge itself and the token should pass the minimum requirements. For LP tokens, both the DEX and the token should pass the minimum requirements. This applies to the technical and centralization risk requirements._

### 2. Single Assets Scoring Methodology

For whitelisted assets, market and liquidity risks are assessed to calculate an asset’s score, which is then used as part of the process to determine the asset’s risk parameters. In this section, we will explore how that score is calculated and how it is used within the overall risk parameters methodology.

#### Risk Metrics

The scoring methodology evaluates assets in two broad categories: market risk and liquidity risk. Market risk is related to the volatility of the asset and extreme changes in its price, whereas liquidity risk is related to the ability to liquidate the asset. Specifically, assets are scored using the following metrics:

- **Daily 95% Conditional Value-at-Risk (CVaR, 365-days):** an average of the “extreme” losses in the tail of the distribution of asset returns beyond the value at risk (VaR) cutoff point defined over the past 365 days.
- **Maximum intraday drawdown (90-day):** maximum price change (from high to low) in a trading day over the last 90 days.
- **Median 24hr volume (365-day, logarithm):** median 24hr volume over the last 365 days.
- **Median 24hr market capitalization (7-day average, 90-days, logarithm):** median 7-day average 24hr market capitalization over the last 90 days.
- **Average high-low percent quoted spread (30-day):** daily bid-ask spread proxy (see Appendix A for details).
- **Amihud’s illiquidity measure (90-day, logarithm):** daily cost-per-dollar-volume proxy (see Appendix A for details).

The following subsections describe the methodology used to score tokens in each of these metrics.

#### Input Data

The input data for the scoring methodology corresponds to the daily historical data of asset prices, trading volume, and market capitalization over the past year (365 calendar days) from the reference date. In addition, daily high-low-open-close data is used over the past 30 calendar days and +-2% depth as of the reference date. All data is sourced from Coingecko. Coingecko was used for practical reasons and this should not imply an affiliation or endorsement of the brand.

The selection of the assets for the scoring methodology is as follows:

1. The list of available assets is sourced from Coingecko.
2. The top 1,000 assets by market capitalization are selected.
3. All assets that do not have a trading history of at least 90 calendar days prior to the reference date are removed from the set.

#### Scoring Methodology

The scoring methodology consists of three steps:

1. A score is determined for each risk metric separately.
2. Aggregation is performed by using simple averaging of scores.
3. Lastly, the final asset’s score is used to define the asset’s quality category.

Let’s explore each step below.

**Step 1. Defining a score for an individual metric**

Firstly, all metrics for each asset are transformed into a score from 0 to 100 to standardize the scoring methodology and compare different assets more efficiently. For this transformation (from metric to 0-100 score), a linear scaling method (min-max normalization) is used. The normalized values represent individual metric scores assigned to each asset. The detailed procedure is the following:

Let $p_{ij}, i \in [M], j \in [N]$ denote the initial value of the $j$-th metric of the $i$-th asset, $b_{ij}$ is a normalized value of $p_{ij}$; $p_{min,j}, p_{max,j}$ are the minimum and the maximum values of the $j$-th metric over all assets.

For positive metrics (i.e., those that increase with improving asset quality), the normalization is performed as follows:

$$
b_{ij} = \frac{p_{ij} - p_{\text{min},j}}{p_{\text{max},j} - p_{\text{min},j}} \times 100, \quad i \in [M],\ j \in [N]
$$

whereas if a metric increase has a negative effect on the final rating the formula becomes

$$
b_{ij} = \frac{p_{\text{max},j} - p_{ij}}{p_{\text{max},j} - p_{\text{min},j}} \times 100, \quad i \in [M],\ j \in [N]
$$

Using the above formulas each ith asset is described by a vector of normalized parameters

$$
\mathbf{b}_{i} = (b_{i1}, \ldots, b_{iN})^T, \quad i \in [M]
$$

As a result of this step, the values of all metrics are brought to the same scale in such a way that all metrics positively impact the asset quality (the closer the score to 100 the better the asset quality in regards to that metric).

**Step 2. Aggregation of metrics**

Once scores for all metrics are calculated, they are averaged to get the asset’s final score.

_Example:_

| Asset | Daily 95% CVaR | Maximum Intraday Drawdown | Median 24hr volume | Median 24hr market capitalization | Mean high-low percentage quoted spread | Amihud's illiquidity measure |
| :---: | :------------: | :-----------------------: | :----------------: | :-------------------------------: | :------------------------------------: | :--------------------------: |
|   X   |       90       |            82             |         47         |                60                 |                   70                   |              80              |

Let asset X have the following scores:

Then the total score is:

$$
\text{Final Score} = \frac{90 + 82 + 47 + 60 + 70 + 80}{6} = 71.5
$$

**Step 3. Binning**

The range of final score values is divided into sub-ranges to provide five quality categories: “very good”; “good”; “medium”; “bad”; “very bad”. The following binning procedure is applied to define the category intervals.

The upper expectation (ceiling) for the final score is set to be 80, and the lower expectation (floor) is the 10th percentile of the distribution of score values. Assets with a final score above the ceiling are assigned a category “very good.” while those with a final score below the floor are assigned a category “very bad.”

The intervals between ceiling and floor are defined based on the equal width binning procedure. The width of each interval is:

$$
\Delta = \frac{\text{ceiling} - \text{floor}}{k}
$$

where $k$ equals $N-2$, $N –$ is the number of categories. The corresponding interval boundaries are:

$$
\text{floor} + \Delta,\quad \text{floor} + 2\Delta,\quad \ldots,\quad \text{floor} + (k - 1)\Delta
$$

Each asset is assigned a quality category depending on the interval in which the value of the final score falls, according to the following table:

| Quality Category |   Score    |
| :--------------: | :--------: |
|    Very good     | \[80; 100] |
|       Good       | \[68; 80]  |
|      Medium      | \[56; 68]  |
|       Bad        | \[43, 56]  |
|     Very bad     |  \[0; 43]  |

_Table 1. Bins for quality categories_

These categories are used to define the maximum allowable LTVs within each category and risk horizons for the LTV calculation methodology (see Section 3).

The procedure for determining the final score is similar for new assets (not included in the initial data sample). Firstly, all metrics are calculated based on historical data and normalized using the minimum and maximum values previously defined from the sample (see the table 2 below). If the metric value exceeds the maximum or below the minimum, it is assumed to be equal to the maximum or minimum value, respectively. Finally, the obtained scores are averaged to get the total score.

<table><thead><tr><th valign="top">Metric</th><th align="center" valign="top">Min value</th><th align="center" valign="top">Max value</th></tr></thead><tbody><tr><td valign="top">Daily CvaR (95%), %</td><td align="center" valign="top">-0.3</td><td align="center" valign="top">24.4</td></tr><tr><td valign="top">Median intraday drawdown</td><td align="center" valign="top">0.3</td><td align="center" valign="top">47.9</td></tr><tr><td valign="top">Median 7-day average market cap, log $</td><td align="center" valign="top">10,3</td><td align="center" valign="top">26.7</td></tr><tr><td valign="top">Mean high-low percentage quoted spread, %</td><td align="center" valign="top">0.1</td><td align="center" valign="top">9.2</td></tr><tr><td valign="top">Amihud's illuquidity, log</td><td align="center" valign="top">0.1</td><td align="center" valign="top">31.3</td></tr></tbody></table>

_Table 2. Min and max values used for metrics normalization_

### 3. Risk Parameters

This section describes the approach to determine the risk parameters for whitelisted assets and LP tokens, namely Liquidation LTV, Maximum LTV, and Margin of Safety.

#### 3.1 Definitions

- **Liquidation LTV** is the LTV at which a position is defined as undercollateralized and the user becomes liquidatable.
- **Maximum LTV** (≤ Liquidation LTV) is the maximum LTV allowed when the user is opening or adjusting a position.
- **Margin of Safety** is the difference between the Liquidation LTV and Max. LTV. It’s a safety cushion to avoid users becoming liquidatable immediately after opening a position at the maximum allowed LTV.

The derivation of Liquidation LTV is described in Section 3.2. The approach to define Margin of Safety and corresponding Maximum LTV is provided in Section 3.3. Lastly, in Section 3.4 the methodology to determine these risk parameters for LP tokens is explored.

#### 3.2 Liquidation LTV for Single Asset Tokens

Liquidation LTV is defined for each token as follows:

$$
\text{Liq.\,LTV} = \min\left(\text{LTV}_{\text{estimated}}, \text{LTV}_{\text{cap}}\right)
$$

where

$$
LTVestimated=1-Haircut
$$

$$
\text{Haircut} = \text{Market Risk Component} + \text{Liquidity Risk Component}
$$

$$
\text{Market Risk Component} \geq 0, \quad \text{Liquidity Risk Component} \geq 0
$$

The haircut intends to capture the percentage potential loss of value of a given asset after it becomes liquidatable due to the following factors:

- Market risk component – risk related to possible extreme price movements.
- Liquidity risk component – the cost of liquidating a position following a liquidation event due to the impact of the liquidation on the market price.

A detailed description of the calculation approach for both components is given in the following subsections. The greater the asset's market and/or liquidity risk, the higher the corresponding haircut and the lower the LTV.

The $LTV_{cap}$ serves to limit the LTV obtained from the historical data to ensure conservatism and depends on the token’s quality as defined in Section 2 (see Table 3 below).

**Market Risk Component**

The market risk component is an LTV adjustment defined such that the expected likelihood\* of the price of the asset dropping more than the market risk component is 1%. Hence the market risk component is defined as the 99% conditional value-at-risk with a given risk horizon (average of the “extreme” returns in the left tail of the asset returns distribution, beyond the value at risk cutoff point):

$$
\text{Market Risk Component} = -\text{CVaR}(99\%, \text{Risk Horizon})
$$

where CVaR(99%, Risk Horizon) ≤ 0 is defined by using the historical-simulation approach, which implies that the probability distribution and corresponding tail-risk are estimated empirically from the observed price movements (percentage asset returns) over the past 365 days from the reference date.

_It’s important to highlight that this methodology only provides an estimate of extreme future price trajectories of a given asset. This estimate is based on past price performance and, as such, it should be understood as a backward-looking, fallible (though valuable) tool for predicting future prices._

The risk horizon represents the longest period required for a position to be liquidated. It is assumed to depend on the asset category (see table 3 below) and varies from 1 to 5 days. The riskier the asset, the longer the period used to calculate relative price movements and quantify corresponding tail-risk (CVaR). Usually, liquidations within DeFi happen within 1 day. However, the minimum 1-day horizon is used to ensure conservatism as the historical simulation approach is backward-looking and may not cover all potential movements of the asset price in the future.

Note: estimating the distribution quantile can be inaccurate for assets with short histories. To take this into account, we use quantiles for those pairs where we have price histories over the past 200-365 days, while for others (90-200 days history), we use the extreme move approach - maximum observed percentage returns over the available historical period.

**Liquidity Risk Component**

The liquidity risk adjustment is defined per asset using the -2% dollar depth aggregated over different exchanges as of the reference date. It is a cost-per-dollar-volume liquidity risk measure that is interpreted as capital in USD required to move the price by 2% down from the last traded price. The list of exchanges considered includes Uniswap, Osmosis, and top-10 exchanges according to the Coingecko ranking.

The liquidity risk component is calculated for each token as follows:

$$
\text{Liquidity Risk Component} = \text{Swap Size } \$ \times \left( \frac{0.02}{\text{Depth}_{-2\%}} \right)
$$

Here the multiplier\

$$
\frac{0.02}{\text{Depth}_{-2\%}}
$$

shows how much % the price will move down subject to $1 volume.

Depth refers to the ability of the market to absorb the sale or exit of a position. A liquidator who liquidates a position of an ordinary user is not likely to impact the asset price. Selling a large block of assets though, can cause the price to fall when the asset is sold. Hence, the Swap Size is set to depend on the asset's deposit cap and is defined conservatively, assuming a medium-size transaction amount that can have a notable impact on the asset price as 1% of the deposit cap.

The risk horizon and $LTV_{cap}$ for each token’s category are provided in the table below:

_Table 3. Risk horizons and LTV caps per asset’s quality category_

#### 3.3 Maximum LTV and Margin of Safety for Single Asset Tokens

The Liquidation LTV is defined based on the $CVaR(99\%, \text{horizon})$ with the horizon determined by the token’s quality category. The safety margin is defined as the absolute difference between the CVaR calculated at the defined horizon plus 1 day and the $CVaR(99\%, \text{horizon})$:

Thus, the margin of safety is defined by the relative price drop incurred in one additional day in relation to the horizon used to determine the Liquidation LTV.

The higher the price volatility of the token, the more the price can fall with an increase in the risk horizon by 1 day, and therefore the higher the safety margin and the lower the corresponding Maximum LTV will be.

The following caps are applied to the margin of safety derived from the historical data depending on the token’s quality category:

_Table 4. Margin of Safety caps per token’s quality category_

The minimum margin of safety is set to be 0.005.

The Maximum LTV is defined based on an absolute adjustment applied to the Liquidation LTV as follows:

$$
\text{Max. LTV} = \text{Liq. LTV} - \text{Margin of Safety}
$$

#### 3.4 Risk Parameters for LP tokens

The Liquidation LTV of LP tokens is calculated as the average of the Liquidation LTVs of the individual assets that compose the LP token, adjusted for IL risks:

$$
\text{Liq. LTV}_{\text{LP token}} = \text{Avg}(\text{Liq. LTV}_1, \text{Liq. LTV}_2) \times \text{IL Risk Adjustment}
$$

where $Liq.LTV_{1}, Liq.LTV_{2}$ are the Liquidation LTVs of the assets that compose the LP token (assuming a 50/50 LP token). The IL Risk Adjustment $\,\leq\,1$ is intended to capture the additional impermanent loss risks associated with holding an LP token (vs. a 50/50 portfolio of the individual assets).

The IL risk is defined as follows:

$$
\text{IL Risk Adjustment} = 1 + \text{Expected IL}
$$

where Expected $IL \leq 0$.

Assuming a 50%/50% LP token and constant product AMM, IL is calculated as follows:

$$
\text{IL} = 2 \cdot \frac{\sqrt{R}}{R + 1} + 1
$$

where $R = \frac{P_{1}}{P_{0}} = \frac{1 + r^x_{1}}{1 + r^y_{1}}$, $r^x_{1}$ and $r^y_{1}$ are simple assets’ returns calculated over the unit of time and $P_i$ is the pool price. _Note that the above IL formula excludes trading fees and other rewards LP token holders may accrue. This is intentional and is done to calculate a worse-case IL, which ultimately generates a more conservative LTV for the LP token._

From the above formula, historical ILs for each pool are calculated by using the 10-day overlapping asset returns over the past 365 days.

Then the expected IL is estimated by using the historical simulation value-at-risk approach. Based on the empirical distribution of ILs, value-at-risk measures the loss value that will not be exceeded with a probability of 95% over a 10-day risk horizon:

$$
\text{IL Risk Adjustment} = 1 + \text{VaR}_{95\%,\,10\text{-day}}(\text{IL distribution})
$$

The risk horizon represents the longest period needed for liquidation (the longest period over which the protocol can be exposed to the position, i.e., liquidating the LP token).

The risk horizon is set to 10-days to ensure conservatism.

_Note: Estimating the distribution quantile can be inaccurate for assets with short histories. To take this into account, we use quantiles for those pairs where we have price history over the past 200-365 days, while for others (90-200 days history), we use the extreme move approach - maximum observed ILs over the available historical period._

The applied IL risk adjustment allows to capture the size of the loss (risk exposure) within the chosen risk horizon and the associated probability level (the likelihood of a loss of a given magnitude (with a 5% chance of exceeding it)). Using a historical simulation method to estimate value-at-risk captures any empirical dependencies (including non-linear ones) between the two assets in the pool.

The Margin of Safety and the Maximum LTV for LP token are defined as follows:

$$
\text{Margin of Safety}_{\text{LP token}} = \text{Avg}(\text{Margin of Safety}_1, \text{Margin of Safety}_2)
$$

$$
\text{Max. LTV}_{\text{LP token}} = \text{Liq. LTV}_{\text{LP token}} - \text{Margin of Safety}_{\text{LP token}}
$$

where $Margin\ of\ Safety_{1},\ Margin\ of\ Safety_{2}$ are the Margins of Safety of the assets that compose the LP token.

### 4. Model Usage, Monitoring and Update

Approaches used in this framework to define risk parameters are primarily data-driven; hence the obtained risk parameters are expected to change in response to varying market conditions. Therefore, obtained LTVs can be revised regularly (i.e. once every six months or urgently in case of severe market stress) to avoid stale risk parameters.

When updating the model, the historical data period can also be revised to ensure that the sample covers at least one period of acute stress (e.g., May 2022).

Additionally, the sanity of the final outputs of the model should be checked by the community such that final parameter adjustments are made when considered necessary.

### 5. Disclaimers

Please Note: The proposed risk framework is not intended as financial advice and should not be relied upon; rather, it is being made available for educational purposes as a starting point for each person’s own independent review and analysis of risks. The risk framework could fail to account for certain risks or could fail to adequately weigh the risks that it does account for. Use at your own risk. No representation, warranty, guaranty, indemnity or assumption of risk is being provided hereby. This article is subject to and qualified by the Mars Disclaimers/Disclosures.

### Appendix A. Description of risk metrics

#### Amihud’s illiquidity measure

The metric is calculated as follows:

$$
\text{illiq} = \frac{1}{n} \sum_{i=1}^{n} \frac{|R_i|}{V_i}
$$

where $R_{i}$ is the daily asset return at day $i$ and $V_{i}$ is the daily dollar trading volume at $i$.

In cases where significant price changes with small trading volume exist, this ratio increases, which means that the illiquidity of the stock increases. Everything else being equal, a higher trading volume will lead to a lower Amihud illiquidity measure.

This metric is considered a proxy for market depth liquidity measure.

#### High-low percentage quoted spread

The metric is calculated as follows:

$$
\text{Spread} = \frac{1}{2} \cdot \frac{P_{\text{high}} - P_{\text{low}}}{P_{\text{mid}}}
$$

where $$P_{\text{high}}$ is the highest daily price, $P_{\text{low}}$$ is the lowest daily price, and $P_{\text{mid}}$ is the mid-price. The full spread $P_{\text{high}} - P_{\text{low}}$ represents the cost of buying and selling the asset today. As we are only interested in the cost of selling, the cost of liquidity is only half of the spread.

This metric represents a proxy for the bid-ask spread, widely used as a market width measure.
