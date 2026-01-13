# Sign In

Sign in to DeltaDeFi using your Cardano wallet address. This endpoint authenticates the user and returns a JWT token for subsequent API calls.

{% tabs %}
{% tab title="Curl" %}
```sh
curl --location 'https://api.deltadefi.io/accounts/signin' \
--header 'Content-Type: application/json' \
--data '{
    "wallet_address": "addr1qx...",
    "referral_code": "FRIEND123"
}'
```
{% endtab %}

{% tab title="NodeJs (axios)" %}
```javascript
const axios = require('axios');
let data = JSON.stringify({
  "wallet_address": "addr1qx...",
  "referral_code": "FRIEND123"
});

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: 'https://api.deltadefi.io/accounts/signin',
  headers: { 
    'Content-Type': 'application/json'
  },
  data: data
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
  url := "https://api.deltadefi.io/accounts/signin"
  method := "POST"

  payload := strings.NewReader(`{
    "wallet_address": "addr1qx...",
    "referral_code": "FRIEND123"
}`)

  client := &http.Client{}
  req, err := http.NewRequest(method, url, payload)
  if err != nil {
    fmt.Println(err)
    return
  }
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

**Response:**

```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user_id": "550e8400-e29b-41d4-a716-446655440000",
  "is_first_time": false,
  "is_onboarding_ready": true
}
```

---

## Authentication Flow

1. **Sign In**: Call this endpoint with your wallet address to receive a JWT token
2. **Use Token**: Include the JWT token in the `Authorization` header for authenticated requests, OR
3. **Use API Key**: Alternatively, use your API key in the `X-API-KEY` header (see [Create new API key](create-new-api-key.md))

{% hint style="info" %}
The JWT token expires after a set period. For programmatic trading, we recommend using an API key instead.
{% endhint %}

---

## First Time Users

If `is_first_time` is `true`, the user needs to complete onboarding by creating a spot account. See [Create Spot Account](get-spot-account.md) for details.

---

## Request Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| wallet_address | string | Yes | Cardano wallet address in bech32 format |
| referral_code | string | No | Optional referral code |

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| token | string | JWT token for authentication |
| user_id | string | User ID |
| is_first_time | boolean | Whether this is the user's first sign in |
| is_onboarding_ready | boolean | Whether the user has completed onboarding (created spot account) |
