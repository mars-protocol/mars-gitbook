---
description: >-
  The Incentives Contract handles additional incentives. It offers the
  capability to incentivise markets permissionlessly by third parties. Incentive
  assets have to be whitelisted to be applied.
---

# Incentives

### Deployments

Neutron: [neutron1aszpdh35zsaz0yj80mz7f5dtl9zq5jfl8hgm094y0j0vsychfekqxhzd39](https://neutron.celat.one/neutron-1/contracts/neutron1aszpdh35zsaz0yj80mz7f5dtl9zq5jfl8hgm094y0j0vsychfekqxhzd39)

Osmosis: [osmo1nkahswfr8shg8rlxqwup0vgahp0dk4x8w6tkv3rra8rratnut36sk22vrm](https://osmosis.celat.one/osmosis-1/contracts/osmo1nkahswfr8shg8rlxqwup0vgahp0dk4x8w6tkv3rra8rratnut36sk22vrm)

***

### Types

The types of the Incentives Contract can be found [here](https://github.com/mars-protocol/core-contracts/blob/master/scripts/types/generated/mars-incentives/MarsIncentives.types.ts).

For reference on the Queries and Methods:

{% code title="Base Types" %}
```typescript
type Addr = string
type Decimal = string
type Uint128 = string
```
{% endcode %}

{% code title="Coin Types" %}
```typescript
interface Coin {
  amount: Uint128
  denom: string
  [k: string]: unknown
}
```
{% endcode %}

***

### Queries

#### active\_emissions

Return active emissions for a specific market by denom.

{% code title="Query message" %}
```typescript
{
    active_emissions: {
        denom: string
        kind: 'red_bank' | 'perp_vault'
    } 
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: [
        {
              denom: string
              emission_rate: Uint128
        },
        ...
    ]   
}
```
{% endcode %}

#### config

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
        address_provider: Addr
        epoch_duration: number
        max_whitelisted_denoms: number
        owner?: string | null
        proposed_new_owner?: string | null
        whitelist_count: number
    }
}
```
{% endcode %}

#### emission

{% code title="Query message" %}
```typescript
{
    emission: {
        denom: string
        incentive_denom: string
        kind: 'red_bank' | 'perp_vault'
        timestamp: number
    } 
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        emission_rate: Uint128
        epoch_start: number
    }
}
```
{% endcode %}

#### emissions

{% code title="Query message" %}
```typescript
{
    emissions: {
        denom: string
        incentive_denom: string
        kind: 'red_bank' | 'perp_vault'
        limit?: number | null
        start_after_timestamp?: number | null
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: [
        {
            emission_rate: Uint128
            epoch_start: number
        },
        ...
    ]   
}
```
{% endcode %}

#### incentive\_state

{% code title="Query message" %}
```typescript
{
    incentive_state: {
        denom: string
        incentive_denom: string
        kind: 'red_bank' | 'perp_vault'
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
          denom: string
          incentive_denom: string
          index: Decimal
          kind: 'red_bank' | 'perp_vault'
          last_updated: number
    }
}
```
{% endcode %}

#### incentive\_states

{% code title="Query message" %}
```typescript
{
    incentive_states: {
        limit?: number | null
        start_after_denom?: string | null
        start_after_incentive_denom?: string | null
        start_after_kind?: 'red_bank' | 'perp_vault' | null
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: [
        {
            denom: string
            incentive_denom: string
            index: Decimal
            kind: 'red_bank' | 'perp_vault'
            last_updated: number
        },
        ...   
    ]
}
```
{% endcode %}

#### staked\_astro\_lp\_position

{% code title="Query message" %}
```typescript
{
    staked_astro_lp_position: {
        account_id: string
        lp_denom: string
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
          lp_coin: Coin
          rewards: Coin[]
    }
}
```
{% endcode %}

#### staked\_astro\_lp\_positions

{% code title="Query message" %}
```typescript
{
    staked_astro_lp_positions: {
        account_id: string
        limit?: number | null
        start_after?: string | null
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        data: [
            {
                lp_coin: Coin
                rewards: Coin[]
            },
            ...
        ]
        metadata: {
            has_more: boolean
        }
    }
}
```
{% endcode %}

#### staked\_astro\_lp\_rewards

{% code title="Query message" %}
```typescript
{
    staked_astro_lp_rewards: {
        account_id: string
        lp_denom: string
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        data: [
            [string, Coin[]],
            ...
        ]
        metadata: {
            has_more: boolean
        }
    }
}
```
{% endcode %}

#### user\_unclaimed\_rewards

{% code title="Query message" %}
```typescript
{
    user_unclaimed_rewards: {
        account_id?: string | null
        limit?: number | null
        start_after_denom?: string | null
        start_after_incentive_denom?: string | null
        start_after_kind?: 'red_bank' | 'perp_vault' | null
        user: string
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: Coin[]
}
```
{% endcode %}

#### whitelist

{% code title="Query message" %}
```typescript
{
    whitelist: {}
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: [
        {
            denom: string
            min_emission_rate: Uint128
        },
        ...   
    ]
}
```
{% endcode %}

***

### Methods

#### balance\_change

{% code title="Execution message" %}
```typescript
{
    balance_change: {
        account_id?: string | null
        denom: string
        kind: 'red_bank' | 'perp_vault'
        total_amount: Uint128
        user_addr: Addr
        user_amount: Uint128
    }
}
```
{% endcode %}

#### claim\_rewards

{% code title="Execution message" %}
```typescript
{
    claim_rewards: {
        account_id?: string | null
        limit?: number | null
        start_after_denom?: string | null
        start_after_incentive_denom?: string | null
        start_after_kind?: 'red_bank' | 'perp_vault' | null
    }
}
```
{% endcode %}

#### claim\_staked\_astro\_lp\_rewards

{% code title="Execution message" %}
```typescript
{
    claim_staked_astro_lp_rewards: {
        account_id: string
        lp_denom: string
    }    
}
```
{% endcode %}

#### set\_asset\_incentive

{% code title="Execution message" %}
```typescript
{
    set_asset_incentive: {
        denom: string
        duration: number
        emission_per_second: Uint128
        incentive_denom: string
        kind: 'red_bank' | 'perp_vault'
        start_time: number
    }
}
```
{% endcode %}

#### stake\_astro\_lp

{% code title="Execution message" %}
```typescript
{
    stake_astro_lp: {
        account_id: string
        lp_coin: Coin
    }
}
```
{% endcode %}

#### unstake\_astro\_lp

<pre class="language-typescript" data-title="Execution message"><code class="lang-typescript">{
<strong>    unstake_astro_lp: {
</strong>        account_id: string
        lp_coin: ActionCoin
    }
}
</code></pre>
