# Getting started

1. Connect Wallet and retrieve your api key [auth.md](../auth.md "mention")
2. Test API connection

{% tabs %}
{% tab title="curl" %}
```powershell
curl --location 'https://api.deltadefi.io/accounts/balance' \
--header 'X-API-KEY: <your_api_key>'
```

A successful response should return an empty array with a status code <kbd><mark style="color:green;">200<mark style="color:green;"></kbd>

```
[]
```
{% endtab %}
{% endtabs %}
