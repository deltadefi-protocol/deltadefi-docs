# Cancel Order

Cancel a single order by order ID. This endpoint directly cancels the order without requiring a separate build/submit step.

{% tabs %}
{% tab title="Curl" %}
```sh
curl --location --request POST 'https://api.deltadefi.io/order/<order_id>/cancel' \
--header 'X-API-KEY: <your_api_key>'
```
{% endtab %}

{% tab title="NodeJs (axios)" %}
```javascript
const axios = require('axios');

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: 'https://api.deltadefi.io/order/<order_id>/cancel',
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
  url := "https://api.deltadefi.io/order/<order_id>/cancel"
  method := "POST"

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
  "order_id": "550e8400-e29b-41d4-a716-446655440000"
}
```

{% hint style="info" %}
**Note:** The old build/submit pattern for cancelling orders has been deprecated. Orders are now cancelled directly with a single API call.
{% endhint %}
