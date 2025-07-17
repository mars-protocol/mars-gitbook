---
description: >-
  The Perps Contract provides data for the Perpetual Futures platform. It
  returns all market states and is needed for the Credit Manager to be able to
  execute trigger orders.
---

# Perps

### Deployments

Neutron: [neutron1g3catxyv0fk8zzsra2mjc0v4s69a7xygdjt85t54l7ym3gv0un4q2xhaf6](https://neutron.celat.one/neutron-1/contracts/neutron1g3catxyv0fk8zzsra2mjc0v4s69a7xygdjt85t54l7ym3gv0un4q2xhaf6)\
\
Perps Market API: [https://backend.prod.mars-dev.net/v2/perps\_market?chain=neutron](https://backend.prod.mars-dev.net/v2/perps_market?chain=neutron)

***

### Types

The types of the Perps Contract can be found [here](https://github.com/mars-protocol/core-contracts/blob/master/scripts/types/generated/mars-perps/MarsPerps.types.ts).

For reference on the Queries and Methods:

{% code title="Base Types" %}
```typescript
type Decimal = string
type Uint128 = string
type Int128 = string
type SignedDecimal = string
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

<pre class="language-typescript" data-title="Return output"><code class="lang-typescript">{
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
<strong>    }
</strong>}
</code></pre>

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

{% code title="Return output" %}
```typescript
{
    data: {
        cash_flow: {
            accrued_funding: Int128
            closing_fee: Int128
            opening_fee: Int128
            price_pnl: Int128
            protocol_fee: Uint128
        }
        denom: string
        enabled: boolean
        funding: {
            last_funding_accrued_per_unit_in_base_denom: SignedDecimal
            last_funding_rate: SignedDecimal
            max_funding_velocity: Decimal
            skew_scale: Uint128
        }
        last_updated: number
        long_oi: Uint128
        short_oi: Uint128
        total_abs_multiplied_positions: Int256
        total_entry_cost: Int128
        total_entry_funding: Int128
        total_squared_positions: Uint256
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

{% code title="Return output" %}
```typescript
{
    data: {
        data: [
            {
                denom: string
                enabled: boolean
                long_oi: Uint128
                long_oi_value: Uint128
                short_oi: Uint128
                short_oi_value: Uint128
                current_funding_rate: SignedDecimal
            },
            ...
        ]
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

{% code title="Return output" %}
```typescript
{
    data: {
        rate: SignedDecimal
        fee: {
            denom: string
            amount: Uint128
        }
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
        abolished: boolean
        emergency_owner?: string | null
        initialized: boolean
        owner?: string | null
        proposed?: string | null
    }
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

{% code title="Return output" %}
```typescript
{
    data: {
        account_id: string
        position?: {
            base_denom: string
            current_exec_price: Decimal
            current_price: Decimal
            denom: string
            entry_exec_price: Decimal
            entry_price: Decimal
            realized_pnl: {
                accrued_funding: Int128
                closing_fee: Int128
                opening_fee: Int128
                pnl: Int128
                price_pnl: Int128
            }
            size: Int128
            unrealized_pnl: {
                accrued_funding: Int128
                closing_fee: Int128
                opening_fee: Int128
                pnl: Int128
                price_pnl: Int128
            }
        }
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

{% code title="Return output" %}
```typescript
{
    data: {
        base_denom: string
        closing_exec_price?: Decimal | null
        closing_fee: Uint128
        opening_exec_price?: Decimal | null
        opening_fee: Uint128
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

{% code title="Return output" %}
```typescript
{
    data: [
        {
            account_id: string
            position?: {
                base_denom: string
                current_exec_price: Decimal
                current_price: Decimal
                denom: string
                entry_exec_price: Decimal
                entry_price: Decimal
                realized_pnl: {
                    accrued_funding: Int128
                    closing_fee: Int128
                    opening_fee: Int128
                    pnl: Int128
                    price_pnl: Int128
                }
                size: Int128
                unrealized_pnl: {
                    accrued_funding: Int128
                    closing_fee: Int128
                    opening_fee: Int128
                    pnl: Int128
                    price_pnl: Int128
                }
            }
        },
        ...
    ]
}
```
{% endcode %}

#### positions\_by\_account

{% code title="Query message" %}
```typescript
{
    positions_by_account: {
        account_id: string
        action?: 'default' | 'liquidation' | null
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        account_id: string
        positions: [
            {
                base_denom: string
                current_exec_price: Decimal
                current_price: Decimal
                denom: string
                entry_exec_price: Decimal
                entry_price: Decimal
                realized_pnl: {
                    accrued_funding: Int128
                    closing_fee: Int128
                    opening_fee: Int128
                    pnl: Int128
                    price_pnl: Int128
                }
                size: Int128
                unrealized_pnl: {
                    accrued_funding: Int128
                    closing_fee: Int128
                    opening_fee: Int128
                    pnl: Int128
                    price_pnl: Int128
                }
            },
            ...
        ]
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

{% code title="Return output" %}
```typescript
{
    data: {
        accrued_funding: Int128
        closing_fee: Int128
        opening_fee: Int128
        pnl: Int128
        price_pnl: Int128
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

<pre class="language-typescript" data-title="Return output"><code class="lang-typescript">{
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
<strong>        }
</strong>    }
}
</code></pre>

#### vault

{% code title="Query message" %}
```typescript
{
    vault: {
        action?: 'default' | 'liquidation' | null
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        collateralization_ratio?: Decimal | null
        share_price?: Decimal | null
        total_balance: Int128
        total_debt: Uint128
        total_liquidity: Uint128
        total_shares: Uint128
        total_unlocking_or_unlocked_amount: Uint128
        total_unlocking_or_unlocked_shares: Uint128
        total_withdrawal_balance: Uint128
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

{% code title="Return output" %}
```typescript
{
    data: {
        denom: string
        deposit: {
              amount: Uint128
              shares: Uint128
        }
        unlocks: [
            {
                amount: Uint128
                cooldown_end: number
                created_at: number
                shares: Uint128
            },
            ...
        ]
    }
}
```
{% endcode %}

***

### Methods

#### close\_all\_positions

<pre class="language-typescript" data-title="Execution message"><code class="lang-typescript">{
<strong>    close_all_positions: {
</strong>        account_id: string
        action?: 'default' | 'liquidation' | null
    }
}
</code></pre>

#### deleverage

{% code title="Execution message" %}
```typescript
{
    deleverage: {
        account_id: string
        denom: string
    }
}
```
{% endcode %}

#### deposit

{% code title="Execution message" %}
```typescript
{
    deposit: {
        account_id?: string | null
        max_shares_receivable?: Uint128 | null
    }
}
```
{% endcode %}

#### execute\_order

{% code title="Execution message" %}
```typescript
{
    execute_order: {
        account_id: string
        denom: string
        reduce_only?: boolean | null
        size: Int128
    }
}
```
{% endcode %}

#### unlock

{% code title="Execution message" %}
```typescript
{
    unlock: {
        account_id?: string | null
        shares: Uint128
    }
}
```
{% endcode %}

#### withdraw

{% code title="Execution message" %}
```typescript
{
    withdraw: {
        account_id?: string | null
        min_receive?: Uint128 | null
    }
}
```
{% endcode %}

***

### Audit

{% file src="../.gitbook/assets/2024-12-04 Audit Report - Mars Perps v1.0.pdf" %}
