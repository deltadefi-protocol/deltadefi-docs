# Market depth streams

`/market/ws/depth/:symbol?api_key=<your_api_key>`&#x20;

## This websocket will feed notifications for

* newly created orders that exists on the order book

**Query params**

| Name     | Value             |
| -------- | ----------------- |
| api\_key | \<your\_api\_key> |

**Stream Response**

{% tabs %}
{% tab title="market price" %}
```json
// exmaple response for market depth
{
  type: "Market",
  sub_type: "market_depth",
  side: "buy",
  price: "0.77",
  quantity: 120
}


```
{% endtab %}
{% endtabs %}

