# Submit cancel order transaction

{% hint style="warning" %}
**Deprecated:** This endpoint no longer exists. The cancel order flow has been simplified.
{% endhint %}

The build/submit pattern for cancelling orders has been replaced with a single direct cancel endpoint.

Please use the new [Cancel Order](build-cancel-order-transaction.md) endpoint instead:

```
POST /order/{orderId}/cancel
```

This new endpoint cancels an order directly without requiring a separate submit step.
