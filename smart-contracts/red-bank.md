# Red Bank

### Deployments

Neutron: [neutron1n97wnm7q6d2hrcna3rqlnyqw2we6k0l8uqvmyqq6gsml92epdu7quugyph](https://neutron.celat.one/neutron-1/contracts/neutron1n97wnm7q6d2hrcna3rqlnyqw2we6k0l8uqvmyqq6gsml92epdu7quugyph)

Osmosis: [osmo1c3ljch9dfw5kf52nfwpxd2zmj2ese7agnx0p9tenkrryasrle5sqf3ftpg](https://osmosis.celat.one/osmosis-1/contracts/osmo1c3ljch9dfw5kf52nfwpxd2zmj2ese7agnx0p9tenkrryasrle5sqf3ftpg)

***

### Types

The types of the Incentives Contract can be found [here](https://github.com/mars-protocol/core-contracts/blob/master/scripts/types/generated/mars-red-bank/MarsRedBank.types.ts).

For reference on the Queries and Methods:

{% code title="Base Types" %}
```typescript
type Decimal = string
type Uint128 = string
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

<pre class="language-typescript" data-title="Return output"><code class="lang-typescript">{
<strong>    data: {
</strong>        address_provider: string
        owner?: string | null
        proposed_new_owner?: string | null
    }
}
</code></pre>

#### ~~market~~ (outdated)

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
        borrow_index: Decimal
        borrow_rate: Decimal
        collateral_total_scaled: Uint128
        debt_total_scaled: Uint128
        denom: string
        indexes_last_updated: number
        interest_rate_model: {
            base: Decimal
            optimal_utilization_rate: Decimal
            slope_1: Decimal
            slope_2: Decimal
        }
        liquidity_index: Decimal
        liquidity_rate: Decimal
        reserve_factor: Decimal
    }
}
```
{% endcode %}

#### market\_v2

{% code title="Query message" %}
```typescript
{
    market_v2: {
        denom: string
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        borrow_index: Decimal
        borrow_rate: Decimal
        collateral_total_amount: Uint128
        collateral_total_scaled: Uint128
        debt_total_amount: Uint128
        debt_total_scaled: Uint128
        denom: string
        indexes_last_updated: number
        interest_rate_model: {
            base: Decimal
            optimal_utilization_rate: Decimal
            slope_1: Decimal
            slope_2: Decimal
        }
        liquidity_index: Decimal
        liquidity_rate: Decimal
        reserve_factor: Decimal
        utilization_rate: Decimal
    }
}
```
{% endcode %}

#### ~~markets~~ (outdated)

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
                borrow_index: Decimal
                borrow_rate: Decimal
                collateral_total_scaled: Uint128
                debt_total_scaled: Uint128
                denom: string
                indexes_last_updated: number
                interest_rate_model: {
                    base: Decimal
                    optimal_utilization_rate: Decimal
                    slope_1: Decimal
                    slope_2: Decimal
                }
                liquidity_index: Decimal
                liquidity_rate: Decimal
                reserve_factor: Decimal
            },
            ...
        ]
    }
}
```
{% endcode %}

#### markets\_v2

{% code title="Query message" %}
```typescript
{
    markets_v2: {
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
                borrow_index: Decimal
                borrow_rate: Decimal
                collateral_total_amount: Uint128
                collateral_total_scaled: Uint128
                debt_total_amount: Uint128
                debt_total_scaled: Uint128
                denom: string
                indexes_last_updated: number
                interest_rate_model: {
                    base: Decimal
                    optimal_utilization_rate: Decimal
                    slope_1: Decimal
                    slope_2: Decimal
                }
                liquidity_index: Decimal
                liquidity_rate: Decimal
                reserve_factor: Decimal
            },
            ...
        ]
        meta_data: {
            has_more: boolean
        }
    }
}
```
{% endcode %}

#### scaled\_debt\_amount

{% code title="Query message" %}
```typescript
{
    scaled_debt_amount: {
        amount: Uint128
        denom: string
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: Uint123
}
```
{% endcode %}

#### scaled\_liquidity\_amount

{% code title="Query message" %}
```typescript
{
    scaled_liquidity_amount: {
        amount: Uint128
        denom: string
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: Uint123
}
```
{% endcode %}

#### underlying\_debt\_amount

{% code title="Query message" %}
```typescript
{
    underlying_debt_amount: {
        amount_scaled: Uint128
        denom: string
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: Uint123
}
```
{% endcode %}

#### underlying\_liquidity\_amount

{% code title="Query message" %}
```typescript
{
    underlying_liquidity_amount: {
        amount_scaled: Uint128
        denom: string
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: Uint123
}
```
{% endcode %}

#### user\_collateral

{% code title="Query message" %}
```typescript
{
    user_collateral: {
        account_id?: string | null
        denom: string
        user: string
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        amount: Uint128
        amount_scaled: Uint128
        denom: string
        enabled: boolean
    }
}
```
{% endcode %}

#### ~~user\_collaterals~~ (outdated)

{% code title="Query message" %}
```typescript
{
    user_collaterals: {
        account_id?: string | null
        limit?: number | null
        start_after?: string | null
        user: string
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: [
        {
            account_id?: string | null
            limit?: number | null
            start_after?: string | null
            user: string
        },
        ...
    ]    
}
```
{% endcode %}

#### user\_collaterals\_v2

{% code title="Query message" %}
```typescript
{
    user_collaterals_v2: {
        account_id?: string | null
        limit?: number | null
        start_after?: string | null
        user: string
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
                account_id?: string | null
                limit?: number | null
                start_after?: string | null
                user: string
            },
            ...
        ]
        meta_data: {
            has_more: boolean
        }
    }
}
```
{% endcode %}

#### user\_debt

{% code title="Query message" %}
```typescript
{
    user_debt: {
        denom: string
        user: string
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        amount: Uint128
        amount_scaled: Uint128
        denom: string
        uncollateralized: boolean
    }
}
```
{% endcode %}

#### user\_debts

{% code title="Query message" %}
```typescript
{
    user_debts: {
        limit?: number | null
        start_after?: string | null
        user: string
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: [
        {
            amount: Uint128
            amount_scaled: Uint128
            denom: string
            uncollateralized: boolean
        },
        ...
    ]
}
```
{% endcode %}

#### user\_position

{% code title="Query message" %}
```typescript
{
    user_position: {
        account_id?: string | null
        user: string
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        health_status: 'not_borrowing' | {
            borrowing: {
                liq_threshold_hf: Decimal
                max_ltv_hf: Decimal
            }
        }
        total_collateralized_debt: Uint128
        total_enabled_collateral: Uint128
        weighted_liquidation_threshold_collateral: Uint128
        weighted_max_ltv_collateral: Uint128
    }
}
```
{% endcode %}

#### user\_position\_liquidation\_pricing

{% code title="Query message" %}
```typescript
{
    user_position_liquidation_pricing: {
        account_id?: string | null
        user: string
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        health_status: 'not_borrowing' | {
            borrowing: {
                liq_threshold_hf: Decimal
                max_ltv_hf: Decimal
            }
        }
        total_collateralized_debt: Uint128
        total_enabled_collateral: Uint128
        weighted_liquidation_threshold_collateral: Uint128
        weighted_max_ltv_collateral: Uint128
    }
}
```
{% endcode %}

***

### Methods

#### borrow

{% code title="Execution message" %}
```typescript
{
      borrow: {
            amount: Uint128
            denom: string
            recipient?: string | null
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
        on_behalf_of?: string | null
    }
}
```
{% endcode %}

#### liquidate

{% code title="Execution message" %}
```typescript
{
    liquidate: {
        collateral_denom: string
        recipient?: string | null
        user: string
    }
}
```
{% endcode %}

#### repay

{% code title="Execution message" %}
```typescript
{
    repay: {
        on_behalf_of?: string | null
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
        amount?: Uint128 | null
        denom: string
        liquidation_related?: boolean | null
        recipient?: string | null
    }
}
```
{% endcode %}
