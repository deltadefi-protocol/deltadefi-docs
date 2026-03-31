# Trade

DeltaDeFi offers spot trading on an order-book model, powered by Hydra L2 for near-instant execution.

## Key specs

| Metric | Value |
|--------|-------|
| Avg confirmation | ~50ms on Hydra L2 |
| Trading fee | 0.10% flat (10bps) |
| Gas fees | None |
| Spread vs AMM | ~5–6x tighter |
| Cost per $1K trade | ~$1.40 (vs ~$8.50 on AMM) |
| Custody | Non-custodial, L1 settlement guarantee |

## How it works

1. **Connect wallet** — Create a DeltaDeFi account linked to your Cardano wallet address.
2. **Deposit** — Transfer ADA or supported tokens into your trading account.
3. **Trade** — Place limit or market orders on the order book. Orders are matched on Hydra L2 with sub-second confirmation.
4. **Withdraw** — Move funds back to Cardano L1 at any time.

All trades happen on Hydra L2, giving you centralized-exchange speed without giving up custody of your assets.

## Order types

See [Order Types](order-types.md) for details on supported order types including limit orders and market orders.

## API access

DeltaDeFi provides a Binance-compatible REST + WebSocket API for programmatic trading. See [Developers](../../../start-trading/developers/) for full API documentation and SDKs in TypeScript, Python, Rust, and Go.
