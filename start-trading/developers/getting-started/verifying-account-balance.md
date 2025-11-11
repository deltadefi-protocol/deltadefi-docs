# Verifying account balance

{% hint style="info" %}
:sparkles:Pre-requisite:  You must create an account and obtain an API key via the user interface

[Create account here](../../getting-started/create-account.md)
{% endhint %}

### :white\_check\_mark: Verifying account balance

After you have made a successful deposit through our frontend UI, you can check your latest account balance via the [balances.md](../api-documentation/account/balances.md "mention") API.

{% tabs %}
{% tab title="curl" %}
```sh
curl --location 'https://api.deltadefi.io/accounts/balance' \
--header 'X-API-KEY: <your_api_key>'
```


{% endtab %}

{% tab title="NodeJs" %}
```javascript
const axios = require('axios');

let config = {
  method: 'get',
  maxBodyLength: Infinity,
  url: 'https://api.deltadefi.io/accounts/balance',
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

  url := "https://api.deltadefi.io/accounts/balance"
  method := "GET"

  client := &http.Client {
  }
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

Your Response should look something like below:

```json
[
    {
        "asset": "ada",
        "asset_unit": "",
        "free": 0,
        "locked": 100
    }
]
```

### Related FAQ

* [How do I get my API keys?](../auth.md)
* [How long does it take to deposit & withdraw?](../../../faq/product.md#how-long-does-it-take-to-deposit-and-withdrawal)
* [What are locked and free balances?](../../../faq/product.md#what-are-locked-and-free-balance)

