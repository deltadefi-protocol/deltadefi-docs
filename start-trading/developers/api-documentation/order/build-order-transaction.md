# Build order transaction

Build a new order transaction. This endpoint creates an unsigned transaction that must be signed and submitted via the [Submit Order Transaction](submit-order-transaction.md) endpoint.

***

{% openapi-operation spec="V13" path="/orders/build" method="post" %}
[OpenAPI V13](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/146df47964f80e2dc987856ffff1fb5c47812bac51e24beb8afdb298326dded0.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260113%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260113T063932Z&X-Amz-Expires=172800&X-Amz-Signature=30f95348ddd7569d7df5bc57296e57d26645478e13c38ca3ac15958addd02169&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

## Request Parameters

| Parameter                   | Type    | Required    | Description                                                                                         |
| --------------------------- | ------- | ----------- | --------------------------------------------------------------------------------------------------- |
| symbol                      | string  | Yes         | Trading pair symbol (e.g., `ADAUSDM`)                                                               |
| side                        | string  | Yes         | Order side: `buy` or `sell`                                                                         |
| type                        | string  | Yes         | Order type: `limit` or `market`                                                                     |
| base\_quantity              | string  | Conditional | Quantity in base asset (e.g., ADA). **Use either `base_quantity` OR `quote_quantity`, not both.**   |
| quote\_quantity             | string  | Conditional | Quantity in quote asset (e.g., USDM). **Use either `base_quantity` OR `quote_quantity`, not both.** |
| price                       | string  | Conditional | Order price. **Required for limit orders, ignored for market orders.**                              |
| max\_slippage\_basis\_point | string  | No          | Maximum slippage in basis points. **Only applicable for market orders.**                            |
| post\_only                  | boolean | No          | If `true`, order only posts if it doesn't match immediately. **Only applicable for limit orders.**  |

***

## Order Types

### Limit Order

A limit order is placed at a specific price. It will only execute at that price or better.

**Required parameters:**

* `symbol`, `side`, `type` (set to `limit`)
* `price` - The limit price
* Either `base_quantity` or `quote_quantity`

**Optional parameters:**

* `post_only` - Set to `true` to ensure the order only acts as a maker (adds liquidity). If it would match immediately, the order is rejected.

### Market Order

A market order executes immediately at the best available price. No price is specified.

**Required parameters:**

* `symbol`, `side`, `type` (set to `market`)
* Either `base_quantity` or `quote_quantity`

**Optional parameters:**

* `max_slippage_basis_point` - Maximum acceptable slippage (1 basis point = 0.01%). If not set, unlimited slippage is allowed.

{% hint style="warning" %}
**Market Order Slippage:** If `max_slippage_basis_point` is not set, the market order will fill at any price until the order is complete or your balance is exhausted. Set a slippage limit to protect against unfavorable fills.
{% endhint %}

***

## Quantity Specification

You must specify **either** `base_quantity` **or** `quote_quantity`, but **not both**.

| Field           | Description                        | Example           |
| --------------- | ---------------------------------- | ----------------- |
| base\_quantity  | Amount of base asset (e.g., ADA)   | `"100"` = 100 ADA |
| quote\_quantity | Amount of quote asset (e.g., USDM) | `"93"` = 93 USDM  |

**Example for ADAUSDM pair:**

* Buy 100 ADA: `{"base_quantity": "100", "side": "buy", ...}`
* Buy $93 worth of ADA: `{"quote_quantity": "93", "side": "buy", ...}`

***

## Code Examples

### Limit Order Example

{% tabs %}
{% tab title="Curl" %}
```sh
curl --location 'https://api.deltadefi.io/order/build' \
--header 'X-API-KEY: <your_api_key>' \
--header 'Content-Type: application/json' \
--data '{
    "symbol": "ADAUSDM",
    "side": "buy",
    "type": "limit",
    "base_quantity": "100",
    "price": "0.93"
}'
```
{% endtab %}

{% tab title="NodeJs (axios)" %}
```javascript
const axios = require('axios');
let data = JSON.stringify({
  "symbol": "ADAUSDM",
  "side": "buy",
  "type": "limit",
  "base_quantity": "100",
  "price": "0.93"
});

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: 'https://api.deltadefi.io/order/build',
  headers: { 
    'X-API-KEY': '<your_api_key>', 
    'Content-Type': 'application/json'
  },
  data: data
};

axios.request(config)
.then((response) => {
  console.log(JSON.stringify(response.data));
})
.catch((error) => {
  console.log(error);
});
```
{% endtab %}

{% tab title="Go" %}
```go
package main

import (
  "fmt"
  "strings"
  "net/http"
  "io"
)

func main() {
  url := "https://api.deltadefi.io/order/build"
  method := "POST"

  payload := strings.NewReader(`{
    "symbol": "ADAUSDM",
    "side": "buy",
    "type": "limit",
    "base_quantity": "100",
    "price": "0.93"
}`)

  client := &http.Client{}
  req, err := http.NewRequest(method, url, payload)
  if err != nil {
    fmt.Println(err)
    return
  }
  req.Header.Add("X-API-KEY", "<your_api_key>")
  req.Header.Add("Content-Type", "application/json")

  res, err := client.Do(req)
  if err != nil {
    fmt.Println(err)
    return
  }
  defer res.Body.Close()

  body, err := io.ReadAll(res.Body)
  if err != nil {
    fmt.Println(err)
    return
  }
  fmt.Println(string(body))
}
```
{% endtab %}
{% endtabs %}

### Market Order Example

{% tabs %}
{% tab title="Curl" %}
```sh
curl --location 'https://api.deltadefi.io/order/build' \
--header 'X-API-KEY: <your_api_key>' \
--header 'Content-Type: application/json' \
--data '{
    "symbol": "ADAUSDM",
    "side": "buy",
    "type": "market",
    "base_quantity": "100",
    "max_slippage_basis_point": "100"
}'
```
{% endtab %}

{% tab title="NodeJs (axios)" %}
```javascript
const axios = require('axios');
let data = JSON.stringify({
  "symbol": "ADAUSDM",
  "side": "buy",
  "type": "market",
  "base_quantity": "100",
  "max_slippage_basis_point": "100"  // 1% max slippage
});

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: 'https://api.deltadefi.io/order/build',
  headers: { 
    'X-API-KEY': '<your_api_key>', 
    'Content-Type': 'application/json'
  },
  data: data
};

axios.request(config)
.then((response) => {
  console.log(JSON.stringify(response.data));
})
.catch((error) => {
  console.log(error);
});
```
{% endtab %}

{% tab title="Go" %}
```go
package main

import (
  "fmt"
  "strings"
  "net/http"
  "io"
)

func main() {
  url := "https://api.deltadefi.io/order/build"
  method := "POST"

  payload := strings.NewReader(`{
    "symbol": "ADAUSDM",
    "side": "buy",
    "type": "market",
    "base_quantity": "100",
    "max_slippage_basis_point": "100"
}`)

  client := &http.Client{}
  req, err := http.NewRequest(method, url, payload)
  if err != nil {
    fmt.Println(err)
    return
  }
  req.Header.Add("X-API-KEY", "<your_api_key>")
  req.Header.Add("Content-Type", "application/json")

  res, err := client.Do(req)
  if err != nil {
    fmt.Println(err)
    return
  }
  defer res.Body.Close()

  body, err := io.ReadAll(res.Body)
  if err != nil {
    fmt.Println(err)
    return
  }
  fmt.Println(string(body))
}
```
{% endtab %}
{% endtabs %}

### Post-Only Limit Order Example

{% tabs %}
{% tab title="Curl" %}
```sh
curl --location 'https://api.deltadefi.io/order/build' \
--header 'X-API-KEY: <your_api_key>' \
--header 'Content-Type: application/json' \
--data '{
    "symbol": "ADAUSDM",
    "side": "buy",
    "type": "limit",
    "base_quantity": "100",
    "price": "0.90",
    "post_only": true
}'
```
{% endtab %}
{% endtabs %}

***

## Response

```json
{
  "order_id": "550e8400-e29b-41d4-a716-446655440000",
  "tx_hex": "84a400818258203b40265111d8bb3c3c608d95b3a0bf83461ace32d79336579a1939b3aad1c0b700018182583900..."
}
```

| Field     | Type   | Description                                                                                                 |
| --------- | ------ | ----------------------------------------------------------------------------------------------------------- |
| order\_id | string | Unique order identifier. Use this when submitting the signed transaction.                                   |
| tx\_hex   | string | Unsigned transaction hex. Sign this and submit via [Submit Order Transaction](submit-order-transaction.md). |

***

## Next Steps

After building the order:

1. **Sign the transaction** using your wallet - see [How to sign a Cardano transaction](../../../../faq/cardano.md#how-can-i-sign-a-cardano-transaction)
2. **Submit the signed transaction** via [Submit Order Transaction](submit-order-transaction.md)

***

## Error Codes

| Code | Error                           | Description                                        |
| ---- | ------------------------------- | -------------------------------------------------- |
| 4050 | Insufficient balance            | Not enough free balance to place the order         |
| 4100 | Order size too small            | Order must be at least 5 ADA equivalent            |
| 4101 | Invalid order price             | Price must be greater than 0                       |
| 4102 | Invalid price decimal places    | Price has too many decimal places                  |
| 4103 | Invalid quantity decimal places | Quantity has too many decimal places               |
| 4104 | Post-only would match           | Post-only order would match immediately (rejected) |
| 4106 | Invalid symbol                  | Trading pair not found                             |
| 4109 | Insufficient liquidity          | Not enough liquidity for market order              |
| 4110 | Max open orders exceeded        | Too many open orders                               |

***

## Related

* [Submit Order Transaction](submit-order-transaction.md)
* [Cancel Order](build-cancel-order-transaction.md)
* [Order Records](../account/order-records.md)
* [Order Types](../../../../about/learn/trade/order-types.md)
