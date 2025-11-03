---
title: Blurt API Reference

language_tabs: # Idiomas que aparecerão nas abas de código
  - shell

toc_footers:
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentação para a API da Blurt Blockchain
---

# Introduction

Bem-vindo à documentação da API da Blurt! Você pode usar nossa API para acessar os endpoints da blockchain da Blurt.

Os exemplos de código estão na área escura à direita.

# Blocks

Used to query values related to the block plugin. These AppBase API methods are still under development and subject to change.

## get_block_header

Retrieve a block header of the referenced block, or null if no matching block was found.

### Query Parameters

| Parameter         | Description                                            |
| ----------------- | ------------------------------------------------------ |
| `block_num` (int) | Queries the block headers for a specific block number. |

```shell
# Exemplo de Requisição
curl -s --data '{"jsonrpc":"2.0", "method":"block_api.get_block_header", "params":{"block_num":8675309}, "id":1}' https://rpc.blurt.world
```

> O comando acima retorna um JSON estruturado assim:

```json
{
  "jsonrpc": "2.0",
  "result": {
    "header": {
      "previous": "00845fec025ede5178d189f904b7eec417d21227",
      "timestamp": "2021-05-07T04:21:15",
      "witness": "blurthispano",
      "transaction_merkle_root": "0000000000000000000000000000000000000000",
      "extensions": [
        {
          "type": "fee_info",
          "value": { "operation_flat_fee": 1, "bandwidth_kbytes_fee": 150 }
        }
      ]
    }
  },
  "id": 1
}
```

## get_block

Retrieve a full, signed block of the referenced block, or null if no matching block was found.

### Query Parameters

| Parameter         | Description                      |
| ----------------- | -------------------------------- |
| `block_num` (int) | Queries a specific block number. |

```shell
# Exemplo de Requisição
curl -s --data '{"jsonrpc":"2.0", "method":"block_api.get_block", "params":{"block_num":8675309}, "id":1}' https://rpc.blurt.world
```

> O comando acima retorna um JSON estruturado assim:

```json
{
  "jsonrpc": "2.0",
  "result": {
    "block": {
      "previous": "00845fec025ede5178d189f904b7eec417d21227",
      "timestamp": "2021-05-07T04:21:15",
      "witness": "blurthispano",
      "transaction_merkle_root": "0000000000000000000000000000000000000000",
      "extensions": [
        {
          "type": "fee_info",
          "value": { "operation_flat_fee": 1, "bandwidth_kbytes_fee": 150 }
        }
      ],
      "witness_signature": "20e8e29ff76df5cca9223644c36ae8da54be2820fdf18ce3397119b05fc77c95d85f1cab89fc47cde620fa01e1f395cfb2e314d06175088801e442c82c08c7da59",
      "transactions": [],
      "block_id": "00845fed151ce8e36159d9e2360303b1247a4515",
      "signing_key": "BLT5wqzRhKp6y5ea1b8uW8TsK87owrbBT95Ww8DUEtbdS7PhLeUVd",
      "transaction_ids": []
    }
  },
  "id": 1
}
```

# Condenser API

All calls in condenser_api will return [] as the argument, as the array argument passing is opaque and implemented in the API calls themselves. They follow the current argument formatting. Existing apps should only need to skip using login_api and send all of their calls to condenser_api without any other changes required to use Appbase.

## get_trending_tags

### Query Parameters

| Parameter      | Default | Description                                       |
| -------------- | ------- | ------------------------------------------------- |
| `tag` (string) | `null`  | Queries the top trending tags.                    |
| `limit` (int)  | 100     | Queries the tags after `tag`, up to `limit` tags. |

```shell
# Exemplo de Requisição
curl -s --data '{"jsonrpc":"2.0", "method":"condenser_api.get_trending_tags", "params":["blurt",1], "id":1}' https://rpc.blurt.world
```

Returns the list of trending tags.

> O comando acima retorna um JSON estruturado assim:

```json
{
  "jsonrpc": "2.0",
  "result": [
    {
      "name": "rewards",
      "comments": 396,
      "top_posts": 7,
      "total_payouts": "74661.630 BLURT"
    },
    {
      "name": "kr",
      "comments": 44,
      "top_posts": 96,
      "total_payouts": "32423.738 BLURT"
    },
    {
      "name": "blurt",
      "comments": 68,
      "top_posts": 96,
      "total_payouts": "27303.856 BLURT"
    }
  ],
  "id": 1
}
```

## get_chain_properties

```shell
# Exemplo de Requisição
curl -s --data '{"jsonrpc":"2.0", "method":"condenser_api.get_chain_properties", "params":[], "id":1}' https://rpc.blurt.world
```

Returns the chain properties.

> O comando acima retorna um JSON estruturado assim:

```json
{
  "jsonrpc": "2.0",
  "result": {
    "account_creation_fee": "100.000 BLURT",
    "maximum_block_size": 65536,
    "account_subsidy_budget": 797,
    "account_subsidy_decay": 347321,
    "operation_flat_fee": "0.050 BLURT",
    "bandwidth_kbytes_fee": "0.200 BLURT",
    "proposal_fee": "1000.000 BLURT"
  },
  "id": 1
}
```

## get_discussions_by_author_before_date

### Query Parameters

| Parameter           | Description                            |
| ------------------- | -------------------------------------- |
| `author` (string)   | The author to query.                   |
| `permlink` (string) | The permlink to query.                 |
| `date` (string)     | The date to query before (ISO format). |
| `limit` (int)       | The number of results to return.       |

```shell
# Exemplo de Requisição
curl -s --data '{"jsonrpc":"2.0", "method":"condenser_api.get_discussions_by_author_before_date", "params":["hiveio","firstpost","2025-04-19T22:49:43",1], "id":1}' https://api.hive.blog
```

> O comando acima retorna um JSON estruturado assim:

```json
{
  "jsonrpc": "2.0",
  "result": [
    {
      "post_id": 1837728,
      "author": "hellobot",
      "permlink": "2025-11-02",
      "category": "hellobot",
      "title": "Current day: 2025-11-02",
      "body": "Aloha!\n## Blurt Statistics\n- **New Accounts**: 2\n- **New Votes**: 4452\n- **New Articles**: 298\n- **New Comments**: 303\n- **Welcome to new users:** @karphiy, @jompiy\n## Special dates\n- **The time remaining until the new year**: 61 days remaining\n- **Time for summer holidays**: 242 days remaining\n- **Time for Santa Claus**: 35 days remaining\n## Blurt's DApps\n- [BlurtLatam](//blurtlatam.intinte.org): Alternative to Blurt.blog uncensored interface\n- [BlurtCreator](//blurtcreator.intinte.org): Free account creator for Blurt Blockchain\n- [Swap Pools](//beeswap.dcity.io/pools?search=blurt): Earn from providing liquidity and support Blurt's security\n- [Khrom's Tutorials](//blurt.pl): Gain knowledge about Blurt from Khrom user guides",
      "json_metadata": "{\"tags\":[\"hellobot\"]}",
      "created": "2025-11-01T23:05:09",
      "last_update": "2025-11-01T23:05:09",
      "depth": 0,
      "children": 0,
      "net_rshares": 1651741638,
      "last_payout": "1969-12-31T23:59:59",
      "cashout_time": "2025-11-08T23:05:09",
      "total_payout_value": "0.000 BLURT",
      "curator_payout_value": "0.000 BLURT",
      "pending_payout_value": "3.271 BLURT",
      "promoted": "0.000 BLURT",
      "replies": [],
      "body_length": 734,
      "active_votes": [
        { "voter": "fervi", "rshares": "151518960", "percent": "10000" },
        { "voter": "hellobot", "rshares": "193065359", "percent": "10000" },
        { "voter": "marendan", "rshares": "151225551", "percent": "10000" },
        { "voter": "blurtpowerbot", "rshares": "1155931768", "percent": "149" }
      ],
      "parent_author": "",
      "parent_permlink": "hellobot",
      "url": "/hellobot/@hellobot/2025-11-02",
      "root_title": "Current day: 2025-11-02",
      "beneficiaries": [],
      "max_accepted_payout": "1000000.000 BLURT",
      "percent_blurt": 10000
    }
  ],
  "id": 1
}
```

## broadcast_transaction

Used to broadcast a transaction.

### Require Parameters

| Parameter                 | Description                                       |
| ------------------------- | ------------------------------------------------- |
| signatures (array/string) | Need a valid signatures(hash)                     |
| expiration (string/data)  | Future data expiration                            |
| ref_block_num (int)       | Need get a valid ref_block_num                    |
| ref_block_prefix (int)    | Need get from blockchain a valid ref_block_prefix |
| operations (array)        |                                                   |

example operations:
["vote",{"voter":"hiveio","author":"alice","permlink":"a-post-by-alice","weight":10000}]
['transfer', { from, to, amount, memo }]
['account_update', {account,owner,active,posting,memo_key ,json_metadata ,posting_json_metadata}] 'Public keys'
...

```shell
# Exemplo de Requisição
curl -s --data '{"jsonrpc":"2.0", "method":"condenser_api.broadcast_transaction", "params":[{"ref_block_num":1097,"ref_block_prefix":2181793527,"expiration":"2025-11-03T02:55:21","operations":[["vote",{"voter":"hiveio","author":"alice","permlink":"a-post-by-alice","weight":10000}]],"extensions":[],"signatures":[]}], "id":1}' https://rpc.blurt.blog
```

> O comando acima retorna um JSON estruturado assim:

```json
{}
```

## broadcast_transaction_synchronous

Used to broadcast a transaction and waits for it to be processed synchronously.

### Require Parameters

| Parameter                 | Description                                       |
| ------------------------- | ------------------------------------------------- |
| signatures (array/string) | Need a valid signatures(hash)                     |
| expiration (string/data)  | Future data expiration                            |
| ref_block_num (int)       | Need get a valid ref_block_num                    |
| ref_block_prefix (int)    | Need get from blockchain a valid ref_block_prefix |
| operations (array)        |                                                   |

example operations:
["vote",{"voter":"hiveio","author":"alice","permlink":"a-post-by-alice","weight":10000}]
['transfer', { from, to, amount, memo }]
['account_update', {account,owner,active,posting,memo_key ,json_metadata ,posting_json_metadata}] 'Public keys'
...

```shell
# Exemplo de Requisição
curl -s --data '{"jsonrpc":"2.0", "method":"condenser_api.broadcast_transaction", "params":[{"ref_block_num":1097,"ref_block_prefix":2181793527,"expiration":"2025-11-03T02:55:21","operations":[["vote",{"voter":"hiveio","author":"alice","permlink":"a-post-by-alice","weight":10000}]],"extensions":[],"signatures":[]}], "id":1}' https://rpc.blurt.blog
```

> O comando acima retorna um JSON estruturado assim:

```json
{}
```

## get_account_count

Returns the number of accounts.

```shell
# Exemplo de Requisição
curl -s --data '{"jsonrpc":"2.0", "method":"condenser_api.get_account_count", "params":[], "id":1}' https://rpc.blurt.world
```

> O comando acima retorna um JSON estruturado assim:

```json
{ "jsonrpc": "2.0", "result": 1398633, "id": 1 }
```

## get_account_history

Returns a history of all operations for a given account. Parameters:

### Query Parameters

| Nome | O que faz | Exemplo |
|------|------------|----------|
| `account` | Nome da conta | `"bgo"` |
| `start` | Onde começar (`-1` = novo, `1000` = antigo) | `-1` |
| `limit` | Quantos mostrar (máx. `1000`) | `1000` |
| `operation_filter_low` | Tipo de ação:<br>• vazio = tudo<br>• `1` = votos<br>• `262144` = mensagens<br>• `0, 1` = pagamentos | `1` |

---

## 💡 Exemplos

```js
["bgo", -1, 1000]          // tudo
["bgo", -1, 1000, 1]       // só votos
["bgo", -1, 1000, 262144]  // só mensagens
["bgo", -1, 1000, 0, 1]    // só pagamentos
```

```shell
# Exemplo de Requisição
curl -s --data '{"jsonrpc":"2.0", "method":"condenser_api.get_account_history", "params":["bgo", -1, 2], "id":1}'  https://rpc.blurt.world
```

> O comando acima retorna um JSON estruturado assim:

```json
{
  "jsonrpc": "2.0",
  "result": [
    [
      5158,
      {
        "trx_id": "d833294550cc1b540bb9be95771e4bbd4120bcdd",
        "block": 54747550,
        "trx_in_block": 0,
        "op_in_trx": 0,
        "virtual_op": 0,
        "timestamp": "2025-11-02T23:12:09",
        "op": [
          "vote",
          {
            "voter": "bgo",
            "author": "pichat",
            "permlink": "zcash-soars-while-bitcoin-freezes-is-liquidity-flowing-the-other-way-1762042557167",
            "weight": 10000
          }
        ]
      }
    ],
    [
      5160,
      {
        "trx_id": "1782ec37014b95a4b6446a666b797c90e6ad9fbc",
        "block": 54747560,
        "trx_in_block": 0,
        "op_in_trx": 0,
        "virtual_op": 0,
        "timestamp": "2025-11-02T23:12:39",
        "op": [
          "vote",
          {
            "voter": "bgo",
            "author": "amani2765",
            "permlink": "5zsa16-using-cypherflow-ai-with-pay-as-you-go-models",
            "weight": 10000
          }
        ]
      }
    ]
  ],
  "id": 1
}
```

## get_accounts

Returns accounts, queried by name. Parameters: account:string array; delayed_votes_active:boolean

### Query Parameters

| account (string array) |                                                  |
| ---------------------- | ------------------------------------------------ |
| ["bgo", "hellobot"]    | Queries for accounts named “hiveio” and “alice”. |

Or more accounts...

```shell
# Exemplo de Requisição
curl -s --data '{"jsonrpc":"2.0", "method":"condenser_api.get_accounts", "params":[["bgo", "hellobot"]], "id":1}' https://rpc.blurt.world
```

> O comando acima retorna um JSON estruturado assim:

```json
{
  "jsonrpc": "2.0",
  "result": [
    {
      "id": 1391955,
      "name": "bgo",
      "owner": {
        "weight_threshold": 1,
        "account_auths": [],
        "key_auths": [
          ["BLT8g31Ex2n1oJZNAkawhwKqiwVNAzBk73q2UoJgu6b1Ge92PphSE", 1]
        ]
      },
      "active": {
        "weight_threshold": 1,
        "account_auths": [],
        "key_auths": [
          ["BLT5QixVjadKTjA7aDpXvkwneVH3YzejdRvV6XSpGpmViM1mpEtf4", 1]
        ]
      },
      "posting": {
        "weight_threshold": 1,
        "account_auths": [],
        "key_auths": [
          ["BLT6rgd5LiUc7YRHevacoUH5BBkDokgxRw67mLCFHwSDP9mzCwSVh", 1]
        ]
      },
      "memo_key": "BLT7NqRhs5hGNGwHQKD5x2eT4h4G6s5dZewhApH1Y24xrfLiADVEE",
      "json_metadata": "{\"profile\":{\"profile_image\":\"https://img.blurt.world/blurtimage/bgo/d16c3f05cd38e0063077501cf1b29a940ea9a352.png\",\"name\":\"BGO\"}}",
      "posting_json_metadata": "",
      "proxy": "",
      "last_owner_update": "1970-01-01T00:00:00",
      "last_account_update": "2025-10-19T20:36:51",
      "created": "2021-07-11T04:15:30",
      "mined": false,
      "recovery_account": "sm-silva",
      "last_account_recovery": "1970-01-01T00:00:00",
      "reset_account": "null",
      "comment_count": 0,
      "lifetime_vote_count": 0,
      "post_count": 312,
      "can_vote": true,
      "voting_manabar": {
        "current_mana": "81369347882",
        "last_update_time": 1762125159
      },
      "voting_power": 8178,
      "balance": "740.351 BLURT",
      "savings_balance": "0.000 BLURT",
      "savings_withdraw_requests": 0,
      "reward_blurt_balance": "0.445 BLURT",
      "reward_vesting_balance": "5.091061 VESTS",
      "reward_vesting_blurt": "5.754 BLURT",
      "vesting_shares": "99363.782798 VESTS",
      "delegated_vesting_shares": "0.000000 VESTS",
      "received_vesting_shares": "125.534391 VESTS",
      "vesting_withdraw_rate": "0.000000 VESTS",
      "next_vesting_withdrawal": "1969-12-31T23:59:59",
      "withdrawn": 0,
      "to_withdraw": 0,
      "withdraw_routes": 0,
      "curation_rewards": 1722106,
      "posting_rewards": 8406596,
      "proxied_vsf_votes": [0, 0, 0, 0],
      "witnesses_voted_for": 0,
      "last_post": "2025-11-01T21:19:24",
      "last_root_post": "2025-11-01T14:04:48",
      "last_vote_time": "2025-11-02T23:12:39",
      "post_bandwidth": 0,
      "pending_claimed_accounts": 0,
      "vesting_balance": "0.000 BLURT",
      "transfer_history": [],
      "market_history": [],
      "post_history": [],
      "vote_history": [],
      "other_history": [],
      "witness_votes": [],
      "tags_usage": [],
      "guest_bloggers": []
    },
    {
      "id": 503019,
      "name": "hellobot",
      "owner": {
        "weight_threshold": 1,
        "account_auths": [],
        "key_auths": [
          ["BLT4x8H1Ymb1Kf7WFxVYpUpStotMykjuRAVpg4KoBqQVQfEtHCSZy", 1]
        ]
      },
      "active": {
        "weight_threshold": 1,
        "account_auths": [],
        "key_auths": [
          ["BLT8CPPHdfFYfGf9mDojyQ3KduNDa2Q899WZVNJC4bSt5wAJgf39y", 1]
        ]
      },
      "posting": {
        "weight_threshold": 1,
        "account_auths": [],
        "key_auths": [
          ["BLT7EpgLTegNPEfkCRK7tBjoAV773y7KYKrPqp1bpidSwcHqBGop9", 1]
        ]
      },
      "memo_key": "BLT7TUtCBiBKeVrV1pbygyn8sRyXJ689j5v58QH8Axt6BDSjEPReY",
      "json_metadata": "",
      "posting_json_metadata": "",
      "proxy": "",
      "last_owner_update": "1970-01-01T00:00:00",
      "last_account_update": "1970-01-01T00:00:00",
      "created": "1970-01-01T00:00:00",
      "mined": true,
      "recovery_account": "",
      "last_account_recovery": "1970-01-01T00:00:00",
      "reset_account": "null",
      "comment_count": 0,
      "lifetime_vote_count": 0,
      "post_count": 1050,
      "can_vote": true,
      "voting_manabar": {
        "current_mana": "9208619537",
        "last_update_time": 1762124709
      },
      "voting_power": 6185,
      "balance": "23.322 BLURT",
      "savings_balance": "0.000 BLURT",
      "savings_withdraw_requests": 0,
      "reward_blurt_balance": "10.128 BLURT",
      "reward_vesting_balance": "53.479118 VESTS",
      "reward_vesting_blurt": "60.426 BLURT",
      "vesting_shares": "14888.154316 VESTS",
      "delegated_vesting_shares": "0.000000 VESTS",
      "received_vesting_shares": "0.000000 VESTS",
      "vesting_withdraw_rate": "0.000000 VESTS",
      "next_vesting_withdrawal": "1969-12-31T23:59:59",
      "withdrawn": 132731000,
      "to_withdraw": 132731000,
      "withdraw_routes": 0,
      "curation_rewards": 1249911,
      "posting_rewards": 7780779,
      "proxied_vsf_votes": [0, 0, 0, 0],
      "witnesses_voted_for": 0,
      "last_post": "2025-11-02T23:05:09",
      "last_root_post": "2025-11-02T23:05:09",
      "last_vote_time": "2025-11-02T23:05:09",
      "post_bandwidth": 0,
      "pending_claimed_accounts": 0,
      "vesting_balance": "0.000 BLURT",
      "transfer_history": [],
      "market_history": [],
      "post_history": [],
      "vote_history": [],
      "other_history": [],
      "witness_votes": [],
      "tags_usage": [],
      "guest_bloggers": []
    }
  ],
  "id": 1
}
```
