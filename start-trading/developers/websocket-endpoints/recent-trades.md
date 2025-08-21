# Recent trades

`/market/recent-trade/:symbol?api_key=<your_api_key>`&#x20;

## This websocket will feed notifications for

* new trades for a specific trading pair

**Query params**

| Name     | Value             |
| -------- | ----------------- |
| api\_key | \<your\_api\_key> |

**Stream Response**

{% tabs %}
{% tab title="recent trades" %}
```json
[
  {
    "timestamp": "2025-08-21T03:43:00.204624Z",
    "symbol": "ADAUSDM",
    "side": "sell",
    "price": 0.7803,
    "amount": 4.6
  },
  {
    "timestamp": "2025-08-21T03:43:00.20169Z",
    "symbol": "ADAUSDM",
    "side": "buy",
    "price": 0.78,
    "amount": 5.4
  },
  {
    "timestamp": "2025-08-21T03:42:41.033791Z",
    "symbol": "ADAUSDM",
    "side": "buy",
    "price": 0.78,
    "amount": 10
  },
  {
    "timestamp": "2025-08-20T22:53:00.007111Z",
    "symbol": "ADAUSDM",
    "side": "sell",
    "price": 0.78,
    "amount": 4.6
  },
  {
    "timestamp": "2025-08-20T22:53:00.004846Z",
    "symbol": "ADAUSDM",
    "side": "buy",
    "price": 0.75,
    "amount": 5.4
  },
]
```
{% endtab %}
{% endtabs %}

