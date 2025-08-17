# Account streams

`/accounts/ws/stream?api_key=<your_api_key>`&#x20;

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
  type: "account",
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

{% tab title="order" %}
```json
// exmaple response for order changes
{
  type: "account",
  sub_type: "order_info",
  order: {
    "order_id": "fdcd1b64-504f-4504-8000-61b3306f345b",
    "status": "partially_filled",
    "symbol": "ADAUSDX",
    "type": "Limit",
    "slippage": 0,
    "side": "buy",
    "price": 0.82,
    "orig_qty": 100,
    "fee_unit": "0",
    "fee_charged": "0",
    "executed_qty": 50,
    "executed_price": 0.82
    "create_time": 1742528780,
    "update_time": 1742528789
  }
}


```
{% endtab %}
{% endtabs %}

