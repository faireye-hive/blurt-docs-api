````markdown
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

```shell
# Exemplo de Requisição
curl "[https://hivexplorer.com/api/get_block_header?block_num=8675309](https://hivexplorer.com/api/get_block_header?block_num=8675309)"
````

> O comando acima retorna um JSON estruturado assim:

```json
{
  "header": {
    "extensions": [],
    "previous": "00845fec1c00bd07264f68c1fc50e989b7ca0160",
    "timestamp": "2017-01-21T16:33:06",
    "transaction_merkle_root": "c034bfb36fe4401ce2a4d10f3e595a62be2eddd7",
    "witness": "pfunk"
  }
}
```

Retrieve a block header of the referenced block, or null if no matching block was found.

### HTTP Request

`GET /api/get_block_header`

### Query Parameters

Parameter | Description
\--------- | -----------
`block_num` (int) | Queries the block headers for a specific block number.

## get\_block

```shell
# Exemplo de Requisição
curl "[https://hivexplorer.com/api/get_block?block_num=8675309](https://hivexplorer.com/api/get_block?block_num=8675309)"
```

> O comando acima retorna um JSON estruturado assim:

```json
{
  "previous": "0000000000000000000000000000000000000000",
  "timestamp": "2016-03-24T16:05:00",
  "witness": "initminer",
  "transaction_merkle_root": "0000000000000000000000000000000000000000",
  "extensions": [],
  "witness_signature": "204f8ad56a8f5cf722a02b035a61b500aa59b9519b2c33c77a80c0a714680a5a5a7a340d909d19996613c5e4ae92146b9add8a7a663eef37d837ef881477313043",
  "transactions": [],
  "block_id": "0000000109833ce528d5bbfb3f6225b39ee10086",
  "signing_key": "STM8GC13uCZbP44HzMLV6zPZGwVQ8Nt4Kji8PapsPiNq1BK153XTX",
  "transaction_ids": []
}
```

Retrieve a full, signed block of the referenced block, or null if no matching block was found.

### HTTP Request

`GET /api/get_block`

### Query Parameters

Parameter | Description
\--------- | -----------
`block_num` (int) | Queries a specific block number.

## get\_block\_range

```shell
# Exemplo de Requisição
curl "[https://hivexplorer.com/api/get_block_range?starting_block_num=70548020&count=15](https://hivexplorer.com/api/get_block_range?starting_block_num=70548020&count=15)"
```

> O comando acima retorna um JSON estruturado assim:

```json
{
  "blocks": [
    {
      "previous": "04347a33f9155dc51c88601e782dcb86c4e5088b",
      "timestamp": "2022-12-15T13:46:54",
      "witness": "arcange",
      "transaction_merkle_root": "cba20a1395221712b10fd20c38de08e2a5759cbc",
      "extensions": [],
      "witness_signature": "20f491bcfff5854cbec6105633334ce89fabbd9e1dc03866dca27969e0375056392ea2ab87355ee85c13d261fc7cd2b52bf3278035ab8227f739091474e3a1480c",
      "transactions": [
        {
          "ref_block_num": 31282,
          "ref_block_prefix": 237252741,
          "expiration": "2022-12-15T13:47:18",
          "operations": [
            {
              "type": "custom_json_operation",
              "value": {
                "required_auths": [
                  "checkyzk"
                ],
                "required_posting_auths": [],
                "id": "sm_market_rent",
                "json": "{\"items\":[\"6ae699d473a4fa9613b83045192b879ceef58fdd-2\"],\"currency\":\"DEC\",\"days\":2,\"player\":\"dudoicon\"}"
              }
            }
          ],
          "extensions": [],
          "signatures": [
            "1f4ce4b443938051dbdc6f2042a78cd86876b2beb825d1dd1ec5f4fcd9e0d54fb00c50f641a37ef04973145496512aaf7417b4285a3e212c4171c18b3bc43aa699"
          ]
        }
      ],
      "block_id": "04347a34af5312512765bab3a2e40c8602254957",
      "signing_key": "STM6Z9ZtRoEXPqsMRTFqLopuL9jDg5gydcwkQEoWazg6uhGTkbYKM",
      "transaction_ids": [
        "b4a607f19e4fc9ffa9da11fbc2b65c7ad26671b9",
        "67c5ae6732f4fb383f6b41f30ee3d458410cb173",
        "767783b233f97401b8383f1af431573917a10161",
        "5fe0e855a9867776e9b3b438ba457b6d75796598"
      ]
    }
  ]
}
```

Retrieve a range of full, signed blocks. The list may be shorter than requested if count blocks would take you past the current head block.

### HTTP Request

`GET /api/get_block_range`

### Query Parameters

Parameter | Description
\--------- | -----------
`starting_block_num` (int) | Height of the first block to be returned
`count` (int) | The maximum number of blocks to return

# Condenser API

All calls in condenser\_api will return [] as the argument, as the array argument passing is opaque and implemented in the API calls themselves. They follow the current argument formatting. Existing apps should only need to skip using login\_api and send all of their calls to condenser\_api without any other changes required to use Appbase.

## get\_trending\_tags

```shell
# Exemplo de Requisição
curl "[https://hivexplorer.com/api/get_trending_tags?start_tag=%22aaa%22&limit=10](https://hivexplorer.com/api/get_trending_tags?start_tag=%22aaa%22&limit=10)"
```

> O comando acima retorna um JSON estruturado assim:

```json
[
  {
    "name": "",
    "total_payouts": "0.000 HBD",
    "net_votes": 0,
    "top_posts": 0,
    "comments": 0,
    "trending": ""
  }
]
```

Returns the list of trending tags.

### HTTP Request

`GET /api/get_trending_tags`

### Query Parameters

Parameter | Default | Description
\--------- | ------- | -----------
`tag` (string) | `null` | Queries the top trending tags.
`limit` (int) | 100 | Queries the tags after `tag`, up to `limit` tags.

## get\_chain\_properties

```shell
# Exemplo de Requisição
curl "[https://hivexplorer.com/api/get_chain_properties](https://hivexplorer.com/api/get_chain_properties)"
```

> O comando acima retorna um JSON estruturado assim:

```json
{
  "account_creation_fee": "3.000 HIVE",
  "maximum_block_size": 65536,
  "hbd_interest_rate": 2000,
  "account_subsidy_budget": 797,
  "account_subsidy_decay": 347321
}
```

Returns the chain properties.

### HTTP Request

`GET /api/get_chain_properties`

## get\_feed\_history

```shell
# Exemplo de Requisição
curl "[https://hivexplorer.com/api/get_feed_history](https://hivexplorer.com/api/get_feed_history)"
```

> O comando acima retorna um JSON estruturado assim:

```json
{
  "id": 0,
  "current_median_history": {
    "base": "0.405 HBD",
    "quote": "1.000 HIVE"
  },
  "market_median_history": {
    "base": "0.405 HBD",
    "quote": "1.000 HIVE"
  },
  "current_min_history": {
    "base": "0.397 HBD",
    "quote": "1.000 HIVE"
  },
  "current_max_history": {
    "base": "0.422 HBD",
    "quote": "1.000 HIVE"
  },
  "price_history": [
    {
      "base": "0.416 HBD",
      "quote": "1.000 HIVE"
    },
    {
      "base": "0.412 HBD",
      "quote": "1.000 HIVE"
    }
  ]
}
```

Returns the history of price feed values.

### HTTP Request

`GET /api/get_feed_history`

## get\_current\_median\_history\_price

```shell
# Exemplo de Requisição
curl "[https://hivexplorer.com/api/get_current_median_history_price](https://hivexplorer.com/api/get_current_median_history_price)"
```

> O comando acima retorna um JSON estruturado assim:

```json
{
  "base": "0.405 HBD",
  "quote": "1.000 HIVE"
}
```

Get current median market price.

### HTTP Request

`GET /api/get_current_median_history_price`

## get\_discussions\_by\_author\_before\_date

```shell
# Exemplo de Requisição
curl "[https://hivexplorer.com/api/get_discussions_by_author_before_date?author=%22ecency%22&permlink=%22ecency-development-and-maintenance-4%22&date=2023-11-04T22:49:43&limit=2](https://hivexplorer.com/api/get_discussions_by_author_before_date?author=%22ecency%22&permlink=%22ecency-development-and-maintenance-4%22&date=2023-11-04T22:49:43&limit=2)"
```

> O comando acima retorna um JSON estruturado assim:

```json
[
  {
    "active_votes": [
      {
        "percent": "4000",
        "reputation": 341233778618,
        "rshares": 768760982022,
        "voter": "boatymcboatface"
      }
    ],
    "author": "ecency",
    "author_reputation": 481129921188588,
    "beneficiaries": [],
    "body": "The #24 edition of the Monthly Guest Curation Program...",
    "body_length": 3797,
    "cashout_time": "1969-12-31T23:59:59",
    "category": "ecency",
    "children": 15,
    "created": "2023-10-30T09:45:54",
    "curator_payout_value": "8.845 HBD",
    "depth": 0,
    "json_metadata": "{\"image\":[\"[https://cdn.discordapp.com](https://cdn.discordapp.com)...\"],\"tags\":[\"ecency\",\"hive\",\"curation\",\"guestcurators\"],\"description\":\"\",\"app\":\"ecency/3.0.36-vision\",\"format\":\"markdown+html\",\"image_ratios\":[\"1.0000\"]}",
    "last_payout": "2023-11-06T09:45:54",
    "last_update": "2023-11-04T11:11:30",
    "max_accepted_payout": "1000000.000 HBD",
    "net_rshares": 37317216249639,
    "parent_author": "",
    "parent_permlink": "ecency",
    "pending_payout_value": "0.000 HBD",
    "percent_hbd": 10000,
    "permlink": "ecency-monthly-guest-curation-program-d34368ec623ec",
    "post_id": 128422803,
    "promoted": "0.000 HBD",
    "replies": [],
    "root_title": "Ecency Monthly Guest Curation Program #25",
    "title": "Ecency Monthly Guest Curation Program #25",
    "total_payout_value": "8.902 HBD",
    "url": "/ecency/@ecency/ecency-monthly-guest-curation-program-d34368ec623ec"
  }
]
```

condenser\_api.get\_discussions\_by\_author\_before\_date

### HTTP Request

`GET /api/get_discussions_by_author_before_date`

### Query Parameters

Parameter | Description
\--------- | -----------
`author` (string) | The author to query.
`permlink` (string) | The permlink to query.
`date` (string) | The date to query before (ISO format).
`limit` (int) | The number of results to return.

## get\_collateralized\_conversion\_requests

```shell
# Exemplo de Requisição
curl "[https://hivexplorer.com/api/get_collateralized_conversion_requests?account=%22hbdstabilizer%22](https://hivexplorer.com/api/get_collateralized_conversion_requests?account=%22hbdstabilizer%22)"
```

> O comando acima retorna um JSON estruturado assim:

```json
[]
```

Get HIVE to HBD (Collateralized) convert requests.

### HTTP Request

`GET /api/get_collateralized_conversion_requests`

### Query Parameters

Parameter | Description
\--------- | -----------
`account` (string) | The account to query requests for.

````

---

### O que eu fiz:

1.  **Mudei o Título:** Atualizei o `title` e a `description` no cabeçalho (YAML) para "Blurt API Reference".
2.  **Limpei a Introdução:** Removi as referências aos "Kittens" (gatinhos) e deixei uma introdução genérica.
3.  **Removi a Autenticação:** Removi a seção de autenticação dos gatinhos, já que seus endpoints não parecem usá-la.
4.  **Tradução para Markdown:** Peguei seu HTML para `Blocks` e `Condenser API` e o converti para o formato que o Slate usa:
    * `## Título` para cada endpoint.
    * ` ```shell ` para os exemplos de URL (que vão para a direita).
    * ` ```json ` para as respostas (que vão para a direita).
    * Tabelas Markdown para os parâmetros.
````
