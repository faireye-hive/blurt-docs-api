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

|Parameter | Description|
|--------- | -----------|
|`author` (string) | The author to query.|
|`permlink` (string) | The permlink to query.|
|`date` (string) | The date to query before (ISO format).|
|`limit` (int) | The number of results to return.|

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