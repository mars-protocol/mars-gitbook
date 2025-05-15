# Lending & Borrowing

## Lending & Borrowing on Mars Protocol

### Interest Rate Model

Mars Protocol uses a two-slope utilization model similar to other leading money markets like Aave. This model determines interest rates based on the utilization rate of each asset.

#### How It Works

The interest rate model is designed with two key slopes:

* The first slope (0% to Optimal Utilization) features a gradual increase in rates
* The second slope (Optimal Utilization to 100%) shows a steeper increase to discourage full utilization

<figure><img src=".gitbook/assets/Screenshot 2024-12-17 at 7.35.31 PM.png" alt=""><figcaption></figcaption></figure>

Interest rates are calculated as follows:

* Borrowing APR increases as utilization increases
* Lending APR is derived from the borrowing APR, but is always lower because it's distributed across all lenders
* Protocol aims to maintain utilization around the optimal point for maximum efficiency

### Asset Whitelisting

#### Lending Restrictions

* Only whitelisted assets can be lent or borrowed
* Not all whitelisted assets can be borrowed
* Liquid Staking Tokens (LSTs) typically cannot be borrowed due to potential price manipulation risks
* Assets that cannot be borrowed will not have a lending APR

### Lending Features

#### Deposit Caps

* All whitelisted assets are subject to deposit caps
* Caps apply regardless of whether the asset is being lent
* Current deposit levels and remaining capacity are displayed for each asset
* Detailed information about caps available in risk parameters section

#### Auto-Lend Feature

* Users can enable "Auto-lend" toggle in the credit account section
* When enabled, any deposited assets are automatically lent out
* Simplifies the lending process and maximizes yield opportunities

### Borrowing Features

#### Borrowing Options

* Borrow directly to wallet or credit account
* Wallet borrowing increases account leverage
* Available liquidity displayed for each asset
* Manual debt repayment options available

#### Liquidity Information

* Real-time display of available liquidity for each asset
* Clear indication of maximum borrowing capacity
* Utilization rate impacts borrowing costs

### Tutorials

* [Lending and Borrowing](https://www.youtube.com/watch?v=mIXxmkrlWNI)

