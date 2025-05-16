---
description: >-
  Managed Vaults on Mars Protocol are a powerful tool enabling the decentralized
  deployment of trading strategies via community-managed Credit Accounts.
---

# Managed Vaults

These vaults allow experienced traders or strategy designers to operate funds on behalf of depositors—while adhering to strict security and operational constraints.

Each Managed Vault is built on a **Credit Account**, giving the manager access to leverage and trading capabilities without ever being able to directly deposit or withdraw assets, ensuring robust separation of powers and minimizing risk.

***

### Key Features

Managed Vaults are designed to combine **capital efficiency**, **decentralized strategy deployment**, and **user safety**. Core features include:

* **Fungible LP Shares:**\
  Users who deposit into a vault receive **fungible vault shares**, which represent their proportional claim on the vault’s assets and performance.
* **Vault Manager Access:**\
  Managers interact with the Mars **trading interface** to execute trades and manage leveraged positions via the Credit Account.
* **No Manager Withdrawals:**\
  Managers are **restricted from depositing or withdrawing** from the vault directly. This guarantees that only users control capital inflow and outflow.
* **Automated Liquidity Handling:**\
  If users request withdrawals and the vault lacks sufficient **USDC** liquidity, the system will **automatically borrow USDC** from the Red Bank to fulfill the request, maintaining usability and minimizing friction.

***

### Vault Parameters

Managed Vaults incorporate configurable parameters to balance flexibility with control:

#### Performance Fee

* Accrues **daily** based on the vault’s performance.
* Managers can **claim fees monthly**, aligned with protocol governance standards.
* Performance fee rates are **adjustable**, but only during the monthly withdrawal window to ensure transparency and user trust.

#### Withdrawal Period

* Vaults may enforce a **withdrawal lock-up period**, designed to protect strategy integrity and manage liquidity effectively.
* This period defines how often users may withdraw their funds from the vault.

***

### Vault Management Mechanics

Mars Protocol introduces mechanisms to ensure vaults remain responsive to user actions while preserving strategic autonomy for managers.

* **Withdrawal Scheduling:**\
  The user interface clearly communicates the **upcoming withdrawal window**, allowing users and managers to plan accordingly.
* **USDC Liquidity Preparation:**\
  Vault managers can proactively prepare **USDC liquidity** before scheduled withdrawals to avoid slippage or forced borrowing.
* **Automated Borrowing Backup:**\
  If a vault is underprepared, Mars will **automatically borrow USDC** from the Red Bank to fulfill withdrawals. This ensures **withdrawal reliability** without compromising the strategy.

***

### Tutorials and How-Tos

To support users and prospective vault managers, Mars Protocol provides comprehensive tutorials:

* **Creating & Managing a Vault**\
  A guide for traders or strategy designers on how to configure, launch, and responsibly manage a vault.

{% content-ref url="creating-a-vault.md" %}
[creating-a-vault.md](creating-a-vault.md)
{% endcontent-ref %}

* **Depositing into a Managed Vault**\
  Step-by-step instructions for users to evaluate, select, and deposit into a community vault.

{% content-ref url="depositing-into-vault.md" %}
[depositing-into-vault.md](depositing-into-vault.md)
{% endcontent-ref %}

***

**Managed Vaults democratize access to advanced DeFi strategies**, allowing passive users to benefit from the expertise of experienced traders while maintaining non-custodial control and system-wide transparency.
