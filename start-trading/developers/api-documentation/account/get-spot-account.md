# Get spot account

Manage your DeltaDeFi spot trading account. A spot account is required for trading and holds your encrypted operation key.

***

{% openapi-operation spec="V13" path="/accounts/spot-account" method="get" %}
[OpenAPI V13](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/146df47964f80e2dc987856ffff1fb5c47812bac51e24beb8afdb298326dded0.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260113%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260113T055623Z&X-Amz-Expires=172800&X-Amz-Signature=60d61b555ff02929555f058b130b5d28c93e8e13e28b2170e4b7b432de3f1326&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

## Understanding Operation Keys

The operation key is a crucial security component:

* **Generated client-side**: Never sent to the server in plain text
* **Encrypted with your password**: Uses AES-GCM encryption
* **Used for signing trades**: Authorizes trading operations without your master wallet

{% hint style="warning" %}
The encrypted operation key is stored on DeltaDeFi's servers, but only you can decrypt it with your password. Never share your password or unencrypted operation key.
{% endhint %}
