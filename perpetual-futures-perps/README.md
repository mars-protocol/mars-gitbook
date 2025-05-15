---
description: >-
  Mars Protocol offers oracle-based perpetual futures trading, seamlessly
  integrated into its Credit Account system.
---

# Perpetual Futures (Perps)

This architecture enables cross-margined and cross-collateralized leveraged trading using **USDC as the settlement asset**.

Unlike traditional orderbook-based systems, Mars executes perp trades at real-time **oracle prices**, ensuring deep liquidity access and deterministic execution - making it especially suitable for capital-efficient DeFi trading.

***

### Key Mechanics

#### Trading and Collateralization

* **Oracle Pricing:**\
  All perpetual futures trades are executed at the **oracle price**, removing reliance on orderbook liquidity and minimizing front-running risks.
* **Cross-Margining:**\
  Unrealized **Profit and Loss (PnL)** across positions can be used as additional margin, increasing capital efficiency.
* **Cross-Collateralization:**\
  Any **whitelisted asset** within a Credit Account (e.g., ATOM, stATOM, dATOM, etc.) can serve as collateral for perpetual futures positions, not just USDC.

***

### Trading Fees

* **Per Trade Fee:**\
  A fixed **0.075% fee** is charged on the notional value of each perpetual futures trade. This fee is collected in USDC and partially allocated to the **Perps Vault**.

***

### Funding Rate Mechanism

To maintain alignment between perpetual futures prices and the underlying spot price, Mars implements a **skew-based funding rate model**:

* **Skew-Based Calculation:**\
  Funding rates are determined by **Open Interest (OI) imbalance** between long and short positions - referred to as _skew_.
* **Velocity and Accumulation:**
  * The longer the skew persists in one direction, the **faster funding costs accumulate**.
  * If skew reverses, the funding rate **dampens** accordingly.
* **Key Parameters:**
  * **SkewScale**: Determines the sensitivity of funding rate to skew size.
  * **Funding Rate Velocity**: Controls the rate at which funding accrues.

***

### Expected Price Dynamics

The effective trading price of a perpetual contract can deviate from the oracle price depending on skew:

* **Reduced Skew = Favorable Price:**\
  When a trade **reduces skew**, execution price is more favorable to the trader.
* **Increased Skew = Unfavorable Price:**\
  When a trade **increases skew**, execution price becomes less favorable, discouraging imbalance.

***

### The Perps Vault

The **Perps Vault** acts as the **counterparty to all trades** and manages trade settlements in USDC.

* **PnL Settlements:**
  * **Positive PnL:** Paid out from the vault to the user's Credit Account.
  * **Negative PnL:** Collected from the user's Credit Account.
    * If the account lacks sufficient USDC, the deficit is **borrowed from the Red Bank** (Mars Money Market).
* **Deposit Lock-Up:**\
  Deposits into the vault are subject to a **10-day lockup period**.
* **Fee Participation:**\
  The vault receives a **portion of trading fees**, supporting long-term sustainability.

***

### Keeper Order Bots

Mars supports **automated order execution** through third-party **Keeper Bots**, enabling:

* **Advanced Order Types:**
  * Limit Orders
  * Stop Orders
  * Take Profit / Stop Loss
* **Keeper Fee System:**
  * **Minimum Fee:** $0.20 (adjustable by user).
  * **Priority Queue:** Higher Keeper Fees result in faster execution priority.
  * **Health Checks:** If the order violates health checks (e.g., insolvency), it is cancelled and the Keeper Fee is still paid.

***

### Risk Parameters and Controls

Mars Protocol enforces robust limits to mitigate systemic risk:

* **MaxOI (Maximum Open Interest):**\
  Caps total open interest across long and short positions based on vault liquidity and asset volatility.
* **MaxSkew:**\
  Defines the maximum allowed imbalance between long and short positions to prevent destabilization.
* **Auto-Deleveraging (ADL):**\
  Triggered when either **MaxOI** or **MaxSkew** limits are breached. Positions with larger notional values are prioritized for **forced reduction**, ensuring system solvency.

***

**Mars Perpetual Futures combine high capital efficiency with risk-aware design**, enabling a scalable, transparent, and fair trading environment without traditional orderbook dependencies.
