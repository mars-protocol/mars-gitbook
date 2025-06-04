---
description: >-
  Account liquidation automatically closes undercollateralized positions and
  sells collateral to protect the system from bad debt while incentivizing
  liquidators to maintain market stability.
---

# Liquidations

Account liquidation is the protocol's final safety mechanism that automatically closes positions and sells collateral when a trader's account becomes undercollateralized. This process protects the system from bad debt while providing liquidators with economic incentives to maintain market stability and ensure all participants can meet their obligations.

### Liquidation Trigger

Liquidation occurs when an account's health factor falls below 1.0, indicating that the account's risk-weighted assets are insufficient to cover its obligations. The liquidation process ensures that positions are closed before they can generate losses that exceed the available collateral.

### Liquidation Process

Before the standard liquidation mechanism begins, the protocol automatically closes all perpetual positions in the account. This crucial first step converts complex derivative exposures into simple spot asset and debt positions.

When liquidation is triggered:

1. **Health Factor Check**: Initial verification that HF < 1.0
2. **Position Closure**: All perpetual positions are closed&#x20;
3. **PnL Settlement**: Unrealized profits and losses are settled according to standard procedures
4. **Standard Liquidation**: The account now contains only spot assets and debts. The protocol applies the existing Mars liquidation mechanism.

Importantly, after closing perpetual positions, the health factor may recover above 1.0, but the liquidation process continues to completion to ensure system stability.
