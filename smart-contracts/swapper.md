# Swapper

### Deployments

Neutron: [neutron1udr9fc3kd743dezrj38v2ac74pxxr6qsx4xt4nfpcfczgw52rvyqyjp5au](https://neutron.celat.one/neutron-1/contracts/neutron1udr9fc3kd743dezrj38v2ac74pxxr6qsx4xt4nfpcfczgw52rvyqyjp5au)

Osmosis: [osmo1wee0z8c7tcawyl647eapqs4a88q8jpa7ddy6nn2nrs7t47p2zhxswetwla](https://osmosis.celat.one/osmosis-1/contracts/osmo1wee0z8c7tcawyl647eapqs4a88q8jpa7ddy6nn2nrs7t47p2zhxswetwla)

***

### Types

The types of the Rewards Collector Contract can be found [here](https://github.com/mars-protocol/core-contracts/blob/master/scripts/types/generated/mars-swapper-base/MarsSwapperBase.types.ts).

For reference on the Queries and Methods: &#x20;

{% code title="Base Types" %}
```typescript
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
        router: string
        factory: string
        oracle: string"
    }
}
```
{% endcode %}

#### estimate\_exact\_in\_swap

{% code title="Query message" %}
```typescript
{
    estimate_exact_in_swap: {
        coin_in: Coin
        denom_out: string
        route?: {
            astro: {
                swaps: [
                    {
                        from: string
                        to: string
                    },
                    ...
                ]
        } | {
            osmo: {
                swaps: [
                    {
                        pool_id: number
                        to: string
                    },
                    ...
                ]
        } | null
    } 
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        router: string
        factory: string
        oracle: string"
    }
}
```
{% endcode %}

#### owner

{% code title="Query message" %}
```typescript
{
    owner: {}  
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        router: string
        factory: string
        oracle: string"
    }
}
```
{% endcode %}

#### route

{% code title="Query message" %}
```typescript
{
    route: {
        denom_in: string
        denom_out: string
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        router: string
        factory: string
        oracle: string"
    }
}
```
{% endcode %}

#### routes

{% code title="Query message" %}
```typescript
{
    routes: {
        limit?: number | null
        start_after?: [string, string] | null
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        router: string
        factory: string
        oracle: string"
    }
}
```
{% endcode %}

***

### Methods

#### swap\_exact\_in

{% code title="Execution message" %}
```typescript
{
    swap_exact_in: {
        coin_in: Coin
        denom_out: string
        min_receive: Uint128
        route?: {
            astro: {
                swaps: [
                    {
                        from: string
                        to: string
                    },
                    ...
                ]
        } | {
            osmo: {
                swaps: [
                    {
                        pool_id: number
                        to: string
                    },
                    ...
                ]
        } | null
    }
}
```
{% endcode %}
