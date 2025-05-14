# Zapper

### Deployments

Neutron: [neutron1dr0ckm3u2ztjuscmgqjr85lwyduphxkgl3tc02ac8zp54r05t5dqp5tgyq](https://neutron.celat.one/neutron-1/contracts/neutron1dr0ckm3u2ztjuscmgqjr85lwyduphxkgl3tc02ac8zp54r05t5dqp5tgyq)

Osmosis: [osmo17qwvc70pzc9mudr8t02t3pl74hhqsgwnskl734p4hug3s8mkerdqzduf7c](https://osmosis.celat.one/osmosis-1/contracts/osmo17qwvc70pzc9mudr8t02t3pl74hhqsgwnskl734p4hug3s8mkerdqzduf7c)

***

### Types

The types of the Zapper Contract can be found [here](https://github.com/mars-protocol/core-contracts/blob/master/scripts/types/generated/mars-zapper-base/MarsZapperBase.types.ts).

For reference on the Queries and Methods: &#x20;

{% code title="Base Types" %}
```typescript
type Addr = string
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

#### estimate\_provide\_liquidity

{% code title="Query message" %}
```typescript
{
    estimate_provide_liquidity: {
        coins_in: Coin[]
        lp_token_out: string
    }
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

#### estimate\_withdraw\_liquidity

{% code title="Query message" %}
```typescript
{
    estimate_withdraw_liquidity: {
        coin_in: Coin
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

***

### Methods

#### callback

{% code title="Execution message" %}
```typescript
{
    callback: {
        return_coin: {
            balance_before: Coin
            recipient: Addr
        }
    }
}
```
{% endcode %}

#### provide\_liquidity

{% code title="Execution message" %}
```typescript
{
    provide_liquidity: {
        lp_token_out: string
        minimum_receive: Uint128
        recipient?: string | null
    }
}
```
{% endcode %}

#### withdraw\_liquidity

{% code title="Execution message" %}
```typescript
{
    withdraw_liquidity: {
        minimum_receive: Coin[]
        recipient?: string | null
    }
}
```
{% endcode %}
