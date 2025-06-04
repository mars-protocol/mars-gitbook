---
description: >-
  This section explains how the SkewScale parameter is calibrated in the price
  impact model and the funding rate model.
---

# SkewScale

## SkewScale in the Price Impact Model

### Parameter Calibration Rationale

The parameter calibration aims to align price slippage in perp trading with that of underlying asset spot trading on external markets under balanced market conditions (zero skew). This ensures appealing trading execution when the market exhibits no directional bias.

Depending on the prevailing skew and the direction of the order, the actual slippage may be less than or exceed the slippage on the global market.

### Calculation

$$
SkewScale=Depth_ {s\%} \div 2⋅s%SkewScale = \frac{Depth_{s\%}}{2 \cdot s\%}SkewScale=2⋅s%Depths%​​
$$

where

$$
Depth_{s\%​}=min(Depth_{+s\%}​,Depth_{−s\%​})
$$

$$Depth_{\pm s\%}$$ is the token-denominated global market depth. The final skewScale is rounded to a specific power of 10 depending on number' magnitude.

Formal proof is provided in the Appendix.

### Input Data

| Data Item              | Description                                                                           | Source    | Period/Frequency | Processing          |
| ---------------------- | ------------------------------------------------------------------------------------- | --------- | ---------------- | ------------------- |
| $$Depth_{\pm 2\%, $}$$ | $$\pm 2\%$$ aggregated global market depth across leading exchanges and trading pairs | Coingecko | 90-day median    | Transform to tokens |

### Key Assumptions

* Linear price impact model is used.

## SkewScale in the Funding Rate Model

The same SkewScale parameter is utilized in the funding rate model through a mathematical transformation that establishes the relationship between funding velocity and market skew.

In the funding rate model, the rate is designed to be proportional to the skew relative to the maximum allowable skew:

$$
r_{t} = r_{t-1} + velocity \cdot \frac{skew}{maxSkew} \cdot \Delta t
$$

We can rewrite this equation as follows:

$$
r_{t} = r_{t-1} + velocity \cdot \frac{skewScale}{maxSkew} \cdot \frac{skew}{skewScale} \cdot \Delta t
$$

Let's define the following notation:

$$
maxFundingVelocity := velocity \cdot \frac{skewScale}{maxSkew}​
$$

Then we have the following model (which is used in production):

$$
r_{t} = r_{t-1} + maxFundingVelocity \cdot \frac{skew}{skewScale} \cdot \Delta t
$$

Therefore, the same skewScale parameter is used in the funding rate model, given that maxFundingVelocity is determined using the aforementioned transformation.
