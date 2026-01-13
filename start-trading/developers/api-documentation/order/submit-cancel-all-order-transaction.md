# Submit cancel all order transaction

{% hint style="warning" %}
**Deprecated:** This endpoint no longer exists. The cancel all orders flow has been simplified.
{% endhint %}

The build/submit pattern for cancelling all orders has been replaced with a single direct cancel endpoint.

Please use the new [Cancel All Orders](build-cancel-all-order-transaction.md) endpoint instead:

```
POST /order/cancel-all
```

This new endpoint cancels all orders for a symbol directly without requiring a separate submit step.
