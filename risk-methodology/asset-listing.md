---
description: >-
  Each asset—whether a standard token, an LP token, or part of a new protocol
  integration—must undergo careful evaluation before being added to Mars
  Protocol.
---

# Asset Listing

This process ensures that only **liquid**, **well-governed**, and **secure** assets are supported for lending, borrowing, or use as collateral.

***

## Evaluation Criteria

#### 1. **Technical and Centralization Risks**

* Security of underlying smart contracts
* Protocol governance and upgradeability
* Oracle pricing infrastructure
* Bridging mechanisms (if applicable)

#### 2. **Asset Type Considerations**

Mars applies tailored rules depending on asset class:

**• Single Tokens**

* Examples: `OSMO`, `USDC`, `TIA`
* Assessed for price stability, market depth, and liquidity

**• LP Tokens**

* Examples: `OSMO-axlUSDC LP`, `TIA-stTIA LP`
* Evaluated for **impermanent loss exposure**, dual-asset correlation, and DEX mechanics

> LP tokens may have **lower LTVs** due to IL risk and more complex price dynamics.

***

## Impermanent Loss & LP Tokens

Because **LP tokens are subject to impermanent loss (IL)**—especially during volatile market movements - the Mars framework may impose:

* Lower maximum LTVs
* Higher collateral thresholds for liquidation
* Stricter caps on borrowable amounts

***

## Final Approval

After both evaluation phases, final parameters are defined, including:

* **Loan-to-Value (LTV) Ratio**
* **Borrow and Deposit Caps**
* **Liquidation Thresholds**
* **Supported Use Cases** (collateral, borrowing, lending)

***

All asset listings are governed by the [Mars Protocol DAO](../governance.md), ensuring decentralized, community-led risk management aligned with Mars Protocol's mission of secure, composable DeFi infrastructure.

***
