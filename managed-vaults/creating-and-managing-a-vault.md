# Creating & Managing a Vault

Managed Vaults on Mars Protocol enable users to deploy trading strategies on behalf of depositors. As a vault manager, you can execute trades using your vault’s account, but you **cannot withdraw or transfer** deposited assets directly.\
In return for managing the strategy, you earn a **performance fee** — a percentage of the vault's profit, that is claimable monthly.

This guide walks you through the steps to create and manage a Vault using the Mars App interface. You’ll learn how to:

* Set up your vault’s parameters (title, fee, lockup period, etc.)
* Optionally seed your vault with an initial deposit
* Finalize vault creation and start managing assets



⚠️ **Important notes:**

* A **$50 creation fee** is charged in the selected deposit asset at the time of vault creation.
* It is recommended vaults **are funded** upon creation in order to appear in the public vault listings. Unfunded vaults will remain hidden.



Here’s what the **Create Vault** screen looks like in the Mars App:

> This screen allows you to configure your vault’s title, asset, initial deposit, performance fee, and withdrawal lockup period.

<figure><img src="../.gitbook/assets/Screenshot 2025-05-14 at 5.51.13 PM.png" alt=""><figcaption></figcaption></figure>

#### Add a Clear Strategy Description

When filling in the **description** field during vault creation, it's important to clearly explain the strategy your vault will follow.

A good description helps depositors understand what they’re investing in, how the strategy works, and what to expect in terms of risk or asset focus.

> **Example:**\
> “Rotates between BTC and ETH perpetuals based on relative strength and market signals. Optimized for volatile market conditions.”

Avoid vague descriptions like “trading stuff” or “DeFi plays.” The more transparent and specific you are, the more likely users will trust and deposit into your vault.

#### **Optional: Personalize your vault**

You can connect your **Stargaze profile** or **IBC/ICNS Domain** to display a profile picture, social links, and ENS-style name alongside your vault. This adds credibility and helps depositors connect with your strategy.



### **Finalizing Your Vault**

Once you're happy with your vault’s configuration - including its title, strategy description, performance fee, lockup period, and initial deposit - you can proceed with the creation process.

Creating a Managed Vault requires **up to three on-chain transactions**:

1. **Vault Creation** – Deploys the vault and saves its parameters
2. **Vault Account Minting** – Sets up the credit account tied to the vault
3. **Initial Deposit** _(optional)_ – If you choose to deposit during creation



You’ll be prompted to approve each step in your wallet.

**After creation is complete**, you’ll be redirected to your vault’s dedicated management page. From there, you can begin monitoring performance and executing your trading strategy.

If you funded the vault during creation, it will also appear on the main public vaults listing. Unfunded vaults will remain hidden.



⚠️ **Note:**

The **vault title, deposit asset, description, and withdrawal lockup period** cannot be changed after creation.

You can still adjust the **performance fee** later - but only once per month, typically during the performance fee claim window.



## Managing Your Vault

After successfully creating your Vault, you’ll be redirected to its management dashboard. This is your control center for monitoring performance, managing positions, and preparing for withdrawals.

You can return to this page anytime via the **vault page**, your **portfolio**, or by selecting the vault from the **Credit Account dropdown menu**.

> This screen provides a live overview of your vault’s performance, withdrawal status, and available management actions.

<figure><img src="../.gitbook/assets/Screenshot 2025-05-14 at 8.40.43 PM.png" alt=""><figcaption></figcaption></figure>

### Key Areas of the Vault Dashboard

Here are the key elements you'll find on the vault dashboard:

* **Vault Summary (left panel)**\
  Shows your vault’s title, description, APY, total value locked (TVL), performance fee %, and the withdrawal freeze period. It also includes your Stargaze-linked identity (if connected).
* **Performance Fee Panel (top panel)**\
  Displays how much in fees you’ve earned. You can only claim performance fees once per month -typically during the claim window. A claim button will appear when available.                                         ⚠️ **Note:**\
  The displayed fee amount is based on the vault’s accrued PnL, but this value only updates when someone deposits into or withdraws from the vault. If there’s no user activity, the fee may appear outdated even if your positions have changed in value.
* **Deposit / Unlock Buttons**\
  You can deposit additional funds into your own vault or unlock funds if you’ve previously deposited and requested withdrawal.
*   **Withdrawal Summary Tab**\
    This section provides key insight into withdrawal activity and vault liquidity. You should monitor it closely to ensure your vault can fulfill queued withdrawals.

    Here’s what it shows:

    *   **Accrued PnL** - Displays profit (or loss) generated since the last performance fee withdrawal. This determines your claimable fee.

        > This value only updates when a user interacts with the vault (e.g. deposits or withdrawals). If there’s no activity, it may appear unchanged even if your positions have moved in value.
    * **My Withdrawals tab** – Lets you track any pending withdrawal requests made from your own vault deposits.
    *   **Queued Withdrawals vs. Vault Balance** – Shows how much has been requested for withdrawal vs. how much of the deposit asset is available.

        > If there's a shortfall, the system will **automatically borrow the asset from the Red Bank** to fulfill the withdrawals. It's your responsibility to monitor this and prepare accordingly.
    * **My Withdrawals tab** – Lets you track any pending withdrawal requests made from your own vault deposits.
* **Health & Position Metrics (bottom panel)**\
  Displays key risk indicators such as health factor, leverage, total position value, debt, and current position APY.

> If your vault has any active positions, the bottom panel will display additional tabs such as Summary, Balances, and Perps Positions.

<figure><img src="../.gitbook/assets/Screenshot 2025-05-15 at 9.20.58 PM.png" alt=""><figcaption></figcaption></figure>

\
