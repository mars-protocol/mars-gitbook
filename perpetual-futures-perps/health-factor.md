---
description: >-
  The health factor is a critical risk metric that determines whether a trading
  account remains solvent and above liquidation thresholds.
---

# Health Factor

The health factor computation varies depending on whether the account holds long or short perpetual positions, as each direction presents different risk profiles. The formula incorporates risk-weighted assets, position values, funding payments, and safety margins through closing fees to provide a comprehensive assessment of account solvency.

### Long Position Health Factor

For accounts holding a single long perpetual position, the health factor is calculated as:

$$
HF = \frac{RWA + P \times (LTV_p - \phi_c) + f_{\$}^+ \times LTV_p}{D + P_0 + f_{\$}^-}
$$

### Short Position Health Factor

For accounts holding a single short perpetual position, the health factor is calculated as:

$$
HF = \frac{RWA + P_0 + f_{\$}^+ \times LTV_p}{D + P \times (2 - LTV_p + \phi_c) + f_{\$}^-}
$$

### Component Defintions

* $$RWA$$ (Risk-Weighted Assets): The value of all collateral assets other than the perpetual position, weighted by their respective loan-to-value ratios
* $$D$$ : Total borrowings excluding the perpetual position being evaluated
* $$LTV_p$$: The loan-to-value parameter specific to perpetual positions, determining leverage
* $$\phi_c$$: The closing fee percentage
* $$P_0$$: The notional value of the position when it was opened, calculated as `|q| × p_{ex,0}`
* $$P$$: The current notional value of the position, calculated as `|q| × p_{ex}`
* $$f_{$}^{+}$$: Positive funding payments owed to the position holder (added to assets)
* $$f_{$}^{-}$$  : Negative funding payments owed by the position holder (added to liabilities)

### Multiple Perp Positions

In cases where an account holds multiple perpetual positions across different markets, the health factor is computed similarly by aggregating the corresponding numerator and denominator components from each position. Each perpetual position contributes its respective terms based on whether it is long or short, with all components summed together to calculate the overall account health factor.

### Health Factor Interpretation

The health factor provides clear guidance on account status:

* **HF ≥ 1.0**: Account is healthy and above liquidation threshold
* **HF < 1.0**: Account is subject to liquidation to protect system solvency
* **Higher values**: Indicate greater safety margins and ability to withstand adverse price movements
* **Values approaching 1.0**: Signal increasing risk and potential need for additional collateral

### Risk Management Through Health Factor

The health factor serves multiple risk management functions:

1. **Position Sizing**: Maximum position sizes are determined by ensuring health factor remains above 1.0
2. **Liquidation Trigger**: Automatic liquidation begins when health factor drops below 1.0
3. **Real-time Monitoring**: Continuous calculation allows traders to monitor their risk exposure

### Example of Health Factor Calculation

Consider a trader with the following account composition:

* $50,000 USDC collateral (Liquidation LTV for USDC = 92%)
* $20,000 in other risk-weighted assets
* $10,000 total debt
* 10 ETH long position opened at $2,000 per ETH
* Current ETH price: $2,200
* Perpetual LTV: 90%
* Closing fee: 0.075%
* Accumulated funding: +$100 (positive, owed to trader)

Calculations:

* RWA = $50,000 × 0.92 + $20,000 = $66,000
* P₀ = 10 × $2,000 = $20,000
* P = 10 × $2,200 = $22,000
* f₊ = $100, f₋ = $0

$$
HF = \frac{66,000 + 22,000 \times (0.90 - 0.00075) + 100 \times 0.90}{10,000 + 20,000 + 0}=2.86
$$

This health factor of 2.86 indicates a well-collateralized position with significant safety margin before liquidation.

