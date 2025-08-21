# Account streams

`/accounts/stream?api_key=<your_api_key>`&#x20;

## This websocket will feed notifications for

* account balances updates
* orders updates

**Query params**

| Name     | Value             |
| -------- | ----------------- |
| api\_key | \<your\_api\_key> |

**Stream Response**

{% tabs %}
{% tab title="balance" %}
```json
// exmaple response for ADA balance changes
{
  type: "Account",
  sub_type: "balance",
  balance: [
    {
        "asset": "usdx",
        "asset_unit": "5066154a102ee037390c5236f78db23239b49c5748d3d349f3ccf04b55534458",
        "free": 1153.006812,
        "locked": 0
    },
    {
        "asset": "ada",
        "asset_unit": "",
        "free": 1383.52097,
        "locked": 0
    }
  ]
}


```
{% endtab %}

{% tab title="open_orders" %}
```json
// exmaple response for order changes
{
  "type": "Account",
  "sub_type": "open_orders",
  "data": [
    {
      "orders": [
        {
          "order_id": "331ba963-dcd6-4215-b1a0-c6f1253f4838",
          "status": "open",
          "symbol": "ADAUSDM",
          "orig_qty": "10",
          "executed_qty": "0",
          "side": "buy",
          "price": 0.68,
          "type": "limit",
          "fee_charged": "0",
          "fee_unit": "lovelace",
          "executed_price": 0,
          "slippage": "0",
          "create_time": 1755747489,
          "update_time": 1755747490
        }
      ],
      "order_filling_records": []
    }
  ],
  "total_count": 1,
  "total_page": 1
}


```
{% endtab %}

{% tab title="trading_history" %}
```json
// exmaple response for order changes
{
  "type": "Account",
  "sub_type": "trading_history",
  "data": [
    {
      "orders": [
        {
          "order_id": "632a9057-3450-4758-b955-65a78e72ac19",
          "status": "fully_filled",
          "symbol": "ADAUSDM",
          "orig_qty": "10",
          "executed_qty": "10",
          "side": "buy",
          "price": 0.78,
          "type": "market",
          "fee_charged": "0.02",
          "fee_unit": "lovelace",
          "executed_price": 0.78,
          "slippage": "118205",
          "create_time": 1755747760,
          "update_time": 1755747761,
          "fills": [
            {
              "id": "90af3400-458e-47c8-b232-7157c200c0a7",
              "order_id": "632a9057-3450-4758-b955-65a78e72ac19",
              "execution_price": 0.78,
              "filled_amount": "10",
              "fee_unit": "lovelace",
              "fee_amount": "0.02",
              "role": "taker",
              "counter_party_order_id": "f6897f1e-61ee-4dd5-bb9e-2f210a216fff",
              "create_time": 1755747761
            }
          ]
        }
      ],
      "order_filling_records": []
    }
  ],
  "total_count": 2,
  "total_page": 1
}
```
{% endtab %}

{% tab title="orders_history" %}
```json
// exmaple response for order changes
{
  "type": "Account",
  "sub_type": "orders_history",
  "data": [
    {
      "orders": [
        {
          "order_id": "331ba963-dcd6-4215-b1a0-c6f1253f4838",
          "status": "cancelled",
          "symbol": "ADAUSDM",
          "orig_qty": "10",
          "executed_qty": "0",
          "side": "buy",
          "price": 0.68,
          "type": "limit",
          "fee_charged": "0",
          "fee_unit": "lovelace",
          "executed_price": 0,
          "slippage": "0",
          "create_time": 1755747489,
          "update_time": 1755747662
        }
      ],
      "order_filling_records": []
    }
  ],
  "total_count": 1,
  "total_page": 1
}
```
{% endtab %}
{% endtabs %}

