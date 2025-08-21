# Market price streams

`/market/market-price/:symbol?api_key=<your_api_key>`&#x20;

## This websocket will feed notifications for

* Latest market-price (Last trade price)

**Query params**

| Name     | Value             |
| -------- | ----------------- |
| api\_key | \<your\_api\_key> |

**Stream Response**

{% tabs %}
{% tab title="market price" %}
```json
// exmaple response for market price
{
  type: "Market",
  sub_type: "market_price",
  price: 0.75
}


```
{% endtab %}
{% endtabs %}

