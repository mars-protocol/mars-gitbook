# Perps

### Deployments

Neutron: [neutron1g3catxyv0fk8zzsra2mjc0v4s69a7xygdjt85t54l7ym3gv0un4q2xhaf6](https://neutron.celat.one/neutron-1/contracts/neutron1g3catxyv0fk8zzsra2mjc0v4s69a7xygdjt85t54l7ym3gv0un4q2xhaf6)

### Types

The types of the Perps Contract can be found [here](https://github.com/mars-protocol/core-contracts/blob/master/scripts/types/generated/mars-perps/MarsPerps.types.ts).

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
    address_provider: string
    base_denom: string
    cooldown_period: number
    deleverage_enabled: boolean
    max_positions: number
    max_unlocks: number
    protocol_fee_rate: Decimal
    target_vault_collateralization_ratio: Decimal
    vault_withdraw_enabled: boolean
  }
}
```
{% endcode %}

#### market

{% code title="Query message" %}
```typescript
{
    market: {
        denom: string
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
  data: {
    current_funding_rate: SignedDecimal
    denom: string
    enabled: boolean
    long_oi: Uint128
    long_oi_value: Uint128
    short_oi: Uint128
    short_oi_value: Uint128
  }
}
```
{% endcode %}

#### market\_accounting

{% code title="Query message" %}
```typescript
{
    market_accounting: {
        denom: string
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
  data: {
    accounting: {
      balance: {
        accrued_funding: Int128
        closing_fee: Int128
        opening_fee: Int128
        price_pnl: Int128
        total: Int128
      }
      cash_flow: {
        accrued_funding: Int128
        closing_fee: Int128
        opening_fee: Int128
        price_pnl: Int128
        protocol_fee: Uint128
      }
      withdrawal_balance: {
        accrued_funding: Int128
        closing_fee: Int128
        opening_fee: Int128
        price_pnl: Int128
        total: Int128
      }
    }
    unrealized_pnl: {
      accrued_funding: Int128
      closing_fee: Int128
      opening_fee: Int128
      pnl: Int128
      price_pnl: Int128
    }
  }
}
```
{% endcode %}

#### market\_state

{% code title="Query message" %}
```typescript
{
    market_state: {
        denom: string
    }
}
```
{% endcode %}

#### markets

{% code title="Query message" %}
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

<pre class="language-typescript" data-title="Query message"><code class="lang-typescript">{
    opening_fee: {
        denom: string
        size: Int128
<strong>    }    
</strong>}
</code></pre>

#### owner

{% code title="Query message" %}
```typescript
{
    owner: {}
}
```
{% endcode %}

#### position

{% code title="Query message" %}
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

{% code title="Query message" %}
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

{% code title="Query message" %}
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

{% code title="Query message" %}
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

{% code title="Query message" %}
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

{% code title="Query message" %}
```typescript
{
    total_accounting: {}
}
```
{% endcode %}

#### vault

{% code title="Query message" %}
```typescript
{
    vault: {
        action?: ActionKind | null
    }
}
```
{% endcode %}

#### vault\_position

{% code title="Query message" %}
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
