# Account streams

Real-time WebSocket stream for account-related updates including balances, orders, and points.

## Connection

```
wss://api.deltadefi.io/accounts/stream?api_key=<your_api_key>
```

**Query Parameters**

| Name     | Type   | Required | Description  |
| -------- | ------ | -------- | ------------ |
| api\_key | string | Yes      | Your API key |

***

## Event Types

This WebSocket stream provides the following event types:

| Event Type | Sub Type      | Description                                                         |
| ---------- | ------------- | ------------------------------------------------------------------- |
| Account    | `balance`     | Account balance updates when deposits, withdrawals, or trades occur |
| Account    | `order_info`  | Real-time order status updates (new orders, fills, cancellations)   |
| Account    | `dlta_points` | Points/rewards updates when you earn DLTA points                    |

***

## Event Formats

{% tabs %}
{% tab title="order_info" %}
Real-time order updates. Sent whenever an order status changes (created, partially filled, fully filled, cancelled).

```json
{
  "type": "Account",
  "sub_type": "order_info",
  "order": {
    "id": "550e8400-e29b-41d4-a716-446655440000",
    "account_id": "550e8400-e29b-41d4-a716-446655440001",
    "status": "open",
    "symbol": "ADAUSDM",
    "base_qty": "100.00",
    "quote_qty": "93.00",
    "side": "buy",
    "price": "0.93",
    "type": "limit",
    "locked_base_qty": "100.00",
    "locked_quote_qty": "93.00",
    "executed_base_qty": "0",
    "executed_quote_qty": "0",
    "ob_open_order_base_qty": "100.00",
    "commission_unit": "lovelace",
    "commission": "0",
    "commission_rate_bp": 10,
    "executed_price": "0",
    "created_at": "2024-01-01T00:00:00Z",
    "updated_at": "2024-01-01T00:00:00Z",
    "order_execution_records": []
  }
}
```

**Order Status Values:**

* `building` - Order is being built
* `processing` - Order is being processed
* `open` - Order is active on the order book
* `closed` - Order is fully filled
* `failed` - Order failed
* `cancelled` - Order was cancelled
{% endtab %}

{% tab title="dlta_points" %}
Points updates when you earn DLTA rewards from trading activity.

```json
{
  "type": "Account",
  "sub_type": "dlta_points",
  "dlta_points": {
    "delta": "150",
    "new_total": "15150",
    "season_points": "5150",
    "source_type": "trade",
    "source_ref": "550e8400-e29b-41d4-a716-446655440000",
    "league": "gold"
  }
}
```

**Fields:**

| Field          | Type   | Description                                                            |
| -------------- | ------ | ---------------------------------------------------------------------- |
| delta          | string | Points earned in this update                                           |
| new\_total     | string | New total points balance                                               |
| season\_points | string | Points earned this season                                              |
| source\_type   | string | Source of points: `trade`, `referral`, `bonus`                         |
| source\_ref    | string | Reference ID (e.g., order ID for trades)                               |
| league         | string | Current league tier: `bronze`, `silver`, `gold`, `platinum`, `diamond` |
{% endtab %}

{% tab title="balance" %}
Account balance updates when deposits, withdrawals, or trades occur.

```json
{
  "type": "Account",
  "sub_type": "balance",
  "balance": [
    {
      "asset": "usdm",
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

**Fields:**

| Field       | Type   | Description                         |
| ----------- | ------ | ----------------------------------- |
| asset       | string | Asset symbol (e.g., `ada`, `usdm`)  |
| asset\_unit | string | On-chain asset unit (empty for ADA) |
| free        | number | Available balance for trading       |
| locked      | number | Balance locked in open orders       |
{% endtab %}
{% endtabs %}

***

## Connection Example

{% tabs %}
{% tab title="JavaScript" %}
```javascript
const WebSocket = require('ws');

const ws = new WebSocket('wss://api.deltadefi.io/accounts/stream?api_key=<your_api_key>');

ws.on('open', function open() {
  console.log('Connected to account stream');
});

ws.on('message', function message(data) {
  const event = JSON.parse(data);
  
  switch (event.sub_type) {
    case 'order_info':
      console.log('Order update:', event.order);
      break;
    case 'dlta_points':
      console.log('Points earned:', event.dlta_points.delta);
      break;
    case 'balance':
      console.log('Balance update:', event.balance);
      break;
    default:
      console.log('Event:', event);
  }
});

ws.on('close', function close() {
  console.log('Disconnected from account stream');
});

ws.on('error', function error(err) {
  console.error('WebSocket error:', err);
});
```
{% endtab %}

{% tab title="Python" %}
```python
import websocket
import json

def on_message(ws, message):
    event = json.loads(message)
    
    if event.get('sub_type') == 'order_info':
        print(f"Order update: {event['order']}")
    elif event.get('sub_type') == 'dlta_points':
        print(f"Points earned: {event['dlta_points']['delta']}")
    elif event.get('sub_type') == 'balance':
        print(f"Balance update: {event['balance']}")
    else:
        print(f"Event: {event}")

def on_error(ws, error):
    print(f"Error: {error}")

def on_close(ws, close_status_code, close_msg):
    print("Connection closed")

def on_open(ws):
    print("Connected to account stream")

ws = websocket.WebSocketApp(
    "wss://api.deltadefi.io/accounts/stream?api_key=<your_api_key>",
    on_open=on_open,
    on_message=on_message,
    on_error=on_error,
    on_close=on_close
)

ws.run_forever()
```
{% endtab %}

{% tab title="Go" %}
```go
package main

import (
    "encoding/json"
    "fmt"
    "log"

    "github.com/gorilla/websocket"
)

type Event struct {
    Type      string          `json:"type"`
    SubType   string          `json:"sub_type"`
    Order     json.RawMessage `json:"order,omitempty"`
    DltaPoints json.RawMessage `json:"dlta_points,omitempty"`
    Balance   json.RawMessage `json:"balance,omitempty"`
}

func main() {
    url := "wss://api.deltadefi.io/accounts/stream?api_key=<your_api_key>"
    
    c, _, err := websocket.DefaultDialer.Dial(url, nil)
    if err != nil {
        log.Fatal("dial:", err)
    }
    defer c.Close()

    fmt.Println("Connected to account stream")

    for {
        _, message, err := c.ReadMessage()
        if err != nil {
            log.Println("read:", err)
            return
        }

        var event Event
        json.Unmarshal(message, &event)

        switch event.SubType {
        case "order_info":
            fmt.Printf("Order update: %s\n", event.Order)
        case "dlta_points":
            fmt.Printf("Points update: %s\n", event.DltaPoints)
        case "balance":
            fmt.Printf("Balance update: %s\n", event.Balance)
        default:
            fmt.Printf("Event: %s\n", message)
        }
    }
}
```
{% endtab %}
{% endtabs %}

***

## Related

* [Market Price Streams](market-price-streams.md)
* [Market Depth Streams](market-depth-streams.md)
* [Recent Trades](recent-trades.md)
