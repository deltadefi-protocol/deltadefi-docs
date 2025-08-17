# Auth

Access to all our APIs requires an API key obtained from the dashboard.&#x20;

Simply connect your wallet and navigate to the Dashboard page.

<figure><img src="../../../.gitbook/assets/CleanShot 2025-03-21 at 12.02.48.png" alt=""><figcaption></figcaption></figure>

This key must be included in the headers as "X-API-KEY" for authentication.

```sh
// Example snippet

curl --location 'https://api-dev.deltadefi.io' \
--header 'X-API-KEY: 4125f1d710037fd548a36123cf6dc63d'
```
