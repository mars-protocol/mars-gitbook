---
description: >-
  The Health Contract calculates the health factor of user positions. It is used
  to enable and disable the liquidation by the Credit Manager.
---

# Health

### Deployments

Neutron: [neutron17ktfwsr7ghlxzzma0gw0hke3j3rnssd58q87jv2wzfrk6uhawa3sv8xxtm](https://neutron.celat.one/neutron-1/contracts/neutron17ktfwsr7ghlxzzma0gw0hke3j3rnssd58q87jv2wzfrk6uhawa3sv8xxtm)

Osmosis: [osmo1pdc49qlyhpkzx4j24uuw97kk6hv7e9xvrdjlww8qj6al53gmu49sge4g79](https://osmosis.celat.one/osmosis-1/contracts/osmo1pdc49qlyhpkzx4j24uuw97kk6hv7e9xvrdjlww8qj6al53gmu49sge4g79)

***

### Types

The types of the Health Contract can be found [here](https://github.com/mars-protocol/core-contracts/blob/master/scripts/types/generated/mars-rover-health/MarsRoverHealth.types.ts).

***

### Queries

#### config

Returns the contracts configuration.

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
        credit_manager: string | null
        owner_response: {
            abolished: boolean
            emergency_owner: string | null
            initialized: boolean
            owner: string | null
            proposed: string | null
        }
    }
}
```
{% endcode %}

#### health\_state

{% code title="Query message" %}
```typescript
{
    health_state: {
        account_id: string
        action: ActionKind
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: 'healthy' | {
        unhealthy: {
            max_ltv_health_factor: Decimal
        }
    }
}
```
{% endcode %}

#### health\_values

{% code title="Query message" %}
```typescript
{
    health_values: {
        account_id: string
        action: ActionKind
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        above_max_ltv: boolean
        has_perps: boolean
        liquidatable: boolean
        liquidation_health_factor?: Decimal | null
        liquidation_threshold_adjusted_collateral: Uint128
        max_ltv_adjusted_collateral: Uint128
        max_ltv_health_factor?: Decimal | null
        perps_pnl_loss: Uint128
        perps_pnl_profit: Uint128
        total_collateral_value: Uint128
        total_debt_value: Uint128
    }
}
```
{% endcode %}
