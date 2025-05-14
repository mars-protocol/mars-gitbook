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

Only the owner of the contract can call its methods. That's why they are not part of the documentation.
