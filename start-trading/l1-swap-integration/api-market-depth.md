# API - Market Depth

DeltaDeFi hosts official APIs to improve accessibility of the L1 swap contracts. The entire swap is still mostly handled through Aiken smart contract, the API provides additional information to facilitate informed trading decision going through.

### URL

<table><thead><tr><th width="312.3671875">Environment</th><th>URL Endpoint</th></tr></thead><tbody><tr><td>Pre-Prod</td><td><code>https://operator-staging.deltadefi.io</code></td></tr><tr><td>Mainnet</td><td>TBC</td></tr></tbody></table>

***

### GET /depth/{symbol}

Get the current market depth for a trading pair post fee. The `price` shown in depth response has is exactly what you could expect to trade without fee.

#### Example Request

```
GET /depth/NIGHTUSDM
```

#### Example Response

```json
{
  "timestamp": 1773113131587,
  "bids": [
    { "price": "0.05090", "quantity": "31395" } // Buy order - 31,395 NIGHT at $0.05090
  ],
  "asks": [
    { "price": "0.05311", "quantity": "3977.5" }, // Sell order - 3,977.5 NIGHT at $0.05090
    { "price": "0.05210", "quantity": "6220" }
  ]
}
```

#### Response Fields

<table><thead><tr><th width="143.4375">Field</th><th width="141.69140625">Type</th><th>Description</th></tr></thead><tbody><tr><td>timestamp</td><td>number</td><td>Unix timestamp in milliseconds</td></tr><tr><td>bids</td><td>array</td><td>Buy orders - price/quantity objects</td></tr><tr><td>asks</td><td>array</td><td>Sell orders - price/quantity objects</td></tr></tbody></table>
