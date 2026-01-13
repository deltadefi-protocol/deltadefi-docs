# Market config

Get all supported trading pairs and assets with their metadata. This endpoint provides essential information for trading including token decimals, symbols, and trading pair configurations.



{% openapi-operation spec="V13" path="/app/market-config" method="get" %}
[OpenAPI V13](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/146df47964f80e2dc987856ffff1fb5c47812bac51e24beb8afdb298326dded0.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260113%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260113T061700Z&X-Amz-Expires=172800&X-Amz-Signature=00d2e7544274011ea4c82020135d2ddeeede9898b97ebef7d5a557bec017afbe&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

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

***

## Understanding the Response

### Assets

Each asset includes:

| Field          | Type    | Description                                                               |
| -------------- | ------- | ------------------------------------------------------------------------- |
| symbol         | string  | Human-readable asset name (e.g., ADA, USDM)                               |
| unit           | string  | On-chain asset identifier (policy ID + asset name, or "lovelace" for ADA) |
| decimals       | integer | Number of decimal places for the token on-chain                           |
| max\_qty\_dp   | integer | Maximum decimal places allowed for quantity inputs                        |
| trading\_pairs | array   | List of trading pairs this asset is involved in                           |

### Trading Pairs

Each trading pair includes:

| Field          | Type    | Description                                 |
| -------------- | ------- | ------------------------------------------- |
| symbol         | string  | Trading pair identifier (e.g., "ADAUSDM")   |
| base\_token    | object  | The base asset (what you're buying/selling) |
| quote\_token   | object  | The quote asset (what you're pricing in)    |
| price\_max\_dp | integer | Maximum decimal places for price inputs     |

{% hint style="info" %}
Use this endpoint to dynamically discover available trading pairs and properly format quantities and prices in your trading application.
{% endhint %}
