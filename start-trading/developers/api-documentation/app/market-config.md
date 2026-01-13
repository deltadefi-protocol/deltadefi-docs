# Market Configuration

Get all supported trading pairs and assets with their metadata. This endpoint provides essential information for trading including token decimals, symbols, and trading pair configurations.

{% tabs %}
{% tab title="Curl" %}
```sh
curl --location 'https://api.deltadefi.io/app/market-config'
```
{% endtab %}

{% tab title="NodeJs (axios)" %}
```javascript
const axios = require('axios');

let config = {
  method: 'get',
  maxBodyLength: Infinity,
  url: 'https://api.deltadefi.io/app/market-config'
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
  url := "https://api.deltadefi.io/app/market-config"
  method := "GET"

  client := &http.Client{}
  req, err := http.NewRequest(method, url, nil)
  if err != nil {
    fmt.Println(err)
    return
  }

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
  "assets": [
    {
      "symbol": "ADA",
      "unit": "lovelace",
      "decimals": 6,
      "max_qty_dp": 2,
      "trading_pairs": ["ADAUSDM"]
    },
    {
      "symbol": "USDM",
      "unit": "c48cbb3d5e57ed56e276bc45f99ab39abe94e6cd7ac39fb402da47ad.0014df105553444d",
      "decimals": 6,
      "max_qty_dp": 2,
      "trading_pairs": ["ADAUSDM"]
    }
  ],
  "trading_pairs": [
    {
      "symbol": "ADAUSDM",
      "base_token": {
        "symbol": "ADA",
        "unit": "lovelace",
        "decimals": 6,
        "max_qty_dp": 2
      },
      "quote_token": {
        "symbol": "USDM",
        "unit": "c48cbb3d5e57ed56e276bc45f99ab39abe94e6cd7ac39fb402da47ad.0014df105553444d",
        "decimals": 6,
        "max_qty_dp": 2
      },
      "price_max_dp": 4
    }
  ]
}
```

---

## Understanding the Response

### Assets

Each asset includes:

| Field | Type | Description |
|-------|------|-------------|
| symbol | string | Human-readable asset name (e.g., ADA, USDM) |
| unit | string | On-chain asset identifier (policy ID + asset name, or "lovelace" for ADA) |
| decimals | integer | Number of decimal places for the token on-chain |
| max_qty_dp | integer | Maximum decimal places allowed for quantity inputs |
| trading_pairs | array | List of trading pairs this asset is involved in |

### Trading Pairs

Each trading pair includes:

| Field | Type | Description |
|-------|------|-------------|
| symbol | string | Trading pair identifier (e.g., "ADAUSDM") |
| base_token | object | The base asset (what you're buying/selling) |
| quote_token | object | The quote asset (what you're pricing in) |
| price_max_dp | integer | Maximum decimal places for price inputs |

{% hint style="info" %}
Use this endpoint to dynamically discover available trading pairs and properly format quantities and prices in your trading application.
{% endhint %}
