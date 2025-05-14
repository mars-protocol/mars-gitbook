---
description: >-
  The Account NFT Contract returns all Credit Account NFT infos and handles the
  minting and burning of Credit Accounts via the Credit Manager.
---

# Account NFT

### Deployments

Neutron: [neutron184kvu96rqtetmunkkmhu5hru8yaqg7qfhd8ldu5avjnamdqu69squrh3f5](https://neutron.celat.one/neutron-1/contracts/neutron184kvu96rqtetmunkkmhu5hru8yaqg7qfhd8ldu5avjnamdqu69squrh3f5)

Osmosis: [osmo1450hrg6dv2l58c0rvdwx8ec2a0r6dd50hn4frk370tpvqjhy8khqw7sw09](https://osmosis.celat.one/osmosis-1/contracts/osmo1450hrg6dv2l58c0rvdwx8ec2a0r6dd50hn4frk370tpvqjhy8khqw7sw09)

***

### Types

The types of the Account NFT Contract can be found [here](https://github.com/mars-protocol/core-contracts/blob/master/scripts/types/generated/mars-account-nft/MarsAccountNft.types.ts).

For reference on the Queries and Methods:

{% code title="Base Types" %}
```typescript
type Binary = string
type Uint128 = string
type Expiration =
  | {
      at_height: number
    }
  | {
      at_time: Timestamp
    }
  | {
      never: {}
    }
```
{% endcode %}

***

### Queries

#### all\_nft\_info

Returns all NFT related infos for a the provided token\_id.

{% code title="Query message" %}
```typescript
{
    all_nft_info: {
        include_expired?: boolean | null
        token_id: string
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        access: {
            approvals: [
                {
                      expires: Expiration
                      spender: string
                },
                ...
            ]
            owner: string
        }
        info: {
            extension: [k: string]: unknown
            token_uri?: string | null
        }
    }
}
```
{% endcode %}

#### all\_operators

{% code title="Query message" %}
```typescript
{
    all_operators: {
        include_expired?: boolean | null
        limit?: number | null
        owner: string
        start_after?: string | null
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        operators: [
            {
                expires: Expiration
                spender: string
            },
            ...
        ]
    }
}
```
{% endcode %}

#### all\_tokens

{% code title="Query message" %}
```typescript
{
    all_tokens: {
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
        tokens: string[]
    }
}
```
{% endcode %}

#### approvals

{% code title="Query message" %}
```typescript
{
    approvals: {
        include_expired?: boolean | null
        token_id: string
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        approvals: [
            {
                expires: Expiration
                spender: string
            },
            ...
        ]
    }
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
        credit_manager_contract_addr?: string | null
        health_contract_addr?: string | null
        max_value_for_burn: Uint128
    }
}
```
{% endcode %}

#### contract\_info

{% code title="Query message" %}
```typescript
{
    contract_info: {}
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        name: string
        symbol: string
    }
}
```
{% endcode %}

#### minter

{% code title="Query message" %}
```typescript
{
    minter: {}
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        minter: string
    }
}
```
{% endcode %}

#### next\_id

{% code title="Query message" %}
```typescript
{
    next_id: {}
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: Uint128
}
```
{% endcode %}

#### nft\_info

{% code title="Query message" %}
```typescript
{
    nft_info: {
        token_id: string
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        extension: [k: string]: unknown
        token_uri?: string | null
    }
}
```
{% endcode %}

#### num\_tokens

{% code title="Query message" %}
```typescript
{
    num_tokens: {}
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        count: number
    }
}
```
{% endcode %}

#### owner\_of

{% code title="Query message" %}
```typescript
{
    owner_of: {
        include_expired?: boolean | null
        token_id: string
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        approvals: [
            {
                expires: Expiration
                spender: string
            },
            ...
        ]         
        owner: string
    }
}
```
{% endcode %}

#### ownership

{% code title="Query message" %}
```typescript
{
    ownership: {}
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        owner: string
        pending_owner: Expiration | null
        pending_expiry: Addr | null
    }
}
```
{% endcode %}

#### tokens

{% code title="Query message" %}
```typescript
{
    tokens: {
        limit?: number | null
        owner: string
        start_after?: string | null
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        tokens: string[]
    }
}
```
{% endcode %}

***

### Methods

The Account NFT methods can only be executed by the [Credit Manager](credit-manager.md). The methods are therefore not a part of the documentation.
