---
description: >-
  The Perps Risk Framework is employed by Mars protocol for estimating risk
  parameters in perps markets.
---

# Perps Risk Framework

The primary goal is to ensure sufficient margin and safeguards against extreme losses, price manipulation, and excessive market imbalances.

### Key Risk Parameters

* **Margin Requirements:** Maximum Leverage, Maximum LTV, Liquidation LTV are determined using the extreme-loss approach and CVaR risk metric based on historical price data. Leverage caps are applied according to asset quality categories.
* **Market Impact Model Parameter:** SkewScale is calculated based on global market depth to ensure attractive trading when the market is balanced.
* **Open Interest Limits:** Maximum Open Interest (MaxOI) and Maximum Skew are determined through multiple approaches: Extreme Price Change, Manipulation Scenario, and Expert Caps, with consideration for vault TVL.
* **Funding Rate Model Parameters:** MaxFundingVelocity is calculated to incentivize traders to close positions when the skew is high and prevent extreme price changes from generating profits beyond what funding payments would offset.
* **Trading Fees:** Maker and taker fees are established based on competitor analysis.

### Methodology Highlights

* Calculations are primarily based on historical price data, global market depth, and vault TVL.
* Conservative assumptions, such as static skew and worst-case scenarios, are often used in calculations.
* Risk parameters are typically updated every three months but can be urgently updated based on risk alerts, such as substantial TVL decreases or withdrawals.
* Special cases are considered for new assets with limited data history.

### Other Risk Management Measures

* Dynamic Risk Alerts and Monitoring Systems for key parameters.
* Lockdown period for vault LPs.
* Autodeleverage mechanism for MaxOI control.

The framework aims to balance risk management and capital efficiency, ensuring the long-term sustainability of Mars protocol's perp markets.

All risk parameters are calculated off-chain and approved through the proposals for Risk DAO.
