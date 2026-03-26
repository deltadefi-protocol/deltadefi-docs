# Integration APIs

DeltaDeFi hosts official APIs to improve accessibility of the L1 swap contracts. The entire swap is still mostly handled through Aiken smart contract, the API provides additional information to facilitate informed trading decisions. These endpoints are designed for aggregators integrating with DeltaDeFi's L1 swap infrastructure. All endpoints listed below are public and do not require API key authentication.

### URL

| Environment | URL Endpoint |
|---|---|
| Pre-Prod | `https://operator-staging.deltadefi.io` |
| Mainnet | TBC |

***

### GET /swapIntent/depth/{symbol}

Get the current market depth for a trading pair post fee. The `price` shown in depth response has already factored in fees — it is exactly what you could expect to trade at.

{% hint style="info" %}
This endpoint uses internal symbol names (e.g. `ADAUSDM`, `NIGHTUSDM`, `NIGHTADA`), not the aggregator-facing `USDCx` symbols from `/pairs`.
{% endhint %}

#### Example Request

```
GET /swapIntent/depth/NIGHTUSDM
```

#### Example Response

```json
{
  "timestamp": 1773113131587,
  "bids": [
    { "price": "0.05090", "quantity": "31395" }
  ],
  "asks": [
    { "price": "0.05311", "quantity": "3977.5" },
    { "price": "0.05210", "quantity": "6220" }
  ]
}
```

#### Response Fields

| Field | Type | Description |
|---|---|---|
| timestamp | number | Unix timestamp in milliseconds |
| bids | array | Buy orders — price/quantity objects sorted by descending price |
| asks | array | Sell orders — price/quantity objects sorted by ascending price |

#### Supported Symbols

| Symbol | Type | Description |
|---|---|---|
| `ADAUSDM` | Direct | ADA/USDM pair — 0.2% spread (0.1% trading + 0.1% operator) |
| `NIGHTUSDM` | Direct | NIGHT/USDM pair — 0.2% spread |
| `NIGHTADA` | Cross-pair | Synthetic depth from NIGHTUSDM + ADAUSDM — 0.4% spread (0.2% trading + 0.2% operator) |

***

### GET /pairs

Get the list of supported trading pairs. Use this to understand which pairs are available for integration.

#### Example Request

```
GET /pairs
```

#### Example Response

```json
{
  "pairs": [
    {
      "symbol": "ADAUSDCx",
      "baseToken": "ADA",
      "baseTokenUnit": "lovelace",
      "quoteToken": "USDCx",
      "quoteTokenUnit": "c48f0767b34514e550c04de081673e370e87bf00e6cc0e831a0e4592...",
      "priceDp": 4,
      "quantityDp": 1
    },
    {
      "symbol": "NIGHTUSDCx",
      "baseToken": "NIGHT",
      "baseTokenUnit": "ab4a4f5508ced3e2a8a63770a1355c4830d66ab061",
      "quoteToken": "USDCx",
      "quoteTokenUnit": "c48f0767b34514e550c04de081673e370e87bf00e6cc0e831a0e4592...",
      "priceDp": 5,
      "quantityDp": 1
    },
    {
      "symbol": "NIGHTADA",
      "baseToken": "NIGHT",
      "baseTokenUnit": "ab4a4f5508ced3e2a8a63770a1355c4830d66ab061",
      "quoteToken": "ADA",
      "quoteTokenUnit": "lovelace",
      "priceDp": 3,
      "quantityDp": 1
    }
  ]
}
```

#### Response Fields

| Field | Type | Description |
|---|---|---|
| pairs | array | List of supported trading pairs |
| pairs[].symbol | string | Trading pair symbol used across APIs |
| pairs[].baseToken | string | Human-readable base token name |
| pairs[].baseTokenUnit | string | On-chain unit identifier (policyId + asset name) for the base token |
| pairs[].quoteToken | string | Human-readable quote token name |
| pairs[].quoteTokenUnit | string | On-chain unit identifier (policyId + asset name) for the quote token |
| pairs[].priceDp | number | Decimal places for price display |
| pairs[].quantityDp | number | Decimal places for quantity display |

***

### GET /orders/{txHash}/{outputIndex}

Get the status of a swap intent order by its UTxO reference. The UTxO reference is split into path segments (instead of `txHash#outputIndex`) to avoid URL encoding issues.

#### Example Request

```
GET /orders/a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2/0
```

#### Example Response — On Book

An order that is on-chain at the swap intent script address, waiting to be processed.

```json
{
  "txHash": "a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2",
  "outputIndex": 0,
  "status": "on_book",
  "order": {
    "side": "buy",
    "symbol": "ADAUSDCx",
    "fromAmount": [{ "unit": "c48f0767b...", "quantity": "5000000" }],
    "toAmount": [{ "unit": "lovelace", "quantity": "15000000" }],
    "price": "0.3520"
  },
  "expiryTime": 1773113731587
}
```

#### Example Response — Processing

The operator is actively settling this order.

```json
{
  "txHash": "a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2",
  "outputIndex": 0,
  "status": "processing"
}
```

#### Example Response — Expired

The order is still on-chain but has passed the 600-slot (~10 minute) expiry window and is eligible for cancellation.

```json
{
  "txHash": "a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2",
  "outputIndex": 0,
  "status": "expired",
  "order": {
    "side": "sell",
    "symbol": "NIGHTUSDCx",
    "fromAmount": [{ "unit": "ab4a4f55...", "quantity": "50000000" }],
    "toAmount": [{ "unit": "c48f0767b...", "quantity": "2500000" }],
    "price": "0.05100"
  },
  "expiryTime": 1773113731587
}
```

#### Example Response — Completed

The order was successfully processed. This status is available for up to 1 hour after settlement.

```json
{
  "txHash": "a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2",
  "outputIndex": 0,
  "status": "completed",
  "settlementTxHash": "f7e8d9c0b1a2f7e8d9c0b1a2f7e8d9c0b1a2f7e8d9c0b1a2f7e8d9c0b1a2f7e8"
}
```

#### Example Response — Not Found

The order does not exist, was already spent, or completed more than 1 hour ago.

```
HTTP 404
```

```json
{
  "error": "ORDER_NOT_FOUND"
}
```

#### Response Fields

| Field | Type | Description |
|---|---|---|
| txHash | string | Transaction hash of the swap intent UTxO |
| outputIndex | number | Output index of the swap intent UTxO |
| status | string | Order status: `on_book`, `processing`, `expired`, or `completed` |
| order | object | Order details (present for `on_book` and `expired` statuses) |
| order.side | string | `buy` or `sell` |
| order.symbol | string | Trading pair symbol (e.g. `ADAUSDCx`) |
| order.fromAmount | array | Assets being swapped from (on-chain format: unit + quantity) |
| order.toAmount | array | Minimum assets expected to receive (on-chain format: unit + quantity) |
| order.price | string | Effective price (quote per base) |
| expiryTime | number | Unix timestamp in milliseconds when the order becomes cancellable (present for `on_book` and `expired`) |
| settlementTxHash | string | Transaction hash of the settlement (present for `completed` status only) |

#### Order Status Lifecycle

| Status | Description |
|---|---|
| `on_book` | Order is on-chain at the script address, within the 10-minute validity window |
| `processing` | Operator has claimed the order and is actively settling it on L2 |
| `expired` | Order is on-chain but past the 10-minute validity window; eligible for cancellation |
| `completed` | Order was successfully settled (visible for up to 1 hour after settlement) |

***

### POST /cancel/build

Build a cancel transaction for a swap intent order. This immediately reserves the order so the swap processor will not attempt to fill it, preventing contention.

The cancel transaction can be built at any time, but the on-chain submission will only succeed after the order's 10-minute expiry window has passed (enforced by the Plutus smart contract).

#### Example Request

```
POST /cancel/build
Content-Type: application/json
```

```json
{
  "txHash": "a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2",
  "outputIndex": 0
}
```

#### Example Response

```json
{
  "txHex": "84a400818258..."
}
```

#### Request Fields

| Field | Type | Description |
|---|---|---|
| txHash | string | Transaction hash of the swap intent UTxO (64-character hex) |
| outputIndex | number | Output index of the swap intent UTxO (non-negative integer) |

#### Response Fields

| Field | Type | Description |
|---|---|---|
| txHex | string | Unsigned transaction CBOR hex. Sign this with the user's wallet before submitting. |

#### Error Responses

| Status | Error | Description |
|---|---|---|
| 400 | Swap intent UTxO not found on-chain | The UTxO does not exist at the script address |
| 400 | Invalid swap intent datum | The UTxO does not contain a valid swap intent |
| 400 | Swap intent is already being processed | Another process (swap or cancel) has already claimed this UTxO |
| 422 | Validation error | Invalid txHash or outputIndex format |

***

### POST /cancel/submit

Submit a signed cancel transaction. The operator co-signs the transaction and submits it to the Cardano network. The transaction will be rejected on-chain if the 10-minute expiry window has not yet passed.

#### Example Request

```
POST /cancel/submit
Content-Type: application/json
```

```json
{
  "signedTx": "84a400818258..."
}
```

#### Example Response

```json
{
  "txHash": "f7e8d9c0b1a2f7e8d9c0b1a2f7e8d9c0b1a2f7e8d9c0b1a2f7e8d9c0b1a2f7e8"
}
```

#### Request Fields

| Field | Type | Description |
|---|---|---|
| signedTx | string | User-signed transaction CBOR hex from the build step |

#### Response Fields

| Field | Type | Description |
|---|---|---|
| txHash | string | Confirmed transaction hash of the cancel transaction |

#### Error Responses

| Status | Error | Description |
|---|---|---|
| 400 | No cancel build found | Must call `/cancel/build` first to build the transaction |
| 400 | Cancel transaction not confirmed | Transaction was submitted but not confirmed on-chain |
| 422 | Validation error | Invalid signedTx format |

***

### Cancel Flow

There are two ways to cancel a swap intent:

#### Option 1: API Flow (before or after expiry)

Use this to **reserve** the order immediately — the operator will stop trying to process it while you wait for the expiry window.

1. **Build** — Call `POST /cancel/build` with the UTxO reference. This reserves the order so it will not be processed by the swap operator.
2. **Sign** — Sign the returned `txHex` with the user's wallet (the wallet that created the swap intent).
3. **Submit** — Call `POST /cancel/submit` with the signed transaction. The operator co-signs and submits to the network.
4. **Confirmation** — The operator waits for on-chain confirmation and returns the confirmed transaction hash.

{% hint style="info" %}
You can build the cancel transaction before the expiry window passes, but the on-chain submission will only succeed after ~10 minutes from order creation. This allows you to prepare the cancellation in advance and guarantee the operator will not fill the order in the meantime.
{% endhint %}

#### Option 2: Self-service (after expiry only)

Once the 10-minute expiry window has passed, you can cancel directly by crafting your own transaction — no API call needed. The Plutus smart contract allows the original sender to cancel after `createdAt + 600` slots. See [Craft Transaction without SDK](craft-transaction-without-sdk.md) for details.

{% hint style="warning" %}
With self-service cancellation there is no reservation — the operator may still attempt to process the order if it hasn't expired yet. Use the API flow if you need to guarantee the order won't be filled.
{% endhint %}
