# Deposit funds

{% hint style="info" %}
:sparkles:Pre-requisite:  You must create an account and obtain an API key via the user interface

[Create account here](../../getting-started/create-account.md)
{% endhint %}

{% stepper %}
{% step %}
### &#x20;Build a deposit transaction

You must first build a transaction using your current UTxO state before processing.&#x20;

[#how-can-i-get-utxos-from-my-wallet-address](../../../faq/cardano.md#how-can-i-get-utxos-from-my-wallet-address "mention")

* For in-depth API details[build-deposit-transaction.md](../api-documentation/account/build-deposit-transaction.md "mention").&#x20;
* For a list of supported assets, view [assets.md](../assets.md "mention")

In the following example, we're depositing 10 Ada, equivalent to `10_000_000` lovelace

{% tabs %}
{% tab title="Curl" %}
```sh
curl --location 'https://api.deltadefi.io/accounts/deposit/build' \
--header 'x-api-key: <your_api_key>' \
--header 'Content-Type: application/json' \
--data '{
    "deposit_amount": [
        {
            "unit": "lovelace",
            "quantity": "10000000"
        }
    ], 
    "input_utxos": [
        {
            "input": {
                "tx_hash": "6a33db7b4da84707b088d29fd6ec3072f03599427a4854c7ebe88c3052524385",
                "output_index": 4
            },
            "output": {
                "address": "addr_test1qr77kjlsarq8wy22g4flrcznjh5lkug5mvth7qhhkewgmezwvc8hnnjzy82j5twzf8dfy5gjk04yd09t488ys9605dvq4ymc4x",
                "amount": [
                    {
                        "unit": "lovelace",
                        "quantity": "77261137"
                    }
                ],
                "data_hash": null,
                "plutus_data": null,
                "script_ref": null,
                "script_hash": null
            }
        }
    ]
}
```


{% endtab %}

{% tab title="NodeJs (axios)" %}
```javascript
const axios = require('axios');
let data = JSON.stringify({
  "deposit_amount": [
    {
      "unit": "lovelace",
      "quantity": "10000000"
    }
  ],
  "input_utxos": [
    {
      "input": {
        "tx_hash": "6a33db7b4da84707b088d29fd6ec3072f03599427a4854c7ebe88c3052524385",
        "output_index": 4
      },
      "output": {
        "address": "addr_test1qr77kjlsarq8wy22g4flrcznjh5lkug5mvth7qhhkewgmezwvc8hnnjzy82j5twzf8dfy5gjk04yd09t488ys9605dvq4ymc4x",
        "amount": [
          {
            "unit": "lovelace",
            "quantity": "77261137"
          }
        ],
        "data_hash": null,
        "plutus_data": null,
        "script_ref": null,
        "script_hash": null
      }
    }
  ]
});

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: 'https://api.deltadefi.io/accounts/deposit/build',
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
{% endtabs %}
{% endstep %}

{% step %}
### Submit a deposit transaction

With the returned <mark style="color:orange;">`tx_hex`</mark> from step 1, you will need to sign it before submitting it.

[#how-can-i-sign-a-cardano-transaction](../../../faq/cardano.md#how-can-i-sign-a-cardano-transaction "mention")

For in-depth API details [submit-deposit-transaction.md](../api-documentation/submit-deposit-transaction.md "mention")

{% tabs %}
{% tab title="curl" %}
```sh

curl --location 'https://api.deltadefi.io/accounts/deposit/submit' \
--header 'X-API-key: <your_api_key>' \
--header 'Content-Type: application/json' \
--data '{
    "signed_tx": "<your_signed_tx>"
}

```


{% endtab %}

{% tab title="NodeJs (axios)" %}
```javascript
const axios = require('axios');
let data = JSON.stringify({
  "signed_tx": "<your_signed_tx>"
});

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: 'https://api.deltadefi.io/accounts/deposit/submit',
  headers: { 
    'X-API-key': '<your_api_key>', 
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

  url := "https://api.deltadefi.io/accounts/deposit/submit"
  method := "POST"

  payload := strings.NewReader(`{
    "signed_tx": "<your_signed_tx>"
}`)

  client := &http.Client {
  }
  req, err := http.NewRequest(method, url, payload)

  if err != nil {
    fmt.Println(err)
    return
  }
  req.Header.Add("X-API-key", "<your_api_key>")
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
{% endstepper %}

***

### :white\_check\_mark: Verifying deposit

After you have made a successful deposit request, you can check your latest account balance via the [balances.md](../api-documentation/account/balances.md "mention") API.

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



***

### Related FAQ

* [How do I get my API keys?](../auth.md)
* [What is the minimum amount of deposit and withdrawal?](../../../faq/product.md#the-minimum-deposit-amount)
* [How long does it take to deposit & withdraw?](../../../faq/product.md#how-long-does-it-take-to-deposit-and-withdrawal)
* [What are locked and free balances?](../../../faq/product.md#what-are-locked-and-free-balance)
* [How can I get UTxOs from my wallet address?](../../../faq/cardano.md#how-can-i-get-utxos-from-my-wallet-address)
* [How can I sign a Cardano transaction?](../../../faq/cardano.md#how-can-i-sign-a-cardano-transaction)

