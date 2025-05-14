---
description: >-
  The Credit Manager Contract is the centerpiece of the Mars Protocol v2. It
  serves as a proxy between the user, the Red Bank, the liquidation engine, and
  the Perps contracts.
---

# Credit Manager

### Deployments

Neutron: [neutron1qdzn3l4kn7gsjna2tfpg3g3mwd6kunx4p50lfya59k02846xas6qslgs3r](https://neutron.celat.one/neutron-1/contracts/neutron1qdzn3l4kn7gsjna2tfpg3g3mwd6kunx4p50lfya59k02846xas6qslgs3r)

Osmosis: [osmo1f2m24wktq0sw3c0lexlg7fv4kngwyttvzws3a3r3al9ld2s2pvds87jqvf](https://osmosis.celat.one/osmosis-1/contracts/osmo1f2m24wktq0sw3c0lexlg7fv4kngwyttvzws3a3r3al9ld2s2pvds87jqvf)

***

### Types

The types of the Credit Manager Contract can be found [here](https://github.com/mars-protocol/core-contracts/blob/master/scripts/types/generated/mars-credit-manager/MarsCreditManager.types.ts).

For reference on the Queries and Methods:

{% code title="Base Types" %}
```typescript
type AccountKind =
  | ('default' | 'high_levered_strategy')
  | {
      fund_manager: {
        vault_addr: string
      }
    }
type ActionKind = 'default' | 'liquidation'
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
type HealthState =
  | 'healthy'
  | {
      unhealthy: {
        max_ltv_health_factor: Decimal
      }
    }
type Int128 = string    
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

interface ActionCoin {
  amount: 'account_balance' | { exact: Uint128 }
  denom: string
}
```
{% endcode %}

***

### Conditions

Conditions are used to create triggers for trigger orders. They are referenced as the **Condition** type in the Methods below.

#### health\_factor

```typescript
{
    health_factor: {
        comparison: 'greater_than' | 'less_than'
        threshold: Decimal
    }
}
```

#### oracle\_price

```typescript
{
    oracle_price: {
        comparison: 'greater_than' | 'less_than'
        denom: string
        price: Decimal
    }
}
```

#### relative\_price

```typescript
{
    relative_price: {
        base_price_denom: string
        comparison: 'greater_than' | 'less_than'
        price: Decimal
        quote_price_denom: string
    }
}
```

***

### Actions

A central part of the Credit Manager are the Actions. Actions can be combined into powerful sequences by lining them up in an array (they will be executed in a top to down maner). They are referenced via the **Action** type in the Methods below.

#### borrow

```typescript
{
    borrow: Coin
}
```

#### claim\_astro\_lp\_rewards

```typescript
{
    claim_astro_lp_rewards: {
        lp_denom: string
    }
}
```

#### claim\_rewards

```typescript
{
    claim_rewards: {}
}
```

#### create\_trigger\_order

```typescript
{
    create_trigger_order: {
        actions: Action[]
        conditions: Condition[]
        keeper_fee: Coin
    }
}
```

#### delete\_trigger\_order

```typescript
{
    delete_trigger_order: {
        trigger_order_id: string
    }
}
```

#### deposit

```typescript
{
    deposit: Coin
}
```

#### deposit\_to\_perp\_vault

```typescript
{
    deposit_to_perp_vault: {
        coin: ActionCoin
        max_receivable_shares?: Uint128 | null
    }
}
```

#### enter\_vault

```typescript
{
    enter_vault: {
        coin: ActionCoin
        vault: string
    }
}
```

#### execute\_perp\_order

```typescript
{
    execute_perp_order: {
        denom: string
        order_size: Int128
        reduce_only?: boolean | null
    }
}
```

#### exit\_vault

```typescript
{
    exit_vault: {
        amount: Uint128
        vault: string
    }
}
```

#### exit\_vault\_unlocked

```typescript
{
    exit_vault_unlocked: {
        id: number
        vault: VaultBaseForString
    }
}
```

#### lend

```typescript
{
    lend: ActionCoin
}
```

#### liquidate

```typescript
{
    debt_coin: Coin
    liquidatee_account_id: string
    request: {
        deposit: string
    } | {
        lend: string
    } | {
        vault: {
          position_type: 'u_n_l_o_c_k_e_d' | 'l_o_c_k_e_d' | 'u_n_l_o_c_k_i_n_g'
          request_vault: string
        }
    } | {
        staked_astro_lp: string
    }
}
```

#### provide\_liquidity

<pre class="language-typescript"><code class="lang-typescript"><strong>{
</strong><strong>    provide_liquidity: {
</strong>        coins_in: ActionCoin[]
        lp_token_out: string
        slippage: Decimal
    }
}
</code></pre>

#### reclaim

```typescript
{
    reclaim: ActionCoin
}
```

#### refund\_all\_coin\_balances

```typescript
{
    refund_all_coin_balances: {}
}
```

#### repay

```typescript
{
    repay: {
        coin: ActionCoin
        recipient_account_id?: string | null
    }
}
```

#### request\_vault\_unlock

```typescript
{
    request_vault_unlock: {
        amount: Uint128
        vault: string
    }
}
```

#### stake\_astro\_lp

```typescript
{
    stake_astro_lp: {
        lp_token: ActionCoin
    }
}
```

#### swap\_exact\_in

```typescript
swap_exact_in: {
    coin_in: ActionCoin
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
        }
    }
    | {
        osmo: {
            swaps: [
                {
                    pool_id: number
                    to: string
                },
                ...
            ]
        }
    } | null
}
```

#### unlock\_from\_perp\_vault

```typescript
{
    unlock_from_perp_vault: {
        shares: Uint128
    }
}
```

#### unstake\_astro\_lp

```typescript
{
    unstake_astro_lp: {
        lp_token: ActionCoin
    }
}
```

#### withdraw

```typescript
{
    withdraw: ActionCoin
}
```

#### withdraw\_from\_perp\_vault

```typescript
{
    withdraw_from_perp_vault: {
        min_receive?: Uint128 | null
    }
}
```

#### withdraw\_liquidity

```typescript
{
    withdraw_liquidity: {
        lp_token: ActionCoin
        slippage: Decimal
    }
}
```

#### withdraw\_to\_wallet

```typescript
{
    withdraw_to_wallet: {
        coin: ActionCoin
        recipient: string
    }
}
```

***

### Queries

#### account\_kind

Returns the AccountKind of a specific account\_id.

{% code title="Query message" %}
```typescript
{
    account_kind: {
        account_id: string
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: AccountKind
}
```
{% endcode %}

#### accounts

{% code title="Query message" %}
```typescript
{
    accounts: {
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
    data: [
        {
            id: string
            kind: AccountKind
        },
        ...
    ]
}
```
{% endcode %}

#### all\_account\_trigger\_orders

{% code title="Query message" %}
```typescript
{
    all_account_trigger_orders: {
        account_id: string
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
                account_id: string
                order: {
                    actions: Action[]
                    conditions: Condition[]
                    keeper_fee: Coin
                    order_id: string
                }
            },
            ...
        ]
        metadata: {
            has_more: boolean
        }
    }
}

```
{% endcode %}

#### all\_coin\_balances

<pre class="language-typescript" data-title="Query message"><code class="lang-typescript">{
<strong>    all_coin_balances: {
</strong>        limit?: number | null
        start_after?: [string, string] | null
    }    
}
</code></pre>

{% code title="Return output" %}
```typescript
{
    data: [
        {
            account_id: string
            amount: Uint128
            denom: string
        },
        ...
    ]
}
```
{% endcode %}

#### all\_debt\_shares

<pre class="language-typescript" data-title="Query message"><code class="lang-typescript">{
<strong>    all_debt_shares: {
</strong>        limit?: number | null
        start_after?: [string, string] | null
    }    
}
</code></pre>

{% code title="Return output" %}
```typescript
{
    data: [
        {
            account_id: string
            shares: Uint128
            denom: string
        },
        ...
    ]
}
```
{% endcode %}

#### all\_total\_debt\_shares

{% code title="Query message" %}
```typescript
{
    all_total_debt_shares: {
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
            shares: Uint128
            denom: string
        },
        ...
    ]
}
```
{% endcode %}

#### all\_trigger\_orders

{% code title="Query message" %}
```typescript
{
    all_trigger_orders: {
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
        data: [
            {
                account_id: string
                order: {
                    actions: Action[]
                    conditions: Condition[]
                    keeper_fee: Coin
                    order_id: string
                }
            },
            ...
        ]
        metadata: {
            has_more: boolean
        }
    }
}
```
{% endcode %}

#### all\_vault\_positions

{% code title="Query message" %}
```typescript
{
    all_vault_positions: {
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
            position: {
                vault_position: {
                    amount: {
                        unlocked: string
                    } | {
                        locking: {
                            locked: string
                            unlocking: [
                                {
                                    coin: Coin
                                    id: number
                                },
                            ...
                            ]
                        }
                    }
                    vault: string
                }
            }
        },
        ...
    ]
}
```
{% endcode %}

#### all\_vault\_utilizations

{% code title="Query message" %}
```typescript
{
    all_vault_utilizations: {
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
                utilization: Coin
                vault: string
            },
            ...
        ]
        metadata: {
            has_more: boolean
        }
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
        account_nft?: string | null
        health_contract: string
        incentives: string
        keeper_fee_config: {
            min_fee: Coin
        }
        max_slippage: Decimal
        max_unlocking_positions: Uint128
        oracle: string
        ownership: {
            abolished: boolean
            emergency_owner?: string | null
            initialized: boolean
            owner?: string | null
            proposed?: string | null
        }
        params: string
        perps: string
        perps_liquidation_bonus_ratio: Decimal
        red_bank: string
        rewards_collector?: {
          account_id: string
          address: string
        } | null
        swapper: string
        zapper: string
    }
}
```
{% endcode %}

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
        lp_token: Coin
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

#### positions

<pre class="language-typescript" data-title="Query message"><code class="lang-typescript">{
<strong>    positions: {
</strong>        account_id: string
        action?: ActionKind | null
    }
}
</code></pre>

{% code title="Return output" %}
```typescript
{
    data: {
        account_id: string
        account_kind: AccountKind
        debts: [
            {
                amount: Uint128
                denom: string
                shares: Uint128
            },
            ...
        ]
        deposits: Coin[]
        lends: Coin[]
        perps: [
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
        staked_astro_lps: Coin[]
        vaults: [
            {
                amount: {
                    unlocked: string
                } | {
                    locking: {
                        locked: string
                        unlocking: [
                            {
                                coin: Coin
                                id: number
                            },
                        ...
                        ]
                    }
                }
                vault: string
            },
            ...
        ]
    }
}
```
{% endcode %}

#### total\_debt\_shares

{% code title="Query message" %}
```typescript
{
    total_debt_shares: string
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        shares: Uint128
        denom: string
    }
}
```
{% endcode %}

#### vault\_bindings

{% code title="Query message" %}
```typescript
{
    vault_bindings: {
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
                account_id: string
                vault_address: string
            },
            ...
        ]
        metadata: {
            has_more: boolean
        }
    }
}
```
{% endcode %}

#### vault\_position\_value

{% code title="Query message" %}
```typescript
{
    vault_position_value: {
        vault_position: {
            amount: {
                unlocked: string
            } | {
                locking: {
                    locked: string
                    unlocking: [
                        {
                            coin: Coin
                            id: number
                        },
                    ...
                    ]
                }
            }
            vault: string
        }
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        base_coin: {
            amount: Uint128
            denom: string
            value: Uint128
        }
        vault_coin: {
            amount: Uint128
            denom: string
            value: Uint128
        }
    }
}
```
{% endcode %}

#### vault\_utilization

{% code title="Query message" %}
```typescript
{
    vault_utilization: {
        vault: string
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
          utilization: Coin
          vault: string
    }
}
```
{% endcode %}

### Methods

#### create\_credit\_account

{% code title="Execution message" %}
```typescript
{
    create_credit_account: AccountKind
}
```
{% endcode %}

#### execute\_trigger\_order

{% code title="Execution message" %}
```typescript
{
    execute_trigger_order: {
        account_id: string
        trigger_order_id: string
    }
}
```
{% endcode %}

#### repay\_from\_wallet

{% code title="Execution message" %}
```typescript
{
    repay_from_wallet: {
        account_id: string
    }
}
```
{% endcode %}

#### update\_balances\_after\_deleverage

{% code title="Execution message" %}
```typescript
{
    update_balance_after_deleverage: {
        account_id: string
        pnl:  'break_even' | { 
            profit: Coin
        } | {
            loss: Coin
        }
    }
}
```
{% endcode %}

#### update\_credit\_account

{% code title="Execution message" %}
```typescript
{
    update_credit_account: {
        account_id?: string | null
        account_kind?: AccountKind | null
        actions: Action[]
    }
}
```
{% endcode %}
