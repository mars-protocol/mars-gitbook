---
description: >-
  The Params Contract provides market, vault, and perp data. It is mandatory to
  whitelist and enable markets throughout the Mars Protocol ecosystem.
---

# Params

### Deployments

Neutron: [neutron1x4rgd7ry23v2n49y7xdzje0743c5tgrnqrqsvwyya2h6m48tz4jqqex06x](https://neutron.celat.one/neutron-1/contracts/neutron1x4rgd7ry23v2n49y7xdzje0743c5tgrnqrqsvwyya2h6m48tz4jqqex06x)

Osmosis: [osmo1nlmdxt9ctql2jr47qd4fpgzg84cjswxyw6q99u4y4u4q6c2f5ksq7ysent](https://osmosis.celat.one/osmosis-1/contracts/osmo1nlmdxt9ctql2jr47qd4fpgzg84cjswxyw6q99u4y4u4q6c2f5ksq7ysent)

***

### Types

The types of the Params Contract can be found [here](https://github.com/mars-protocol/core-contracts/blob/master/scripts/types/generated/mars-params/MarsParams.types.ts).

For reference on the Queries and Methods:

{% code title="Base Types" %}
```typescript
type Addr = string
type Decimal = string
type Uint128 = string
```
{% endcode %}

***

### Queries

#### ~~all\_asset\_params~~ (outdated)

Returns all asset params.

{% code title="Query message" %}
```typescript
{
    all_asset_params: {
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
            close_factor: Decimal
            credit_manager: {
                hls?: {
                    correlations: [
                        {
                            coin: {
                                denom: string
                            }
                        } | {
                            vault: {
                                addr: Addr
                            }
                        },
                        ...
                    ]
                    liquidation_threshold: Decimal
                    max_loan_to_value: Decimal
                } | null
                whitelisted: boolean
                withdraw_enabled: boolean
            }
            denom: string
            deposit_cap: Uint128
            liquidation_bonus: {
                max_lb: Decimal
                min_lb: Decimal
                slope: Decimal
                starting_lb: Decimal
            }
            liquidation_threshold: Decimal
            max_loan_to_value: Decimal
            protocol_liquidation_fee: Decimal
            red_bank: {
                borrow_enabled: boolean
                deposit_enabled: boolean
                withdraw_enabled: boolean
            }
        },
        ...
    ]
}
```
{% endcode %}

#### all\_asset\_params\_v2

{% code title="Query message" %}
```typescript
{
    all_asset_params_v2: {
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
                close_factor: Decimal
                credit_manager: {
                    hls?: {
                        correlations: [
                            {
                                coin: {
                                    denom: string
                                }
                            } | {
                                vault: {
                                    addr: Addr
                                }
                            },
                            ...
                        ]
                        liquidation_threshold: Decimal
                        max_loan_to_value: Decimal
                    } | null
                    whitelisted: boolean
                    withdraw_enabled: boolean
                }
                denom: string
                deposit_cap: Uint128
                liquidation_bonus: {
                    max_lb: Decimal
                    min_lb: Decimal
                    slope: Decimal
                    starting_lb: Decimal
                }
                liquidation_threshold: Decimal
                max_loan_to_value: Decimal
                protocol_liquidation_fee: Decimal
                red_bank: {
                    borrow_enabled: boolean
                    deposit_enabled: boolean
                    withdraw_enabled: boolean
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

#### ~~all\_perp\_params~~ (outdated)

{% code title="Query message" %}
```typescript
{
    all_perp_params: {
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
          closing_fee_rate: Decimal
          denom: string
          enabled: boolean
          liquidation_threshold: Decimal
          max_funding_velocity: Decimal
          max_loan_to_value: Decimal
          max_long_oi_value: Uint128
          max_net_oi_value: Uint128
          max_position_value?: Uint128 | null
          max_short_oi_value: Uint128
          min_position_value: Uint128
          opening_fee_rate: Decimal
          skew_scale: Uint128
    ]
}
```
{% endcode %}

#### all\_perp\_params\_v2

{% code title="Query message" %}
```typescript
{
    all_perp_params_v2: {
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
                closing_fee_rate: Decimal
                denom: string
                enabled: boolean
                liquidation_threshold: Decimal
                max_funding_velocity: Decimal
                max_loan_to_value: Decimal
                max_long_oi_value: Uint128
                max_net_oi_value: Uint128
                max_position_value?: Uint128 | null
                max_short_oi_value: Uint128
                min_position_value: Uint128
                opening_fee_rate: Decimal
                skew_scale: Uint128
          ]
          metadata: {
            has_more: boolean
        }
    }
}
```
{% endcode %}

#### all\_total\_deposits\_v2

{% code title="Query message" %}
```typescript
{
    all_total_deposits_v2: {
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
                  amount: Uint128
                  cap: Uint128
                  denom: string
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

#### ~~all\_vault\_configs~~ (outdated)

{% code title="Query message" %}
```typescript
{
    all_vault_configs: {
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
            addr: Addr
            deposit_cap: Coin
            hls?: {
                correlations: [
                    {
                        coin: {
                            denom: string
                        }
                    } | {
                        vault: {
                            addr: Addr
                        }
                    },
                    ...
                ]
                liquidation_threshold: Decimal
                max_loan_to_value: Decimal
            } | null
            liquidation_threshold: Decimal
            max_loan_to_value: Decimal
            whitelisted: boolean
        },
        ...
    ]
}
```
{% endcode %}

#### all\_vault\_configs\_v2

{% code title="Query message" %}
```typescript
{
    all_vault_configs_v2: {
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
                addr: Addr
                deposit_cap: Coin
                hls?: {
                    correlations: [
                        {
                            coin: {
                                denom: string
                            }
                        } | {
                            vault: {
                                addr: Addr
                            }
                        },
                        ...
                    ]
                    liquidation_threshold: Decimal
                    max_loan_to_value: Decimal
                } | null
                liquidation_threshold: Decimal
                max_loan_to_value: Decimal
                whitelisted: boolean
            },
            ...
        ],
        metadata: {
            has_more: boolean
        }
    }
}
```
{% endcode %}

#### asset\_params

{% code title="Query message" %}
```typescript
{
    asset_params: {
        denom: string
    }   
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        close_factor: Decimal
        credit_manager: {
            hls?: {
                correlations: [
                    {
                        coin: {
                            denom: string
                        }
                    } | {
                        vault: {
                            addr: Addr
                        }
                    },
                    ...
                ]
                liquidation_threshold: Decimal
                max_loan_to_value: Decimal
            } | null
            whitelisted: boolean
            withdraw_enabled: boolean
        }
        denom: string
        deposit_cap: Uint128
        liquidation_bonus: {
            max_lb: Decimal
            min_lb: Decimal
            slope: Decimal
            starting_lb: Decimal
        }
        liquidation_threshold: Decimal
        max_loan_to_value: Decimal
        protocol_liquidation_fee: Decimal
        red_bank: {
            borrow_enabled: boolean
            deposit_enabled: boolean
            withdraw_enabled: boolean
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
        address_provider: string
        max_perp_params: number
    }
}
```
{% endcode %}

#### managed\_vault\_config

{% code title="Query message" %}
```typescript
{
    managed_vault_config: {}
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        code_ids: number[]
        min_creation_fee_in_uusd: number
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

#### perp\_params

{% code title="Query message" %}
```typescript
{
    perp_params: {
        denom: string
    } 
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
          closing_fee_rate: Decimal
          denom: string
          enabled: boolean
          liquidation_threshold: Decimal
          max_funding_velocity: Decimal
          max_loan_to_value: Decimal
          max_long_oi_value: Uint128
          max_net_oi_value: Uint128
          max_position_value?: Uint128 | null
          max_short_oi_value: Uint128
          min_position_value: Uint128
          opening_fee_rate: Decimal
          skew_scale: Uint128
    }
}
```
{% endcode %}

#### risk\_manager

{% code title="Query message" %}
```typescript
{
    risk_manager: {}  
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

#### total\_deposit

{% code title="Query message" %}
```typescript
{
    total_deposit: {
        denom: string
    } 
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        amount: Uint128
        cap: Uint128
        denom: string
    }
}
```
{% endcode %}

#### vault\_config

{% code title="Query message" %}
```typescript
{
    vault_config: {
        address: string
    }
}
```
{% endcode %}

{% code title="Return output" %}
```typescript
{
    data: {
        addr: Addr
        deposit_cap: Coin
        hls?: {
            correlations: [
                {
                    coin: {
                        denom: string
                    }
                } | {
                    vault: {
                        addr: Addr
                    }
                },
                ...
            ]
            liquidation_threshold: Decimal
            max_loan_to_value: Decimal
        } | null
        liquidation_threshold: Decimal
        max_loan_to_value: Decimal
        whitelisted: boolean
    }
}
```
{% endcode %}

***

### Methods

Only the owner of the contract can call its methods. That's why they are not part of the documentation.
