# Withdraw funds

{% stepper %}
{% step %}
### Build withdrawal transaction&#x20;

Please note only free balances are able to withdraw from the current hydra cycle. [#free-and-locked-balances](deposit-funds.md#free-and-locked-balances "mention")

For in-depth API details [build-withdrawal-transaction.md](../api-documentation/account/build-withdrawal-transaction.md "mention")

In the following example we're withdrawing 10 Ada, equivalent  to 10\_000\_000 lovelace.

{% tabs %}
{% tab title="curl" %}
```sh
curl --location 'https://api-staging.deltadefi.io/accounts/withdrawal/build' \
--header 'x-api-key: <your_api_key>' \
--header 'Content-Type: application/json' \
--data '{
	"withdrawal_amount": [
		{
			"unit": "lovelace",
			"quantity": "1000000"
		},
	]
}'
```


{% endtab %}

{% tab title="NodeJs (axios)" %}
```javascript
const axios = require('axios');
let data = JSON.stringify({
  "withdrawal_amount": [
    {
      "unit": "lovelace",
      "quantity": "1000000"
    },
  ]
});

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: 'https://api-staging.deltadefi.io/accounts/withdrawal/build',
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

  url := "https://api-staging.deltadefi.io/accounts/withdrawal/build"
  method := "POST"

  payload := strings.NewReader(`{
	"withdrawal_amount": [
		{
			"unit": "lovelace",
			"quantity": "10000000"
		},
	]
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


{% endstep %}

{% step %}
### Submit withdrawal transaction

With the returned <mark style="color:orange;">`tx_hex`</mark> from step 1, you will need to [sign it](../../../faq/cardano.md#how-can-i-sign-a-cardano-transaction) before submitting it.

For in-depth API details [submit-withdrawal-transaction.md](../api-documentation/account/submit-withdrawal-transaction.md "mention")

{% tabs %}
{% tab title="curl" %}
```sh
curl --location 'https://api-staging.deltadefi.io/accounts/withdrawal/submit' \
--header 'X-API-KEY: <your_api_key>' \
--header 'Content-Type: application/json' \
--data '{
    "signed_tx": ""
}'
```
{% endtab %}

{% tab title="NodeJs (axios)" %}
```javascript
const axios = require('axios');
let data = JSON.stringify({
  "signed_tx": ""
});

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: 'https://api-staging.deltadefi.io/accounts/withdrawal/submit',
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

  url := "https://api-staging.deltadefi.io/accounts/withdrawal/submit"
  method := "POST"

  payload := strings.NewReader(`{
    "signed_tx": ""
}`)

  client := &http.Client {
  }
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

***

### :white\_check\_mark: Verifying withdrawal

After you have made a successful withdrawal request, you can check your latest account balance via the [balances.md](../api-documentation/account/balances.md "mention") API.

{% tabs %}
{% tab title="curl" %}
```sh
curl --location 'https://api-staging.deltadefi.io/accounts/balance' \
--header 'X-API-KEY: <your_api_key>'
```
{% endtab %}

{% tab title="NodeJs" %}
```javascript
const axios = require('axios');

let config = {
  method: 'get',
  maxBodyLength: Infinity,
  url: 'https://api-staging.deltadefi.io/accounts/balance',
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

  url := "https://api-staging.deltadefi.io/accounts/balance"
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

{% hint style="info" %}
Your requested withdrawal amount will be converted from <mark style="color:green;">`Free`</mark> will to <mark style="color:orange;">`Locked`</mark> , and will be distributed during the next hydra closed. &#x20;
{% endhint %}

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
{% endstep %}
{% endstepper %}

***

### Related FAQ

* [What is the minimum amount of deposit and withdrawal?](../../../faq/product.md#the-minimum-deposit-amount)
* [How long does it take to deposit & withdraw?](../../../faq/product.md#how-long-does-it-take-to-deposit-and-withdrawal)
* [What are locked and free balances?](../../../faq/product.md#what-are-locked-and-free-balances)
* [How can I sign a Cardano transaction?](../../../faq/cardano.md#how-can-i-sign-a-cardano-transaction)
