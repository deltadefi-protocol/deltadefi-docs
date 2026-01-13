# Market Configuration

Get all supported trading pairs and assets with their metadata. This endpoint provides essential information for trading including token decimals, symbols, and trading pair configurations.

```json
{"openapi":"3.1.1","info":{"title":"Espresso API Server","version":"1.0"},"paths":{"/app/market-config":{"get":{"description":"Get all supported trading pairs and assets with their metadata","responses":{"200":{"description":"OK","content":{"application/json":{"schema":{"$ref":"#/components/schemas/GetMarketConfigResponse"}}}},"500":{"description":"Internal Server Error","content":{"application/json":{"schema":{"$ref":"#/components/schemas/ErrorJSONWithCodeResponse"}}}}},"summary":"Get market configuration","tags":["app"]}}},"components":{"schemas":{"GetMarketConfigResponse":{"properties":{"assets":{"items":{"$ref":"#/components/schemas/MarketConfigAsset"},"type":"array"},"trading_pairs":{"items":{"$ref":"#/components/schemas/MarketConfigTradingPair"},"type":"array"}},"type":"object"},"MarketConfigAsset":{"properties":{"symbol":{"type":"string","description":"Asset symbol (e.g., ADA, USDM)"},"unit":{"type":"string","description":"Asset unit/policy ID (e.g., lovelace)"},"decimals":{"type":"integer","description":"Number of decimal places"},"max_qty_dp":{"type":"integer","description":"Maximum decimal places for quantity input"},"trading_pairs":{"items":{"type":"string"},"type":"array","description":"Trading pairs this asset is part of"}},"type":"object"},"MarketConfigTradingPair":{"properties":{"symbol":{"type":"string","description":"Trading pair symbol (e.g., ADAUSDM)"},"base_token":{"$ref":"#/components/schemas/MarketConfigToken"},"quote_token":{"$ref":"#/components/schemas/MarketConfigToken"},"price_max_dp":{"type":"integer","description":"Maximum decimal places for price"}},"type":"object"},"MarketConfigToken":{"properties":{"symbol":{"type":"string"},"unit":{"type":"string"},"decimals":{"type":"integer"},"max_qty_dp":{"type":"integer"}},"type":"object"},"ErrorJSONWithCodeResponse":{"properties":{"code":{"type":"integer"},"error":{"type":"string"}},"type":"object"}}}}
```

## Example

### Request

```bash
curl -X GET "https://api.deltadefi.io/app/market-config"
```

### Response

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

## Understanding the Response

### Assets

Each asset includes:
- **symbol**: Human-readable asset name
- **unit**: On-chain asset identifier (policy ID + asset name, or "lovelace" for ADA)
- **decimals**: Number of decimal places for the token on-chain
- **max_qty_dp**: Maximum decimal places allowed for quantity inputs
- **trading_pairs**: List of trading pairs this asset is involved in

### Trading Pairs

Each trading pair includes:
- **symbol**: Trading pair identifier (e.g., "ADAUSDM")
- **base_token**: The base asset (what you're buying/selling)
- **quote_token**: The quote asset (what you're pricing in)
- **price_max_dp**: Maximum decimal places for price inputs

{% hint style="info" %}
Use this endpoint to dynamically discover available trading pairs and properly format quantities and prices in your trading application.
{% endhint %}
