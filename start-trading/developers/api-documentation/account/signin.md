# Sign In

Sign in to DeltaDeFi using your Cardano wallet address. This endpoint authenticates the user and returns a JWT token for subsequent API calls.

```json
{"openapi":"3.1.1","info":{"title":"Espresso API Server","version":"1.0"},"paths":{"/accounts/signin":{"post":{"description":"Sign in with wallet address","requestBody":{"description":"Sign in request","required":true,"content":{"application/json":{"schema":{"$ref":"#/components/schemas/SignInRequest"}}}},"responses":{"200":{"description":"OK","content":{"application/json":{"schema":{"$ref":"#/components/schemas/SignInResponse"}}}},"400":{"description":"Bad Request","content":{"application/json":{"schema":{"$ref":"#/components/schemas/ErrorJSONWithCodeResponse"}}}},"422":{"description":"Unprocessable Entity","content":{"application/json":{"schema":{"$ref":"#/components/schemas/ErrorJSONWithCodeResponse"}}}},"500":{"description":"Internal Server Error","content":{"application/json":{"schema":{"$ref":"#/components/schemas/ErrorJSONWithCodeResponse"}}}}},"summary":"Sign in","tags":["accounts"]}}},"components":{"schemas":{"SignInRequest":{"properties":{"wallet_address":{"type":"string","description":"Cardano wallet address (bech32 format)"},"referral_code":{"type":"string","description":"Optional referral code"}},"required":["wallet_address"],"type":"object"},"SignInResponse":{"properties":{"token":{"type":"string","description":"JWT token for authentication"},"user_id":{"type":"string","description":"User ID"},"is_first_time":{"type":"boolean","description":"Whether this is the user's first sign in"},"is_onboarding_ready":{"type":"boolean","description":"Whether the user has completed onboarding (created spot account)"}},"type":"object"},"ErrorJSONWithCodeResponse":{"properties":{"code":{"type":"integer"},"error":{"type":"string"}},"type":"object"}}}}
```

## Example

### Request

```bash
curl -X POST "https://api.deltadefi.io/accounts/signin" \
  -H "Content-Type: application/json" \
  -d '{
    "wallet_address": "addr1qx...",
    "referral_code": "FRIEND123"
  }'
```

### Response

```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user_id": "550e8400-e29b-41d4-a716-446655440000",
  "is_first_time": false,
  "is_onboarding_ready": true
}
```

## Authentication Flow

1. **Sign In**: Call this endpoint with your wallet address to receive a JWT token
2. **Use Token**: Include the JWT token in the `Authorization` header for authenticated requests, OR
3. **Use API Key**: Alternatively, use your API key in the `X-API-KEY` header (see [Create new API key](create-new-api-key.md))

{% hint style="info" %}
The JWT token expires after a set period. For programmatic trading, we recommend using an API key instead.
{% endhint %}

## First Time Users

If `is_first_time` is `true`, the user needs to complete onboarding by creating a spot account. See [Create Spot Account](get-spot-account.md) for details.
