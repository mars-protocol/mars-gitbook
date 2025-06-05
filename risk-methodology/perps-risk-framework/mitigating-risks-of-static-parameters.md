---
description: >-
  This section outlines the key risks arising from static risk parameters and
  the comprehensive measures implemented to manage these risks and maintain
  vault safety.
---

# Mitigating Risks of Static Parameters

### Risk Context

The key risk parameters (MaxOI, MaxSkew, MaxFundingVelocity) are all based on the vault TVL. Because these parameters are determined through Risk DAO proposals and remain static, a significant model risk exists: they can become overestimated if the vault TVL decreases substantially. Overestimation implies that potential losses arising from these parameters could exceed the desired risk tolerance of the vault.

The vault TVL can decrease over time because of two factors:

* Traders realizing large profits
* LPs withdrawing funds

### Risk Mitigation Measures

To manage these model risks, the following measures are implemented:

#### Lockdown Period

A 21-day lockdown period is in place for LPs before they can withdraw funds from the vault.

#### Dynamic Risk Alerts System

A risk alert is triggered upon substantial withdrawals from the vault or if the current net vault TVL significantly falls below the TVL used for risk parameter calibration. Following an alert, risk parameters are updated urgently.

#### Dynamic Risk Parameters Monitoring System

A comprehensive automated framework is under development to monitor risk parameter changes at a given frequency (at least daily).

#### Autodeleverage Mechanism

The autodeleverage mechanism for the vault's Collateralization Ratio and MaxOI control per market automatically closes positions when the actual value exceeds the target threshold.
