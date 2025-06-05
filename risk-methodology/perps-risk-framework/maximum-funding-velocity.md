---
description: >-
  This section explains how the maximum funding velocity parameter is
  calibrated.
---

# Maximum Funding Velocity

### Parameter Calibration Rationale

Under a critical skew level (near the maximum), and given an extreme price change of the underlying asset over a certain horizon (i.e., a strong upward or downward price trend in the direction of the skew), the funding rate velocity must ensure that the accumulated funding payment exceeds or equals the profit from the price change (i.e., the market risk delta is hedged by the funding payment). This incentivizes users to close their positions and return the market to a neutral state, even without intervention from other participants.

Given the use of soft maxSkew restrictions, the theoretical maximum skew is equivalent to maxOI. Therefore, maxOI is used in maxFundingVelocityCalibration instead of maxSkew.

Throughout the considered period, the skew measured in tokens is assumed to remain constant. This represents a highly conservative assumption, positing the absence of arbitrageurs who might respond to increased funding rates.

### Key Parameters

* $$h = 24h$$ is a risk horizon
* $$y$$ is the extreme price change within the risk horizon that is highly probable, determined by the underlying asset's quality category:

| Quality Category | y   |
| ---------------- | --- |
| Very Good        | 5%  |
| Good             | 10% |
| Medium           | 15% |
| Bad              | 40% |
| Very Bad         | 40% |

Estimated figures in the table represent the median historical 95% CVaR for price returns within each specified quality category.

* $$k$$ is the proportional skew level ($$k = K_{t}/K_{\max}$$). Given a low skew, the protocol's risk exposure from unrealized PnL is minimal, which justifies setting the critical threshold at 95%.
* $$\tau = 1/24$$ is the frequency of the funding rate update, $$T = 24$$.

### Calculation

$$
maxFundingVelocity = \text{ceil}\left(\frac{y}{w \cdot \tau^{2} \cdot (S_{1} + y \cdot \tau \cdot S_{2})}, 0\right)
$$

where

$$
S_{1} = \sum_{t=1}^{T} t = T \cdot \frac{T + 1}{2}
$$

$$
S_{2} = \sum_{t=1}^{T} t^{2} = \frac{T \cdot (T + 1) \cdot (2T + 1)}{6}
$$

$$
w = \frac{k \cdot K_{\max}}{skewScale}
$$

$$K_{\max}$$ is the maximum token-denominated skew determined under the oracle price at the moment of calibration.

The formal proof for the above formula is provided in the Appendix.

### Input Data

| Data Item                   | Description                                              | Source    | Period/Frequency                    | Processing                                                   |
| --------------------------- | -------------------------------------------------------- | --------- | ----------------------------------- | ------------------------------------------------------------ |
| $$p$$                       | Price of the underlying asset over the historical period | Coingecko | Frequency: 1h Period: past 365 days | Simple percentage return is calculated over the risk horizon |
| $$K_{\$,max} = maxOI_{\$}$$ | Maximum dollar OI per market                             | RF        | -                                   | -                                                            |
| $$skewScale$$               | Skew scale parameter                                     | RF        | -                                   | -                                                            |

### Proof of MaxFundingVelocity Formula

## Appendix B. Proof for the maxFundingVelocity formula

Results below are derived for long positions, for short positions the calculation is similar.

PnL from the price change at the end of the horizon is the following:

$$PnL_{T} = (p_{T} - p_{0}) \cdot q = q \cdot ((1 + y) \cdot p_{0} - p_{0}) = y \cdot p_{0} \cdot q$$

where $$y$$ is the percentage price return over the horizon.

Funding accrued per each period between the skew-modification events is calculated as follows:

$$f_{t} = p_{t} \cdot q \cdot r_{t} \cdot \tau$$

where $$\tau = \frac{h}{T}$$ is the time step measured in days.

Accumulated funding at the end of the horizon:

$$F_{T} = \sum f_{t} = \tau \cdot q \cdot \sum p_{t} \cdot r_{t} = \tau \cdot q \cdot p_{0} \cdot \sum (1 + y_{t}) \cdot r_{t}$$

Assuming a linear price growth, we have:

$$y_{t} = y \cdot t \cdot \tau$$

Then

$$F_{T} = \tau \cdot q \cdot p_{0} \cdot \sum (1 + y \cdot t \cdot \tau) \cdot r_{t}$$

The funding rate dynamics is the following:

$$r_{t} = r_{t-1} + c \cdot \tau \cdot \frac{K_{t}}{SkewScale}$$

where $$c$$ is the short notation for $$maxFundingVelocity$$.

Let $$r_{0} = 0$$, $$K_{t} = k \cdot K_{max}$$, $$w = k \cdot \frac{K_{max}}{SkewScale}$$. At any given moment, the funding rate is defined as follows:

$$r_{1} = c \cdot \tau \cdot w$$

$$r_{2} = 2 \cdot c \cdot \tau \cdot w$$

$$\vdots$$

$$r_{t} = t \cdot c \cdot \tau \cdot w$$

$$\vdots$$

By integrating the funding rate's behavior into the funding accumulation equation, the following is derived:

$$F_{T} = \tau^{2} \cdot q \cdot p_{0} \cdot c \cdot w \cdot \sum (1 + y \cdot t \cdot \tau) \cdot t$$

The sum $\sum (1 + y \cdot t \cdot \tau) \cdot t$ can be represented as follows:

$$\sum (1 + y \cdot t \cdot \tau) \cdot t = \sum t + y \cdot \tau \sum t^{2} = S_{1} + y \cdot \tau \cdot S_{2}$$

where

$$S_{1} = \sum t = T \cdot \frac{T + 1}{2}$$

$$S_{2} = \sum t^{2} = \frac{T \cdot (T + 1) \cdot (2T + 1)}{6}$$

The cumulative funding is then expressed as:

$$F_{T} = \tau^{2} \cdot q \cdot p_{0} \cdot c \cdot w \cdot (S_{1} + y \cdot \tau \cdot S_{2})$$

By the end of the defined period, the total accumulated funding must be at least equal to the profit or loss that has not yet been realized due to price fluctuations:

$$F_{T} \geq PnL_{T}$$

Let's find the minimum $$maxFundingVelocity$$ at which this inequality satisfies:

$$F_{T} = PnL_{T}$$

This gives the final equation for maxFundingVelocity:

$$\tau^{2} \cdot q \cdot p_{0} \cdot c \cdot w \cdot (S_{1} + y \cdot \tau \cdot S_{2}) = y \cdot p_{0} \cdot q$$

$$\tau^{2} \cdot c \cdot w \cdot (S_{1} + y \cdot \tau \cdot S_{2}) = y$$

The final outcome is achieved by solving the equation for $$c$$.

**This completes the proof.**
