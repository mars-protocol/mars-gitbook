---
description: >-
  The Oracle Contract returns the price data for the entire Money Market and the
  Perps Platform. It utilizes multiple price sources, ranging from external
  oracles like Pyth or Slinky, to TWAP and Spot.
---

# Oracle

### Deployments

Neutron: [neutron1dwp6m7pdrz6rnhdyrx5ha0acsduydqcpzkylvfgspsz60pj2agxqaqrr7g](https://neutron.celat.one/neutron-1/contracts/neutron1dwp6m7pdrz6rnhdyrx5ha0acsduydqcpzkylvfgspsz60pj2agxqaqrr7g)

Osmosis: [osmo1mhznfr60vjdp2gejhyv2gax9nvyyzhd3z0qcwseyetkfustjauzqycsy2g](https://osmosis.celat.one/osmosis-1/contracts/osmo1mhznfr60vjdp2gejhyv2gax9nvyyzhd3z0qcwseyetkfustjauzqycsy2g)

***

### Types

The types of the Oracle Contract can be found [here](https://github.com/mars-protocol/core-contracts/blob/master/scripts/types/generated/mars-oracle-wasm/MarsOracleWasm.types.ts).

For reference on the Queries and Methods:

{% code title="Base Types" %}
```typescript
type Decimal = string
```
{% endcode %}

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
        base_denom: string
        owner: string | null
        proposed_new_owner: string | null
    }
}
```
{% endcode %}

#### price

{% code title="Query message" %}
```typescript
{
    price: {
        denom: string
        kind?: 'default' | 'liquidation' | null
    }  
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        denom: string
        price: Decimal
    }
}
```
{% endcode %}

#### price\_source

{% code title="Query message" %}
```typescript
{
    price_source: {
        denom: string
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        denom: string
        price_source: string
    }
}
```
{% endcode %}

#### price\_sources

{% code title="Query message" %}
```typescript
{
    price_sources: {
        limit?: number | null
        start_after?: string | null
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
            price_source: string
        },
        ...
    ]   
}
```
{% endcode %}

#### prices

{% code title="Query message" %}
```typescript
{
    prices: {
        kind?: 'default' | 'liquidation' | null
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
        
    }
}
```
{% endcode %}

#### prices\_by\_denoms

{% code title="Query message" %}
```typescript
{
    prices_by_denoms: {
        denoms: string[]
        kind?: 'default' | 'liquidation' | null
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
            price: Decimal    
        },
        ...
    ]
}
```
{% endcode %}

***

### Methods

Only the owner of the contract can call its methods. That's why they are not part of the documentation.\
\


***

### Circuit Breakers

Instead of naively absorbing the feeds received from Pyth, Mars v2 implements two new circuit breakers intended to mitigate potential price manipulation attacks. These circuit breakers will activate whenever the volatility of a certain feed is extremely high or there’s too much uncertainty over the real level of a certain price. Whenever any of these filters triggers, the transaction will be invalidated\*. The circuit breakers are the following:

* **Exponential Moving Average (EMA)**: In addition to the spot price, Pyth offers an Exponential Moving Average (EMA) with each price feed. The EMA is a single price that aggregates the spot price and historical prices for a certain asset, where “the most recent samples receive the most weight, and samples further back in time get exponentially less weight the farther in the past they are.” Given this characteristic, the EMA is significantly more resistant to manipulation than the spot price. This is the reason we incorporate the EMA as a circuit breaker. The way we incorporate it is as follows:
  * First, we set some bounds above and below the EMA (i.e. Upper Bound = EMA + 15%; Lower Bound = EMA - 15%).
  * Then we check whether the spot price is within those bounds.
  * If it is, the transaction is valid.
  * If it isn’t, the transaction is invalidated.
* **Confidence Interval (CI)**: Pyth offers a CI with each feed that informs on the level of certainty that the publishers of that feed have on the reported price. All else equal, the larger the CI, the lower the certainty of publishers on the real spot price of the asset. As such, the rationale for incorporating this circuit breaker is obvious. The way it’s implemented is as follows:
  * If the ratio between the CI and the EMA is above a certain threshold, the transaction is invalidated.

Both the magnitude of the EMA bounds and the Confidence Interval threshold are governance defined parameters.

_Note that there are some exceptions on what transactions are invalidated by circuit breakers triggering. These exceptions are: liquidation, deposit and repay transactions. The reason for the exceptions is that we want to always guarantee liveness for these transactions. For liquidations because solvency of the system is a paramount concern and circuit breakers could lead to halting liquidations. For deposit and repay transactions because we want to allow users to always be able to save their positions from liquidation, even when certain circuit breakers are activated. There’s one final exception, and it’s for withdraw transactions from accounts with no debt._

**These circuit breakers trade off liveness for security. For a lending protocol, we believe this is a worthwhile tradeoff. However, users should be aware that when these new circuit breakers are triggered they won’t be able to interact with the protocol (including borrows, withdrawals and so on). This could lead to temporary or permanent loss of funds or value, including the inability to sell assets while prices or market conditions are deteriorating. While we don’t expect this to happen often, it is definitely a possibility.**

**Additionally, as with the new liquidations mechanism, these new circuit breakers might lead to unforeseen issues at both the mechanism and smart contract levels.**\
