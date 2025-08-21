# Market depth streams

`/market/depth/:symbol?api_key=<your_api_key>`&#x20;

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
{
  "timestamp": 1755747950587,
  "bids": [
    {
      "price": 0.195,
      "quantity": 30
    }
  ],
  "asks": [
    {
      "price": 0.3495,
      "quantity": 50.65
    }
  ]
}


```
{% endtab %}
{% endtabs %}

