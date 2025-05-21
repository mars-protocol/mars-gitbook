---
description: >-
  The Address Provider Contract provides the addresses of all most recent and
  currently used contracts of the Mars Protocol's set of Smart Contracts.
---

# Address Provider

### Deployments

Neutron: [neutron17yehp4x7n79zq9dlw4g7xmnrvwdjjj2yecq26844sg8yu74knlxqfx5vqv](https://neutron.celat.one/neutron-1/contracts/neutron17yehp4x7n79zq9dlw4g7xmnrvwdjjj2yecq26844sg8yu74knlxqfx5vqv)

Osmosis: [osmo1g677w7mfvn78eeudzwylxzlyz69fsgumqrscj6tekhdvs8fye3asufmvxr](https://osmosis.celat.one/osmosis-1/contracts/osmo1g677w7mfvn78eeudzwylxzlyz69fsgumqrscj6tekhdvs8fye3asufmvxr)

***

### Types

The types of the Address Provider Contract can be found [here](https://github.com/mars-protocol/core-contracts/blob/master/scripts/types/generated/mars-address-provider/MarsAddressProvider.types.ts).

For reference on the Queries and Methods:

{% code title="Base Types" %}
```typescript
type MarsAddressType =
  | 'incentives' 
  | 'oracle' 
  | 'red_bank' 
  | 'rewards_collector' 
  | 'params' 
  | 'credit_manager'
  | 'protocol_admin'
  | 'fee_collector'
  | 'safety_fund'
  | 'swapper'
  | 'astroport_incentives'
  | 'perps'
  | 'revenue_share'
```
{% endcode %}

***

### Queries

#### address

Provides the address of a certain contract type.

{% code title="Query message" %}
```typescript
{
    address: MarsAddressType
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        address: string
        address_type: MarsAddressType
    }
}
```
{% endcode %}

#### addresses

Provides an array of addresses for provided contract types.

{% code title="Query message" %}
```typescript
{
    addresses: MarsAddressType[]
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: [
        {
            address: string
            address_type: MarsAddressType
        },
        ...
    ]
}
```
{% endcode %}

#### all\_addresses

Returns all stored addresses with pagination.

{% code title="Query message" %}
```typescript
{
    all_addresses: {}
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: [
        {
            address: string
            address_type: MarsAddressType
        },
        ...
    ]
}
```
{% endcode %}

#### config

Returns the contracts config.

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
        owner?: string | null
        prefix: string
        proposed_new_owner?: string | null
    }
}
```
{% endcode %}

