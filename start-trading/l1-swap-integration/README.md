---
icon: arrows-rotate-reverse
---

# L1 Swap Integration

DeltaDeFi is a L2 protocol that operates in Hydra head. Therefore, a typical user cannot access to DeltaDeFi's liquidity with their L1 wallet. In order to improve accessibility of DeltaDeFi's liquidity, we have implemented a liquidity bridge pattern to allow placing a direct swap in Cardano L1.

<figure><img src="../../.gitbook/assets/image (197).png" alt=""><figcaption></figcaption></figure>

### Who should use this?

* DEX aggregator - this pattern primarily serves DEX aggregator. With the L1 swap infrastructure, it makes integration seamless. DeltaDeFi can be seen as a typical L1 exchange in the integration work.
* Cardano programmatic trader / arbitrageur - the swap allows direct L1 programmatic access to DeltaDeFi's liquidity pool trading strategies to include DeltaDeFi's order book at ease

{% hint style="info" %}
Test Tokens: Request test USDCx and NIGHT tokens for preprod at https://alpha-app.deltadefi.io/testing-usd-request
{% endhint %}

***
