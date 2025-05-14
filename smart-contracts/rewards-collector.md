---
description: >-
  The Rewards Collector Contract provides all the needed methods to withdraw
  generated fees and revenue from the Mars Protocol. It also handles swapping
  the collected revenue/fees to a specified asset.
---

# Rewards Collector

### Deployments

Neutron: [neutron1h4l6rvylzcuxwdw3gzkkdzfjdxf4mv2ypfdgvnvag0dtz6x07gps6fl2vm](https://neutron.celat.one/neutron-1/contracts/neutron1h4l6rvylzcuxwdw3gzkkdzfjdxf4mv2ypfdgvnvag0dtz6x07gps6fl2vm)

Osmosis: [osmo1urvqe5mw00ws25yqdd4c4hlh8kdyf567mpcml7cdve9w08z0ydcqvsrgdy](https://osmosis.celat.one/osmosis-1/contracts/osmo1urvqe5mw00ws25yqdd4c4hlh8kdyf567mpcml7cdve9w08z0ydcqvsrgdy)

***

### Types

The types of the Rewards Collector Contract can be found [here](https://github.com/mars-protocol/core-contracts/blob/master/scripts/types/generated/mars-rewards-collector-base/MarsRewardsCollectorBase.types.ts).

***

### Queries

#### config

Returns the Contracts configuration.

{% code title="Query message" %}
```typescript
{
    config: {}    
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        address_provider: string
        channel_id: string
        fee_collector_config: {
            target_denom: string
            transfer_type: 'ibc' | 'bank'
        }
        owner?: string | null
        proposed_new_owner?: string | null
        revenue_share_config: {
            target_denom: string
            transfer_type: 'ibc' | 'bank'
        }
        revenue_share_tax_rate: Decimal
        safety_fund_config: {
            target_denom: string
            transfer_type: 'ibc' | 'bank'
        }
        safety_tax_rate: Decimal
        slippage_tolerance: Decimal
        timeout_seconds: number
    }
}
```
{% endcode %}

***

### Methods

The rewards collector contract is operated by a bot used by the Mars Protocol contributors. There is no need for third party contributors to run or execute the methods of the rewards collector. That's why they are not part of the documentation.
