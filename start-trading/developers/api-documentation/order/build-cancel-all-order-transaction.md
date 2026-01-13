# Cancel All Orders

Cancel all open orders for a given symbol. This endpoint directly cancels all orders without requiring a separate build/submit step.

```json
{"openapi":"3.1.1","info":{"title":"Espresso API Server","version":"1.0"},"security":[{"ApiKeyAuth":[]}],"paths":{"/order/cancel-all":{"post":{"description":"Cancel all open orders for a given symbol","requestBody":{"description":"Cancel all orders request","required":true,"content":{"application/json":{"schema":{"$ref":"#/components/schemas/CancelAllOrdersRequest"}}}},"responses":{"200":{"description":"OK","content":{"application/json":{"schema":{"$ref":"#/components/schemas/CancelAllOrdersResponse"}}}},"400":{"description":"Bad Request","content":{"application/json":{"schema":{"$ref":"#/components/schemas/ErrorJSONWithCodeResponse"}}}},"404":{"description":"Order Not Found","content":{"application/json":{"schema":{"$ref":"#/components/schemas/ErrorJSONWithCodeResponse"}}}},"422":{"description":"Unprocessable Entity","content":{"application/json":{"schema":{"$ref":"#/components/schemas/ErrorJSONWithCodeResponse"}}}},"500":{"description":"Internal Server Error","content":{"application/json":{"schema":{"$ref":"#/components/schemas/ErrorJSONWithCodeResponse"}}}}},"summary":"Cancel all orders","tags":["order"]}}},"components":{"schemas":{"CancelAllOrdersRequest":{"properties":{"symbol":{"type":"string","description":"Trading pair symbol (e.g., ADAUSDM)"}},"required":["symbol"],"type":"object"},"CancelAllOrdersResponse":{"properties":{"order_ids":{"items":{"type":"string"},"type":"array"},"symbol":{"type":"string"}},"type":"object"},"ErrorJSONWithCodeResponse":{"properties":{"code":{"type":"integer"},"error":{"type":"string"}},"type":"object"}}}}
```

## Example

### Request

```bash
curl -X POST "https://api.deltadefi.io/order/cancel-all" \
  -H "X-API-KEY: your_api_key" \
  -H "Content-Type: application/json" \
  -d '{"symbol": "ADAUSDM"}'
```

### Response

```json
{
  "symbol": "ADAUSDM",
  "order_ids": [
    "550e8400-e29b-41d4-a716-446655440000",
    "550e8400-e29b-41d4-a716-446655440001"
  ]
}
```

{% hint style="info" %}
**Note:** The old build/submit pattern for cancelling orders has been deprecated. All orders for a symbol are now cancelled directly with a single API call.
{% endhint %}
