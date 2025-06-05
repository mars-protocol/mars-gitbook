---
description: >-
  A simplified framework for rapidly estimating deposit caps in money markets
  using liquidation modeling and on-chain liquidity analysis.
---

# Deposit Caps Risk Framework

This methodology provides a streamlined approach to estimate deposit caps for money markets between the main RF runs \[[Deposit Cap Methodology](https://forum.marsprotocol.io/t/deposit-caps-methodology-v2/1083)]. Due to the time-intensive process required by the full framework, this simplified version enables rapid cap evaluation and monitoring at interim points.

### Notations

* $$\beta%$$ is the minimum liquidation bonus
* $$L$$ is the $$\beta%$$ on-chain depth (available liquidity with slippage $$\beta$$)
* $$u_{opt}$$ is the optimal utilization threshold (80% is used for all assets for simplicity)
* $$x%$$ is the liquidated portion of the debt
* $$d$$ are the liquidated funds
* $$Q$$ is the total on-chain liquidity
* $$T$$ is the recovery time for DEX liquidity to get restored after massive liquidation

### Model Deposit Cap

Consider an arbitrary liquidation of size $$d$$. Suppose it takes $$T$$ minutes for the DEX liquidity $$L$$ ($$\beta%$$ depth) to get restored.

In this case, a liquidation will be composed of $$n = \frac{d}{L}$$ iterations, where each iteration will take $$T$$ minutes, and will execute $$1/n$$-th of the liquidation. In total $$N = n \cdot T$$ time units will elapse before the liquidation is fully executed.

Hence, the liquidation period can be estimated as follows:

$$
N_L = n \cdot T = \frac{d}{L} \cdot T
$$

Let $$N_L$$ is a known liquidation period. If the debt is not liquidated over this period, it goes bankrupt. To estimate Loan-to-Value (LTV) risk parameters, we assume a minimum one-day liquidation period. In 99% of cases, even extreme price changes within this period should not result in bankruptcy. Therefore, the deposit cap can be set at an amount that can be liquidated within this timeframe ($$N_L = 24h$$).

From this equation, we can find the maximum amount that can be liquidated within a duration of $$N_L$$ assuming a periodic recovery occurs every $$T$$ hours:

$$
d = \frac{N_L}{T} \cdot L
$$

Estimation of liquidatable amount $$d$$:

$$
BorrowedFunds = u_{opt} \cdot DepositCap
$$

If $$x%$$ of all borrowed funds are liquidated, the corresponding amount of collateral liquidated will be:

$$
d = BorrowedFunds \cdot x \cdot (1 + \beta)
$$

where $$\beta$$ is the liquidation bonus.

The deposit cap can be determined by solving the following equation:

$$
u_{opt} \cdot DepositCap \cdot x \cdot (1 + \beta) = \frac{N_L}{T} \cdot L
$$

From which we have the model deposit cap:

$$
ModelDepositCap = \frac{N_L}{T} \cdot \frac{L}{u_{opt} \cdot x \cdot (1 + \beta)}
$$

### Expert Based Cap

The model cap is limited by an expert-based cap, which is set at 150% of the total on-chain liquidity:

$$
ExpertCap = 150% \cdot Q
$$

For new markets the cap is set at 30% of the total on-chain liquidity.

### Key Model Assumptions

* Linear recovery of on-chain liquidity after liquidation
* No market impact of liquidations on the price (liquidation cascade is not modelled)
* Deposit caps are determined independently for each market, disregarding combined effects

These simplifying assumptions are offset by using conservative parameters for the recovery period and liquidatable portion, alongside expert-derived caps.

### Key Model Parameters

The key model parameters are:

* $$x%$$ is the liquidated portion of the debt
* $$T$$ is the recovery time for DEX liquidity to get restored

Historical data should be used to estimate both parameters.

The liquidatable portion, determined by the account's simulation algorithm, is conservatively set at 30% for all assets in this simplified risk framework. Simulations indicate that this percentage typically ranges from 5% to 25%.

Estimating the liquidity recovery period following significant liquidations is challenging due to the difficulty in acquiring data on extreme on-chain liquidation events. However, observed arbitrage activity typically restores liquidity within minutes.

We conservatively consider three parameters:

* Base - 6h
* Optimistic - 2h
* Pessimistic - 12h

### Numerical Example

* $$\beta = 5%$$
* $$Q$$ is the total on-chain liquidity
* $$u_{opt} = 80%$$
* $$x = 30%$$
* $$T = 2h$$
* $$N_L = 24h$$

$$
ModelDepositCap = \frac{24}{2} \cdot \frac{L}{0.8 \cdot 0.3 \cdot (1 + 0.05)} \approx 47 \cdot L
$$

For xyk-type pool, the 5% depth is determined as follows:

$$L = \frac{Q}{2} \cdot 0.05$$

Then

$$
ModelDepositCap = 1.19 \cdot Q
$$

For PCL-type pool, we can apply adjustment of \~1.5x to increase the depth:

$$
L = \frac{Q}{2} \cdot 0.05 \cdot 1.5 = 0.0375 \cdot Q
$$

Then

$$
ModelDepositCap = 1.78 \cdot Q
$$

The expert cap is set to 150% of Q. So, the final cap would be:

$$
FinalDepositCap = \min(ModelDepositCap, ExpertCap) = 1.5 \cdot Q
$$
