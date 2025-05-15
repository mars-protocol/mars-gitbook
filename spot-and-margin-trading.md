# Spot & Margin Trading

Mars Protocol offers two primary trading methods: Spot Trading and Margin Trading. Let's understand how each works and what makes Mars' approach unique.

### **Spot Trading**

Spot trading on Mars is straightforward DEX trading where you directly swap one asset for another using the funds available in your Credit Account. No leverage is involved - you're simply exchanging what you have for what you want at the current market price.

### **Margin Trading**

Margin trading takes things a step further by allowing you to trade with leverage. This means you can open larger positions than your deposited capital would normally allow. For example, with 100 USDC in your Credit Account, you could potentially trade 500 USDC worth of TIA by borrowing the additional 400 USDC.

### **Why Mars is Different**

Traditional DeFi platforms require multiple steps and interactions with money markets to achieve leverage (known as "looping"):

1. Deposit collateral
2. Borrow assets
3. Swap borrowed assets
4. Repeat steps 1-3 multiple times

This approach has two major drawbacks:

* Capital Inefficiency: Each loop requires new transactions and locks up more capital
* Poor User Experience: Multiple transactions mean higher gas fees and complexity

Mars Protocol improves this process through:

* One-Click Leverage: Execute margin trades in a single transaction
* Capital Efficient Credit Accounts: All assets serve as cross-collateral
* Seamless Integration: No need to juggle between multiple protocols or understand complex looping strategies

## **Understanding Leverage Risk**&#x20;

Trading on leverage comes with significant risks that users must understand:

**Liquidation Risk**

* When you trade on margin, your position is at risk of liquidation if your account health factor drops to 1 or below
* This typically happens when the value of your collateral decreases relative to your debt
* Mars provides an estimated liquidation price for each position to help you manage risk

**Liquidation Price Dynamics**

* For simple accounts with a single leveraged position and stablecoin debt, the shown liquidation price is generally accurate
* However, liquidation prices can fluctuate based on:
  * Multiple positions in the account
  * Non-stable debt (volatile assets)
  * Changes in other asset prices within the account

It's crucial to monitor your account health regularly when trading on leverage and maintain adequate safety margins.

### Tutorial

{% embed url="https://www.youtube.com/watch?v=hI6CLS3lTTE" %}

