# Cancel All Orders

Cancel all open orders for a given symbol. This endpoint directly cancels all orders without requiring a separate build/submit step.

{% tabs %}
{% tab title="Curl" %}
```sh
curl --location 'https://api.deltadefi.io/order/cancel-all' \
--header 'X-API-KEY: <your_api_key>' \
--header 'Content-Type: application/json' \
--data '{
    "symbol": "ADAUSDX"
}'
```
{% endtab %}

{% tab title="NodeJs (axios)" %}
```javascript
const axios = require('axios');
let data = JSON.stringify({
  "symbol": "ADAUSDX"
});

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: 'https://api.deltadefi.io/order/cancel-all',
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
  url := "https://api.deltadefi.io/order/cancel-all"
  method := "POST"

  payload := strings.NewReader(`{
    "symbol": "ADAUSDX"
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

**Response:**

```json
{
  "symbol": "ADAUSDX",
  "order_ids": [
    "550e8400-e29b-41d4-a716-446655440000",
    "550e8400-e29b-41d4-a716-446655440001"
  ]
}
```

{% hint style="info" %}
**Note:** The old build/submit pattern for cancelling orders has been deprecated. All orders for a symbol are now cancelled directly with a single API call.
{% endhint %}
