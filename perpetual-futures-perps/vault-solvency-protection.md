# Vault Solvency Protection

## Vault Collateralization Ratio

The vault collateralization ratio (CR) is a critical solvency metric that measures the vault's ability to cover trader profits and maintain system stability. When this ratio falls below safe thresholds, an automated deleveraging mechanism activates to protect liquidity providers and preserve the protocol's financial integrity by systematically reducing the most profitable positions.

CR represents the relationship between the vault's available funds and its potential obligations to profitable traders. This ratio provides real-time insight into the vault's financial health and determines when protective measures must be activated.

$$
CR = \frac{TVL}{VaultDebt}
$$

where:



* **TVL (Total Value Locked)**: The current vault cash-flow balance representing actual deposited funds
* **VaultDebt**: The positive net global unrealized PnL that the vault owes to traders

### Collateralization Ratio Interpretation

The collateralization ratio provides clear signals about vault health:

* **CR > 1.5**: Healthy vault with adequate reserves
* **CR = 1.5**: Critical threshold triggering auto-deleveraging
* **CR < 1.5**: Active deleveraging zone requiring immediate position reductions
* **CR < 1.0**: Vault insolvency requiring emergency measures

## Auto-Deleverage Mechanism

When the collateralization ratio drops below 1.5, the protocol automatically activates deleveraging procedures to restore vault stability. This mechanism prioritizes the most profitable positions for closure, as reducing these positions provides the greatest improvement to the collateralization ratio.

### Deleverage Process

**Deleveraging Process**

The auto-deleveraging system follows a systematic approach:

1. **Threshold Monitoring**: Continuous monitoring of the collateralization ratio
2. **Trigger Activation**: Auto-deleveraging begins when CR falls below threshold
3. **Position Selection**: The system identifies the most profitable positions across all markets
4. **Sequential Closure**: Positions are closed in order of profitability, starting with the highest unrealized gains
5. **Ratio Improvement**: Each closure improves the collateralization ratio by reducing vault debt
6. **Continuation**: The process continues until CR rises above threshold

### Mathematical Rationale

The effectiveness of closing profitable positions can be demonstrated through collateralization ratio analysis. When the vault is solvent (CR ≥ 1.0), closing the most profitable position always improves the ratio because:

* The vault debt decreases by the full amount of the position's unrealized profit
* The vault's cash decreases by the same amount when paying out the profit
* Since CR ≥ 1.0, the vault has sufficient funds to cover the payout while improving the overall ratio

### Benefits of Auto-Deleverage

Auto-deleveraging provides essential protections for all stakeholders:

1. **Liquidity Providers**: Protected from excessive losses and vault insolvency
2. **Traders**: Benefit from system stability and continued operation
3. **Protocol**: Maintains integrity and user confidence
4. **Market**: Preserves orderly functioning during stress periods

This mechanism ensures that even during periods of extreme market movements or concentrated profitable positions, the vault maintains sufficient collateralization to honor its obligations while protecting the broader ecosystem from systemic risk.

