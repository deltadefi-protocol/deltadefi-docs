# Cancel Order

Cancel a single order by order ID. This endpoint directly cancels the order without requiring a separate build/submit step.

```json
{"openapi":"3.1.1","info":{"title":"Espresso API Server","version":"1.0"},"security":[{"ApiKeyAuth":[]}],"paths":{"/order/{orderId}/cancel":{"post":{"description":"Cancel a single order by order ID","parameters":[{"schema":{"type":"string"},"description":"Order ID","in":"path","name":"orderId","required":true}],"responses":{"200":{"description":"OK","content":{"application/json":{"schema":{"$ref":"#/components/schemas/CancelOrderResponse"}}}},"400":{"description":"Bad Request","content":{"application/json":{"schema":{"$ref":"#/components/schemas/ErrorJSONWithCodeResponse"}}}},"404":{"description":"Order Not Found","content":{"application/json":{"schema":{"$ref":"#/components/schemas/ErrorJSONWithCodeResponse"}}}},"500":{"description":"Internal Server Error","content":{"application/json":{"schema":{"$ref":"#/components/schemas/ErrorJSONWithCodeResponse"}}}}},"summary":"Cancel an order","tags":["order"]}}},"components":{"schemas":{"CancelOrderResponse":{"properties":{"order_id":{"type":"string"}},"type":"object"},"ErrorJSONWithCodeResponse":{"properties":{"code":{"type":"integer"},"error":{"type":"string"}},"type":"object"}}}}
```

## Example

### Request

```bash
curl -X POST "https://api.deltadefi.io/order/550e8400-e29b-41d4-a716-446655440000/cancel" \
  -H "X-API-KEY: your_api_key"
```

### Response

```json
{
  "order_id": "550e8400-e29b-41d4-a716-446655440000"
}
```

{% hint style="info" %}
**Note:** The old build/submit pattern for cancelling orders has been deprecated. Orders are now cancelled directly with a single API call.
{% endhint %}
