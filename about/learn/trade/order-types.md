# Order Types

{% hint style="success" %}
**DeltaDeFi Protocol Supports All Possible Order Types**
{% endhint %}

DeltaDeFi can empower all order types existing in traditional finance. However, at the initial stage, we will only support limit orders and market orders.

### Limit Order

Limit orders will always execute with the limit price specified as the order maker, except in case of price crossing at the moment of order placing, where your order will be filled with a better price as an order taker.

### Market Order

Our implementation of market order is implicitly an "enhanced market order", which you can configure the maximum slippage. If there is insufficient market depth to fill all the instructed quantity within the maximum slippage, the remaining order size will be created as limit order at the market price when the order is submitted.

### Other Order Types

With current architecture, DeltaDeFi can be upgraded to support more order types. Please provide direct feedback to the team if you think any additional order type could benefit you or other potential users!
