# Spot Account

Manage your DeltaDeFi spot trading account. A spot account is required for trading and holds your encrypted operation key.

## Get Spot Account

Get spot account details for the authenticated user.

```json
{"openapi":"3.1.1","info":{"title":"Espresso API Server","version":"1.0"},"security":[{"ApiKeyAuth":[]}],"paths":{"/accounts/spot-account":{"get":{"description":"Get spot account details for a user","parameters":[{"schema":{"type":"string"},"description":"API Key","in":"header","name":"X-API-KEY","required":true}],"responses":{"200":{"description":"OK","content":{"application/json":{"schema":{"$ref":"#/components/schemas/GetSpotAccountResponse"}}}},"400":{"description":"Bad Request","content":{"application/json":{"schema":{"$ref":"#/components/schemas/ErrorJSONWithCodeResponse"}}}},"401":{"description":"Unauthorized","content":{"application/json":{"schema":{"$ref":"#/components/schemas/ErrorJSONWithCodeResponse"}}}},"500":{"description":"Internal Server Error","content":{"application/json":{"schema":{"$ref":"#/components/schemas/ErrorJSONWithCodeResponse"}}}}},"summary":"Get spot account","tags":["accounts"]}}},"components":{"schemas":{"GetSpotAccountResponse":{"properties":{"account_id":{"type":"string"},"account_type":{"type":"string"},"created_at":{"type":"string"},"encrypted_operation_key":{"type":"string"},"operation_key_hash":{"type":"string"}},"type":"object"},"ErrorJSONWithCodeResponse":{"properties":{"code":{"type":"integer"},"error":{"type":"string"}},"type":"object"}}}}
```

## Create Spot Account

Create a new spot account for the authenticated user. This is required during onboarding after the first sign-in.

```json
{"openapi":"3.1.1","info":{"title":"Espresso API Server","version":"1.0"},"security":[{"ApiKeyAuth":[]}],"paths":{"/accounts/spot-account":{"post":{"description":"Create a new spot account for a user","parameters":[{"schema":{"type":"string"},"description":"API Key","in":"header","name":"X-API-KEY","required":true}],"requestBody":{"description":"Create Spot Account Request","required":true,"content":{"application/json":{"schema":{"$ref":"#/components/schemas/CreateSpotAccountRequest"}}}},"responses":{"200":{"description":"OK","content":{"application/json":{"schema":{"$ref":"#/components/schemas/CreateSpotAccountResponse"}}}},"400":{"description":"Bad Request","content":{"application/json":{"schema":{"$ref":"#/components/schemas/ErrorJSONWithCodeResponse"}}}},"401":{"description":"Unauthorized","content":{"application/json":{"schema":{"$ref":"#/components/schemas/ErrorJSONWithCodeResponse"}}}},"422":{"description":"Unprocessable Entity","content":{"application/json":{"schema":{"$ref":"#/components/schemas/ErrorJSONWithCodeResponse"}}}},"500":{"description":"Internal Server Error","content":{"application/json":{"schema":{"$ref":"#/components/schemas/ErrorJSONWithCodeResponse"}}}}},"summary":"Create a new spot account","tags":["accounts"]}}},"components":{"schemas":{"CreateSpotAccountRequest":{"properties":{"user_id":{"type":"string","description":"User ID from sign-in response"},"operation_key_hash":{"type":"string","description":"Hash of the operation key"},"encrypted_operation_key":{"type":"string","description":"Operation key encrypted with user's password"},"is_script_operation_key":{"type":"boolean","description":"Whether the operation key is a script key"},"referral_code":{"type":"string","description":"Optional referral code"}},"required":["user_id","operation_key_hash","encrypted_operation_key","is_script_operation_key"],"type":"object"},"CreateSpotAccountResponse":{"properties":{"account_id":{"type":"string"},"account_type":{"type":"string"},"created_at":{"type":"string"},"encrypted_operation_key":{"type":"string"},"operation_key_hash":{"type":"string"}},"type":"object"},"ErrorJSONWithCodeResponse":{"properties":{"code":{"type":"integer"},"error":{"type":"string"}},"type":"object"}}}}
```

### Create Account Example

```bash
curl -X POST "https://api.deltadefi.io/accounts/spot-account" \
  -H "X-API-KEY: your_api_key" \
  -H "Content-Type: application/json" \
  -d '{
    "user_id": "550e8400-e29b-41d4-a716-446655440000",
    "operation_key_hash": "abc123...",
    "encrypted_operation_key": "encrypted_key_data...",
    "is_script_operation_key": false
  }'
```

## Update Spot Account

Update the spot account's operation key. This is useful when rotating keys for security.

```json
{"openapi":"3.1.1","info":{"title":"Espresso API Server","version":"1.0"},"security":[{"ApiKeyAuth":[]}],"paths":{"/accounts/spot-account":{"put":{"description":"Update spot account details for a user","parameters":[{"schema":{"type":"string"},"description":"API Key","in":"header","name":"X-API-KEY","required":true}],"requestBody":{"description":"Update Spot Account Request","required":true,"content":{"application/json":{"schema":{"$ref":"#/components/schemas/UpdateSpotAccountRequest"}}}},"responses":{"200":{"description":"OK","content":{"application/json":{"schema":{"$ref":"#/components/schemas/UpdateSpotAccountResponse"}}}},"400":{"description":"Bad Request","content":{"application/json":{"schema":{"$ref":"#/components/schemas/ErrorJSONWithCodeResponse"}}}},"401":{"description":"Unauthorized","content":{"application/json":{"schema":{"$ref":"#/components/schemas/ErrorJSONWithCodeResponse"}}}},"422":{"description":"Unprocessable Entity","content":{"application/json":{"schema":{"$ref":"#/components/schemas/ErrorJSONWithCodeResponse"}}}},"500":{"description":"Internal Server Error","content":{"application/json":{"schema":{"$ref":"#/components/schemas/ErrorJSONWithCodeResponse"}}}}},"summary":"Update spot account","tags":["accounts"]}}},"components":{"schemas":{"UpdateSpotAccountRequest":{"properties":{"user_id":{"type":"string","description":"User ID"},"encrypted_operation_key":{"type":"string","description":"New encrypted operation key"}},"required":["user_id","encrypted_operation_key"],"type":"object"},"UpdateSpotAccountResponse":{"properties":{"account_id":{"type":"string"},"account_type":{"type":"string"},"created_at":{"type":"string"},"updated_at":{"type":"string"},"encrypted_operation_key":{"type":"string"},"operation_key_hash":{"type":"string"}},"type":"object"},"ErrorJSONWithCodeResponse":{"properties":{"code":{"type":"integer"},"error":{"type":"string"}},"type":"object"}}}}
```

### Update Account Example

```bash
curl -X PUT "https://api.deltadefi.io/accounts/spot-account" \
  -H "X-API-KEY: your_api_key" \
  -H "Content-Type: application/json" \
  -d '{
    "user_id": "550e8400-e29b-41d4-a716-446655440000",
    "encrypted_operation_key": "new_encrypted_key_data..."
  }'
```

## Understanding Operation Keys

The operation key is a crucial security component:

- **Generated client-side**: Never sent to the server in plain text
- **Encrypted with your password**: Uses AES-GCM encryption
- **Used for signing trades**: Authorizes trading operations without your master wallet

{% hint style="warning" %}
The encrypted operation key is stored on DeltaDeFi's servers, but only you can decrypt it with your password. Never share your password or unencrypted operation key.
{% endhint %}
