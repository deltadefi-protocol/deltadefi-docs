# Create new api key

Create a new API key for programmatic access to the DeltaDeFi trading API. API keys provide a more permanent authentication method compared to JWT tokens.

***

{% openapi-operation spec="V13" path="/accounts/new-api-key" method="get" %}
[OpenAPI V13](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/146df47964f80e2dc987856ffff1fb5c47812bac51e24beb8afdb298326dded0.json?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260113%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260113T061700Z&X-Amz-Expires=172800&X-Amz-Signature=00d2e7544274011ea4c82020135d2ddeeede9898b97ebef7d5a557bec017afbe&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

## Important Notes

{% hint style="warning" %}
**Security Warning:**

* Creating a new API key will invalidate your previous API key.
* Never share your API key or commit it to version control.
{% endhint %}

{% hint style="info" %}
**Authentication:** You can authenticate this request using:

* Your current API key in the `X-API-KEY` header
{% endhint %}

