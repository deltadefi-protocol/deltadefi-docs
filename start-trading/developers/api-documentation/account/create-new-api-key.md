# Create New API Key

Create a new API key for programmatic access to the DeltaDeFi trading API. API keys provide a more permanent authentication method compared to JWT tokens.

```json
{"openapi":"3.1.1","info":{"title":"Espresso API Server","version":"1.0"},"security":[{"ApiKeyAuth":[]}],"paths":{"/accounts/new-api-key":{"get":{"description":"Create a new API key for the authenticated user. The new API key will replace any existing API key. Store it securely as it cannot be retrieved again.","parameters":[{"schema":{"type":"string"},"description":"Current API Key or JWT Token","in":"header","name":"X-API-KEY","required":true}],"responses":{"200":{"description":"New API key created successfully","content":{"application/json":{"schema":{"$ref":"#/components/schemas/CreateNewAPIKeyResponse"}}}},"401":{"description":"Unauthorized","content":{"application/json":{"schema":{"$ref":"#/components/schemas/ErrorJSONWithCodeResponse"}}}},"500":{"description":"Internal Server Error","content":{"application/json":{"schema":{"$ref":"#/components/schemas/ErrorJSONWithCodeResponse"}}}}},"summary":"Create new API key","tags":["accounts"]}}},"components":{"schemas":{"CreateNewAPIKeyResponse":{"properties":{"api_key":{"type":"string","example":"dk_live_abc123def456ghi789jkl012mno345","description":"The new API key. Store this securely."},"created_at":{"type":"string","example":"2024-01-01T00:00:00Z","description":"Timestamp when the API key was created"}},"type":"object"},"ErrorJSONWithCodeResponse":{"properties":{"code":{"type":"integer","example":4000},"error":{"type":"string","example":"Invalid request data"}},"type":"object"}}}}
```

---

## Code Examples

{% tabs %}
{% tab title="Curl" %}
```sh
curl --location 'https://api.deltadefi.io/accounts/new-api-key' \
--header 'X-API-KEY: <your_current_api_key>'
```
{% endtab %}

{% tab title="NodeJs (axios)" %}
```javascript
const axios = require('axios');

let config = {
  method: 'get',
  maxBodyLength: Infinity,
  url: 'https://api.deltadefi.io/accounts/new-api-key',
  headers: { 
    'X-API-KEY': '<your_current_api_key>'
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
  url := "https://api.deltadefi.io/accounts/new-api-key"
  method := "GET"

  client := &http.Client{}
  req, err := http.NewRequest(method, url, nil)
  if err != nil {
    fmt.Println(err)
    return
  }
  req.Header.Add("X-API-KEY", "<your_current_api_key>")

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
  "api_key": "dk_live_abc123def456ghi789jkl012mno345",
  "created_at": "2024-01-01T00:00:00Z"
}
```

---

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| api_key | string | The new API key. Store this securely - it cannot be retrieved again. |
| created_at | string | ISO 8601 timestamp when the API key was created |

---

## Important Notes

{% hint style="warning" %}
**Security Warning:** 
- Store your API key securely. It cannot be retrieved after creation.
- Creating a new API key will invalidate your previous API key.
- Never share your API key or commit it to version control.
{% endhint %}

{% hint style="info" %}
**Authentication:** You can authenticate this request using either:
- Your current API key in the `X-API-KEY` header
- A valid JWT token from the [Sign In](signin.md) endpoint
{% endhint %}

---

## Related Endpoints

- [Sign In](signin.md) - Get a JWT token for initial authentication
- [Get API Key](get-spot-account.md) - Retrieve your existing API key (masked)
