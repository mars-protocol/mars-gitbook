---
description: The Mars Protocol follows a strict Governance process.
---

# Governance

The Mars Protocol governance process enables the community to propose, discuss, and implement changes in a structured and transparent manner. It consists of **two to three stages**, depending on the type of proposal

### Step 1:  Proposal Draft on Forum

Anyone—including Mars Protocol contributors - must start by posting a proposal draft on the [Mars Protocol Forum](https://forum.marsprotocol.io/)&#x20;

* **Purpose:** Open community discussion and feedback.
* **Duration:** Must remain open for **at least 3 days**.
* **Requirement:** A proposal (Mars Request for Comment \[MRC]) can only move forward if there is **clear consensus on its feasibility and rationale**.



### Step 2: On-Chain Voting via DAO DAO

Once a forum draft achieves consensus, it can be submitted on-chain through the [Mars Protocol DAO DAO Governance Interface](https://daodao.zone/dao/neutron1pxjszcmmdxwtw9kv533u3hcudl6qahsa42chcs24gervf4ge40usaw3pcr).

* **Voting Period:** 3 days.
* **Eligibility:** Only users who **staked** [**MARS tokens**](governance/mars-token.md) **prior to proposal creation** are eligible to vote.
* **Voting Options:**
  * Yes
  * No
  * Abstain

> On Neutron, the majority of proposals include **executable messages**, meaning actions are carried out automatically once the proposal passes. The rest are signaling proposals that require manual follow-up.
>
> On Osmosis, by contrast, **all proposals are signaling-only**, so every action must be manually executed after the vote passes.



### Step 3 (Optional): Builders Multisig Execution

Some proposals, especially those involving smart contract changes, require manual execution by the **Mars Protocol Builders Multisig**.

* **Structure:** 5 Mars contributors with a **3-of-5 multisig**.
* **Responsibility:** Executing post-vote actions, such as:
  * Adjusting smart contract parameters
  * Broadcasting specific transactions

The Builders Multisig can only initiate the necessary on-chain actions, when a proposal has passed governance via DAO DAO.\
\
\


## Risk Management DAO

Mars Protocol also includes a **Risk Management DAO**, which has special authority to update asset and perpetual market configurations **without going through the full governance process**.

Exceptions apply:

* **Liquidation thresholds**
* **New asset or perps listings**



### Summary

| Stage               | Platform                                   | Duration | Who Participates                                      |
| ------------------- | ------------------------------------------ | -------- | ----------------------------------------------------- |
| Step 1              | [Forum](https://forum.marsprotocol.io/)    | ≥ 3 days | Community & Contributors                              |
| Step 2              | [DAO DAO Governance](https://daodao.zone/) | 3 days   | Staked [MARS Token](governance/mars-token.md) Holders |
| Step 3<sup>\*</sup> | Builders Multisig                          | N/A      | 3 of 5 Mars Contributors                              |

\*Optional step, only for proposals requiring manual execution.
