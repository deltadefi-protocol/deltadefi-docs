# Order records

This page documents the endpoints for retrieving order information.

## Get open orders

Get open orders for the authenticated user with pagination. Quantities are returned in human-readable format adjusted for token decimals.

{% tabs %}
{% tab title="Curl" %}
```sh
curl --location 'https://api.deltadefi.io/accounts/open-orders?symbol=ADAUSDX&page=1&limit=10' \
--header 'X-API-KEY: <your_api_key>'
```
{% endtab %}

{% tab title="NodeJs (axios)" %}
```javascript
const axios = require('axios');

let config = {
  method: 'get',
  maxBodyLength: Infinity,
  url: 'https://api.deltadefi.io/accounts/open-orders?symbol=ADAUSDX&page=1&limit=10',
  headers: { 
    'X-API-KEY': '<your_api_key>'
  }
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
  "net/http"
  "io"
)

func main() {
  url := "https://api.deltadefi.io/accounts/open-orders?symbol=ADAUSDX&page=1&limit=10"
  method := "GET"

  client := &http.Client{}
  req, err := http.NewRequest(method, url, nil)
  if err != nil {
    fmt.Println(err)
    return
  }
  req.Header.Add("X-API-KEY", "<your_api_key>")

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

**Response:**

```json
{
  "data": [
    {
      "id": "order_123",
      "account_id": "acc_456",
      "symbol": "ADAUSDX",
      "side": "buy",
      "type": "limit",
      "status": "open",
      "price": "0.93",
      "base_qty": "100",
      "quote_qty": "93",
      "executed_base_qty": "0",
      "executed_quote_qty": "0",
      "created_at": "2024-01-01T00:00:00Z",
      "updated_at": "2024-01-01T00:00:00Z"
    }
  ],
  "total_count": 1,
  "total_page": 1
}
```

---

## Get trade orders

Get trade orders (orders with executions) for the authenticated user with pagination. Quantities are returned in human-readable format adjusted for token decimals.

{% tabs %}
{% tab title="Curl" %}
```sh
curl --location 'https://api.deltadefi.io/accounts/trade-orders?symbol=ADAUSDX&page=1&limit=10' \
--header 'X-API-KEY: <your_api_key>'
```
{% endtab %}

{% tab title="NodeJs (axios)" %}
```javascript
const axios = require('axios');

let config = {
  method: 'get',
  maxBodyLength: Infinity,
  url: 'https://api.deltadefi.io/accounts/trade-orders?symbol=ADAUSDX&page=1&limit=10',
  headers: { 
    'X-API-KEY': '<your_api_key>'
  }
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
  "net/http"
  "io"
)

func main() {
  url := "https://api.deltadefi.io/accounts/trade-orders?symbol=ADAUSDX&page=1&limit=10"
  method := "GET"

  client := &http.Client{}
  req, err := http.NewRequest(method, url, nil)
  if err != nil {
    fmt.Println(err)
    return
  }
  req.Header.Add("X-API-KEY", "<your_api_key>")

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

**Response:**

```json
{
  "data": [
    {
      "id": "order_123",
      "account_id": "acc_456",
      "symbol": "ADAUSDX",
      "side": "buy",
      "type": "limit",
      "status": "closed",
      "price": "0.93",
      "base_qty": "100",
      "quote_qty": "93",
      "executed_base_qty": "100",
      "executed_quote_qty": "93",
      "executed_price": "0.93",
      "commission": "0.093",
      "commission_unit": "USDX",
      "commission_rate_bp": 10,
      "order_execution_records": [
        {
          "id": "exec_789",
          "order_id": "order_123",
          "execution_price": "0.93",
          "filled_base_qty": "100",
          "filled_quote_qty": "93",
          "role": "taker",
          "created_at": "2024-01-01T00:00:00Z"
        }
      ]
    }
  ],
  "total_count": 1,
  "total_page": 1
}
```

---

## Get account trades

Get execution records (trades) for the authenticated user with pagination. Quantities are returned in human-readable format adjusted for token decimals.

{% tabs %}
{% tab title="Curl" %}
```sh
curl --location 'https://api.deltadefi.io/accounts/trades?symbol=ADAUSDX&page=1&limit=10' \
--header 'X-API-KEY: <your_api_key>'
```
{% endtab %}

{% tab title="NodeJs (axios)" %}
```javascript
const axios = require('axios');

let config = {
  method: 'get',
  maxBodyLength: Infinity,
  url: 'https://api.deltadefi.io/accounts/trades?symbol=ADAUSDX&page=1&limit=10',
  headers: { 
    'X-API-KEY': '<your_api_key>'
  }
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
  "net/http"
  "io"
)

func main() {
  url := "https://api.deltadefi.io/accounts/trades?symbol=ADAUSDX&page=1&limit=10"
  method := "GET"

  client := &http.Client{}
  req, err := http.NewRequest(method, url, nil)
  if err != nil {
    fmt.Println(err)
    return
  }
  req.Header.Add("X-API-KEY", "<your_api_key>")

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

**Response:**

```json
{
  "data": [
    {
      "id": "exec_789",
      "order_id": "order_123",
      "account_id": "acc_456",
      "counter_party_order_id": "order_999",
      "execution_price": "0.93",
      "filled_base_qty": "100",
      "filled_quote_qty": "93",
      "commission": "0.093",
      "commission_unit": "USDX",
      "role": "taker",
      "created_at": "2024-01-01T00:00:00Z"
    }
  ],
  "total_count": 1,
  "total_page": 1
}
```

---

## Get a single order record

Get a single order record by order ID.

{% tabs %}
{% tab title="Curl" %}
```sh
curl --location 'https://api.deltadefi.io/account/order?id=<order_id>' \
--header 'X-API-KEY: <your_api_key>'
```
{% endtab %}

{% tab title="NodeJs (axios)" %}
```javascript
const axios = require('axios');

let config = {
  method: 'get',
  maxBodyLength: Infinity,
  url: 'https://api.deltadefi.io/account/order?id=<order_id>',
  headers: { 
    'X-API-KEY': '<your_api_key>'
  }
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
  "net/http"
  "io"
)

func main() {
  url := "https://api.deltadefi.io/account/order?id=<order_id>"
  method := "GET"

  client := &http.Client{}
  req, err := http.NewRequest(method, url, nil)
  if err != nil {
    fmt.Println(err)
    return
  }
  req.Header.Add("X-API-KEY", "<your_api_key>")

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

**Response:**

```json
{
  "id": "order_123",
  "account_id": "acc_456",
  "symbol": "ADAUSDX",
  "side": "buy",
  "type": "limit",
  "status": "open",
  "price": "0.93",
  "base_qty": "100",
  "quote_qty": "93",
  "executed_base_qty": "0",
  "executed_quote_qty": "0",
  "created_at": "2024-01-01T00:00:00Z",
  "updated_at": "2024-01-01T00:00:00Z"
}
```
