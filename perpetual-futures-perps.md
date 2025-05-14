# Perpetual Futures (Perps)

Mars Protocol implements oracle-based perpetual futures that are cross-margined and cross-collateralized within Credit Accounts. Users can trade at oracle prices using USDC as the settlement asset.

### Key Mechanics

#### Trading and Collateral

* Trades execute at oracle prices without requiring orderbook liquidity
* Perp positions are cross-margined, allowing unrealized PnL to act as collateral
* Any whitelisted asset in the Credit Account can serve as collateral for perp positions

#### Trading Fees

* Current fee: 0.075% of the perp position for each trade

#### Funding Rate

* Determined by Open Interest imbalance between Longs and Shorts (Skew)
* While skew remains in one direction, funding rate accumulates with increasing velocity
* Funding rate decreases when skew reverts direction
* Key parameters: SkewScale and Funding Rate Velocity

#### Expected Price

* Trading price varies based on market skew
* Reducing skew results in favorable pricing
* Increasing skew results in less favorable pricing

#### Perps Vault

* Acts as counterparty to all trades in USDC
* Processes PnL settlements
* Positive PnL: paid from vault to user's Credit Account
* Negative PnL: Paid from the user credit account to the vault. If the account does not hold sufficient USDC, the necessary amount is borrowed from the mars money market (Red Bank)
* 10-day lockup period for vault deposits
* Receives a percentage of trading fees

#### Keeper Order Bots

* Support for Limit, Stop, Take Profit, and Stop Loss orders
* Orders filled by third-party Keeper Bots
* Minimum Keeper Fee: $0.2, adjustable by users
* Higher Keeper Fees increase order fill priority
* Failed health checks result in order cancellation with Keeper Fee paid

#### Risk Parameters

* MaxOI: Maximum Open Interest based on market risk and vault liquidity
* MaxSkew: Maximum allowed imbalance between longs and shorts
* Auto-Deleveraging: Triggered when MaxOI or MaxSkew limits are reached, prioritizing larger position sizes for closure

### Tutorials

​Trading Perps Walkthrough (Zero to Hero)​ - coming soon
