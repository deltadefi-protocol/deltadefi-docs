# Spot Account

Manage your DeltaDeFi spot trading account. A spot account is required for trading and holds your encrypted operation key.

---

## Get Spot Account

Get spot account details for the authenticated user.

{% tabs %}
{% tab title="Curl" %}
```sh
curl --location 'https://api.deltadefi.io/accounts/spot-account' \
--header 'X-API-KEY: <your_api_key>'
```
{% endtab %}

{% tab title="NodeJs (axios)" %}
```javascript
const axios = require('axios');

let config = {
  method: 'get',
  maxBodyLength: Infinity,
  url: 'https://api.deltadefi.io/accounts/spot-account',
  headers: { 
    'X-API-KEY': '<your_api_key>'
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
  url := "https://api.deltadefi.io/accounts/spot-account"
  method := "GET"

  client := &http.Client{}
  req, err := http.NewRequest(method, url, nil)
  if err != nil {
    fmt.Println(err)
    return
  }
  req.Header.Add("X-API-KEY", "<your_api_key>")

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
  "account_id": "550e8400-e29b-41d4-a716-446655440000",
  "account_type": "spot",
  "created_at": "2024-01-01T00:00:00Z",
  "encrypted_operation_key": "encrypted_key_data...",
  "operation_key_hash": "abc123..."
}
```

---

## Create Spot Account

Create a new spot account for the authenticated user. This is required during onboarding after the first sign-in.

{% tabs %}
{% tab title="Curl" %}
```sh
curl --location 'https://api.deltadefi.io/accounts/spot-account' \
--header 'X-API-KEY: <your_api_key>' \
--header 'Content-Type: application/json' \
--data '{
    "user_id": "550e8400-e29b-41d4-a716-446655440000",
    "operation_key_hash": "abc123...",
    "encrypted_operation_key": "encrypted_key_data...",
    "is_script_operation_key": false
}'
```
{% endtab %}

{% tab title="NodeJs (axios)" %}
```javascript
const axios = require('axios');
let data = JSON.stringify({
  "user_id": "550e8400-e29b-41d4-a716-446655440000",
  "operation_key_hash": "abc123...",
  "encrypted_operation_key": "encrypted_key_data...",
  "is_script_operation_key": false
});

let config = {
  method: 'post',
  maxBodyLength: Infinity,
  url: 'https://api.deltadefi.io/accounts/spot-account',
  headers: { 
    'X-API-KEY': '<your_api_key>', 
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
  url := "https://api.deltadefi.io/accounts/spot-account"
  method := "POST"

  payload := strings.NewReader(`{
    "user_id": "550e8400-e29b-41d4-a716-446655440000",
    "operation_key_hash": "abc123...",
    "encrypted_operation_key": "encrypted_key_data...",
    "is_script_operation_key": false
}`)

  client := &http.Client{}
  req, err := http.NewRequest(method, url, payload)
  if err != nil {
    fmt.Println(err)
    return
  }
  req.Header.Add("X-API-KEY", "<your_api_key>")
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
  "account_id": "550e8400-e29b-41d4-a716-446655440000",
  "account_type": "spot",
  "created_at": "2024-01-01T00:00:00Z",
  "encrypted_operation_key": "encrypted_key_data...",
  "operation_key_hash": "abc123..."
}
```

### Request Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| user_id | string | Yes | User ID from sign-in response |
| operation_key_hash | string | Yes | Hash of the operation key |
| encrypted_operation_key | string | Yes | Operation key encrypted with user's password |
| is_script_operation_key | boolean | Yes | Whether the operation key is a script key |
| referral_code | string | No | Optional referral code |

---

## Update Spot Account

Update the spot account's operation key. This is useful when rotating keys for security.

{% tabs %}
{% tab title="Curl" %}
```sh
curl --location --request PUT 'https://api.deltadefi.io/accounts/spot-account' \
--header 'X-API-KEY: <your_api_key>' \
--header 'Content-Type: application/json' \
--data '{
    "user_id": "550e8400-e29b-41d4-a716-446655440000",
    "encrypted_operation_key": "new_encrypted_key_data..."
}'
```
{% endtab %}

{% tab title="NodeJs (axios)" %}
```javascript
const axios = require('axios');
let data = JSON.stringify({
  "user_id": "550e8400-e29b-41d4-a716-446655440000",
  "encrypted_operation_key": "new_encrypted_key_data..."
});

let config = {
  method: 'put',
  maxBodyLength: Infinity,
  url: 'https://api.deltadefi.io/accounts/spot-account',
  headers: { 
    'X-API-KEY': '<your_api_key>', 
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
  url := "https://api.deltadefi.io/accounts/spot-account"
  method := "PUT"

  payload := strings.NewReader(`{
    "user_id": "550e8400-e29b-41d4-a716-446655440000",
    "encrypted_operation_key": "new_encrypted_key_data..."
}`)

  client := &http.Client{}
  req, err := http.NewRequest(method, url, payload)
  if err != nil {
    fmt.Println(err)
    return
  }
  req.Header.Add("X-API-KEY", "<your_api_key>")
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
  "account_id": "550e8400-e29b-41d4-a716-446655440000",
  "account_type": "spot",
  "created_at": "2024-01-01T00:00:00Z",
  "updated_at": "2024-01-02T00:00:00Z",
  "encrypted_operation_key": "new_encrypted_key_data...",
  "operation_key_hash": "abc123..."
}
```

### Request Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| user_id | string | Yes | User ID |
| encrypted_operation_key | string | Yes | New encrypted operation key |

---

## Understanding Operation Keys

The operation key is a crucial security component:

- **Generated client-side**: Never sent to the server in plain text
- **Encrypted with your password**: Uses AES-GCM encryption
- **Used for signing trades**: Authorizes trading operations without your master wallet

{% hint style="warning" %}
The encrypted operation key is stored on DeltaDeFi's servers, but only you can decrypt it with your password. Never share your password or unencrypted operation key.
{% endhint %}
