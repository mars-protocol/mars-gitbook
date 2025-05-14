# Perps

### Deployments

Neutron: [neutron1g3catxyv0fk8zzsra2mjc0v4s69a7xygdjt85t54l7ym3gv0un4q2xhaf6](https://neutron.celat.one/neutron-1/contracts/neutron1g3catxyv0fk8zzsra2mjc0v4s69a7xygdjt85t54l7ym3gv0un4q2xhaf6)

### Types

The types of the Perps Contract can be found [here](https://github.com/mars-protocol/core-contracts/blob/master/scripts/types/generated/mars-perps/MarsPerps.types.ts).

### Queries

#### config

{% code title="QueryMsg" %}
```typescript
{
    config: {}
}
```
{% endcode %}

#### market

{% code title="QueryMsg" %}
```typescript
{
    market: {
        denom: string
    }
}
```
{% endcode %}

#### market\_accounting

{% code title="QueryMsg" %}
```typescript
{
    market_accounting: {
        denom: string
    }
}
```
{% endcode %}

#### market\_state

{% code title="QueryMsg" %}
```typescript
{
    market_state: {
        denom: string
    }
}
```
{% endcode %}

#### markets

{% code title="QueryMsg" %}
```typescript
{
    markets: {
        limit?: number | null
        start_after?: string | null
    }
}
```
{% endcode %}

#### opening\_fee

<pre class="language-typescript" data-title="QueryMsg"><code class="lang-typescript">{
    opening_fee: {
        denom: string
        size: Int128
<strong>    }    
</strong>}
</code></pre>

#### owner

{% code title="QueryMsg" %}
```typescript
{
    owner: {}
}
```
{% endcode %}

#### position

{% code title="QueryMsg" %}
```typescript
{
    position: {
        account_id: string
        denom: string
        order_size?: Int128 | null
        reduce_only?: boolean | null
    }
}
```
{% endcode %}

#### position\_fees

{% code title="QueryMsg" %}
```typescript
{
    position_fees: {
        account_id: string
        denom: string
        new_size: Int128
    }
}
```
{% endcode %}

#### positions

{% code title="QueryMsg" %}
```typescript
{
    positions: {
        limit?: number | null
        start_after?: [string, string] | null
    }
}
```
{% endcode %}

#### positions\_by\_account

{% code title="QueryMsg" %}
```typescript
{
    positions_by_account: {
        account_id: string
        action?: ActionKind | null
    }
}
```
{% endcode %}

#### realized\_pnl\_by\_account\_and\_market

{% code title="QueryMsg" %}
```typescript
{
    realized_pnl_by_account_and_market: {
        account_id: string
        denom: string
    }
}
```
{% endcode %}

#### total\_accounting

{% code title="QueryMsg" %}
```typescript
{
    total_accounting: {}
}
```
{% endcode %}

#### vault

{% code title="QueryMsg" %}
```typescript
{
    vault: {
        action?: ActionKind | null
    }
}
```
{% endcode %}

#### vault\_position

{% code title="QueryMsg" %}
```typescript
{
    vault_position: {
        account_id?: string | null
        user_address: string
    }
}
```
{% endcode %}

### Methods

### Audit

{% file src="../.gitbook/assets/2024-12-04 Audit Report - Mars Perps v1.0.pdf" %}
