# Place a new order

{% hint style="info" %}
:sparkles:Pre-requisite:  You account must have free balances in order to place a new order.   &#x20;

[What are locked and free balances?](../../../faq/product.md#what-are-locked-and-free-balances)
{% endhint %}



{% stepper %}
{% step %}
### Build a limit order transaction

In the following example, we will be creating a limit order.

To place a new order, you must provide the following:

* price&#x20;
* quantity
* side
* symbol
* type

For an in-depth API reference [build-order-transaction.md](../api-documentation/order/build-order-transaction.md "mention")

{% tabs %}
{% tab title="Curl" %}
```sh
curl --location 'https://api.deltadefi.io/order/build' \
--header 'x-api-key: <your_api_key>' \
--header 'Content-Type: application/json' \
--data '{
	"symbol": "ADAUSDX",
    "side": "buy",
    "type": "limit",
    "quantity": 100,
    "price": 0.93    
}'
```


{% endtab %}

{% tab title="NodeJs (axios)" %}
```javascript
const axios = require('axios');
let data = JSON.stringify({
  "symbol": "ADAUSDX",
  "side": "buy",
  "type": "limit",
  "quantity": 100,
  "price": 0.93
});

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: 'https://api.deltadefi.io/order/build',
  headers: { 
    'x-api-key': '<your_api_key>', 
    'Content-Type': 'application/json'
  },
  data : data
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
{% endtabs %}


{% endstep %}

{% step %}
### Submit a limit order transaction

After the order transaction is built, you will then need to [sign it](../../../faq/cardano.md#how-can-i-sign-a-cardano-transaction) before submitting it.

To submit:

{% tabs %}
{% tab title="Curl" %}
```sh
curl --location 'https://api.deltadefi.io/order/submit' \
--header 'X-API-KEY: <your_api_key>' \
--header 'Content-Type: application/json' \
--data '{
    "order_id": "<order_id>",
    "signed_tx":"<signed_tx>"
}'
```


{% endtab %}

{% tab title="NodeJs (axios)" %}
```javascript
const axios = require('axios');
let data = JSON.stringify({
  "order_id": "<order_id>",
  "signed_tx": "<signed_tx>"
});

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: 'https://api-staging.deltadefi.io/order/submit',
  headers: { 

    'X-API-KEY': '<your_api_key>', 
    'Content-Type': 'application/json'
  },
  data : data
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

  url := "https://api-staging.deltadefi.io/order/submit"
  method := "POST"

  payload := strings.NewReader(`{
    "order_id": "<order_id>",
    "signed_tx":"<signed_tx>"
}`)

  client := &http.Client {
  }
  req, err := http.NewRequest(method, url, payload)

  if err != nil {
    fmt.Println(err)
    return
  }
  req.Header.Add("Authorization", "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE3NDI1Mzk5NDAsInN1YiI6ImFkZHJfdGVzdDFxcXpnZzVwY2FleWVhNjl1cHRsOWRhNWc3ZmFqbTRtMHl2eG5keDlmNGx4cGtlaHFnZXp5MHMwNHJ0ZHdsYzB0bHZ4YWZwZHJmeG5zZzd3dzY4Z2UzajdsMGxuc3pzdzJ3dCJ9.OAchsj0tv06NxD9Br0aj0Zw5XzpG8kUFKBuVPtz5AKA")
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


{% endstep %}

{% step %}
### Build a market order transaction

In this example we will be creating a market order.

For an in-depth API reference [build-order-transaction.md](../api-documentation/order/build-order-transaction.md "mention")

To place a market order, provide the following:

* price&#x20;
* quantity
* side
* symbol
* type
* limit\_slippage / max\_slippage\_basis\_point (either one)

_**limit\_slippage (bool)**_: If set to false, the market order will allow unlimited slippage until the entire order quantity is filled, where the account's purchasing power allows

_**max\_slippage\_basis\_points (int)**_: Maximum Slippage is the maximum acceptable deviation between the expected price (market price) and the actual executed price in a market order transaction

{% tabs %}
{% tab title="Curl" %}
```sh
curl --location 'https://api-staging.deltadefi.io/order/build' \
--header 'x-api-key: <your_api_key>' \
--header 'Content-Type: application/json' \
--data '{
    "symbol": "ADAUSDX",
    "side": "buy",
    "type": "market",
    "quantity": 100,
    "limit_slippage": true
}'
```
{% endtab %}

{% tab title="NodeJs (axios)" %}
```javascript
const axios = require('axios');
let data = JSON.stringify({
  "symbol": "ADAUSDX",
  "side": "buy",
  "type": "market",
  "quantity": 100,
  "limit_slippage": false
});

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: 'https://api-staging.deltadefi.io/order/build',
  headers: { 
    'x-api-key': '<your_api_key>', 
    'Content-Type': 'application/json'
  },
  data : data
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

  url := "https://api-staging.deltadefi.io/order/build"
  method := "POST"

  payload := strings.NewReader(`{
    "symbol": "ADAUSDX",
    "side": "buy",
    "type": "market",
    "quantity": 100,
    "limit_slippage":false
}`)

  client := &http.Client {
  }
  req, err := http.NewRequest(method, url, payload)

  if err != nil {
    fmt.Println(err)
    return
  }
  req.Header.Add("x-api-key", "<your_api_key>")
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

After the transaction is built, follow step 2 above to submit the transaction.

***
{% endstep %}
{% endstepper %}

### :book: Get Order Records

After an order is created, you can find your order records with the [order-records.md](../api-documentation/account/order-records.md "mention") API

For open orders:

* Pass the query param <mark style="color:green;">**`openOrder`**</mark>

For orderHistory:

* pass the query param <mark style="color:orange;">**`orderHistory`**</mark>&#x20;

For tradingHistory

* pass the query param <mark style="color:yellow;">**`tradingHistory`**</mark>&#x20;

{% tabs %}
{% tab title="Curl" %}
```sh
curl --location 'https://api.deltadefi.io/accounts/order-records?status=open' \
--header 'x-api-key: <your_api_key>'
```


{% endtab %}

{% tab title="NodeJs (axios)" %}
```javascript
const axios = require('axios');

let config = {
  method: 'get',
  maxBodyLength: Infinity,
  url: 'https://api.deltadefi.io/accounts/order-records?status=open',
  headers: { 
    'x-api-key': '<your_api_key>'
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

  url := "https://api.deltadefi.io/accounts/order-records?status=open"
  method := "GET"

  client := &http.Client {
  }
  req, err := http.NewRequest(method, url, nil)

  if err != nil {
    fmt.Println(err)
    return
  }
  req.Header.Add("x-api-key", "<your_api_key>")

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



***

### Related FAQ

* [What order types are available? ](../../../about/learn/trade/order-types.md)
* [Placing orders through website](../../getting-started/place-order.md)
* [How can I sign a Cardano transaction?](../../../faq/cardano.md#how-can-i-sign-a-cardano-transaction)[ ](../../getting-started/place-order.md)
