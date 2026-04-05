# Integration APIs

DeltaDeFi hosts official APIs to improve accessibility of the L1 swap contracts. The entire swap is still mostly handled through Aiken smart contract, the API provides additional information to facilitate informed trading decisions. These endpoints are designed for aggregators integrating with DeltaDeFi's L1 swap infrastructure. All endpoints listed below are public and do not require API key authentication.

### URL

| Environment | URL Endpoint                            |
| ----------- | --------------------------------------- |
| Pre-Prod    | `https://operator-staging.deltadefi.io` |
| Mainnet     | `https://operator.deltadefi.io`         |

***

### GET - Market Depth

Get the current market depth for a trading pair post fee. The `price` shown in depth response has already factored in fees — it is exactly what you could expect to trade at.

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

| Field     | Type   | Description                                                    |
| --------- | ------ | -------------------------------------------------------------- |
| timestamp | number | Unix timestamp in milliseconds                                 |
| bids      | array  | Buy orders — price/quantity objects sorted by descending price |
| asks      | array  | Sell orders — price/quantity objects sorted by ascending price |

#### Supported Symbols

| Symbol      | Type       | Description                                                                           |
| ----------- | ---------- | ------------------------------------------------------------------------------------- |
| `ADAUSDCx`  | Direct     | ADA/USDC pair — 0.2% spread (0.1% trading + 0.1% operator)                            |
| `NIGHTUSDM` | Direct     | NIGHT/USDC pair — 0.2% spread                                                         |
| `ADANIGHT`  | Cross-pair | Synthetic depth from NIGHTUSDC + ADAUSDC — 0.4% spread (0.2% trading + 0.2% operator) |

***

### GET - Supported Pairs

Get the list of supported trading pairs. Use this to understand which pairs are available for integration.

#### Example Request

```
GET /pairs
```

#### Example Response

```json
[6:44 PM]{
    "pairs": [
        {
            "symbol": "ADAUSDM",
            "baseToken": "ADA",
            "baseTokenUnit": "lovelace",
            "quoteToken": "USDM",
            "quoteTokenUnit": "c48cbb3d5e57ed56e276bc45f99ab39abe94e6cd7ac39fb402da47ad0014df105553444d",
            "priceDp": 4,
            "quantityDp": 1
        },
        {
            "symbol": "NIGHTUSDM",
            "baseToken": "NIGHT",
            "baseTokenUnit": "0691b2fecca1ac4f53cb6dfb00b7013e561d1f34403b957cbb5af1fa4e49474854",
            "quoteToken": "USDM",
            "quoteTokenUnit": "c48cbb3d5e57ed56e276bc45f99ab39abe94e6cd7ac39fb402da47ad0014df105553444d",
            "priceDp": 5,
            "quantityDp": 1
        },
        {
            "symbol": "ADAUSDCx",
            "baseToken": "ADA",
            "baseTokenUnit": "lovelace",
            "quoteToken": "USDCx",
            "quoteTokenUnit": "1f3aec8bfe7ea4fe14c5f121e2a92e301afe414147860d557cac7e345553444378",
            "priceDp": 4,
            "quantityDp": 1
        },
        {
            "symbol": "ADANIGHT",
            "baseToken": "ADA",
            "baseTokenUnit": "lovelace",
            "quoteToken": "NIGHT",
            "quoteTokenUnit": "0691b2fecca1ac4f53cb6dfb00b7013e561d1f34403b957cbb5af1fa4e49474854",
            "priceDp": 3,
            "quantityDp": 1
        }
    ]
}
```

#### Response Fields

| Field                   | Type   | Description                                                          |
| ----------------------- | ------ | -------------------------------------------------------------------- |
| pairs                   | array  | List of supported trading pairs                                      |
| pairs\[].symbol         | string | Trading pair symbol used across APIs                                 |
| pairs\[].baseToken      | string | Human-readable base token name                                       |
| pairs\[].baseTokenUnit  | string | On-chain unit identifier (policyId + asset name) for the base token  |
| pairs\[].quoteToken     | string | Human-readable quote token name                                      |
| pairs\[].quoteTokenUnit | string | On-chain unit identifier (policyId + asset name) for the quote token |
| pairs\[].priceDp        | number | Decimal places for price display                                     |
| pairs\[].quantityDp     | number | Decimal places for quantity display                                  |

***

### GET - Swap Intent UTxOs

Get all UTxOs at the swap intent script address with parsed datum information. Responses are cached for 60 seconds to reduce on-chain queries.

#### Example Request

```
GET /swapIntent/utxos
```

#### Example Response

```json
[
  {
    "tx_hash": "a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2",
    "output_index": 0,
    "address": "addr_test1wz...",
    "amount": [
      { "unit": "lovelace", "quantity": "5000000" },
      { "unit": "c48f0767b...", "quantity": "10000000" }
    ],
    "swap_intent": {
      "accountAddress": "addr_test1qz...",
      "fromAmount": [{ "unit": "c48f0767b...", "quantity": "10000000" }],
      "toAmount": [{ "unit": "lovelace", "quantity": "30000000" }],
      "createdAt": 1773113131,
      "deposit": 2000000
    },
    "is_valid": true
  },
  {
    "tx_hash": "b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3",
    "output_index": 1,
    "address": "addr_test1wz...",
    "amount": [
      { "unit": "lovelace", "quantity": "3000000" }
    ],
    "swap_intent": null,
    "is_valid": false
  }
]
```

#### Response Fields

The response is an array of UTxO objects:

| Field                          | Type        | Description                                                         |
| ------------------------------ | ----------- | ------------------------------------------------------------------- |
| tx\_hash                       | string      | Transaction hash of the UTxO                                        |
| output\_index                  | number      | Output index of the UTxO                                            |
| address                        | string      | Script address holding the UTxO                                     |
| amount                         | array       | Assets held in the UTxO (unit + quantity)                           |
| is\_valid                      | boolean     | Whether the UTxO holds sufficient value to cover `fromAmount` + deposit |
| swap\_intent                   | object/null | Parsed swap intent datum, or `null` if the datum is not parseable   |
| swap\_intent.accountAddress    | string      | Address of the account that created the swap intent                 |
| swap\_intent.fromAmount        | array       | Assets being swapped from (on-chain format: unit + quantity)        |
| swap\_intent.toAmount          | array       | Minimum assets expected to receive (on-chain format: unit + quantity)|
| swap\_intent.createdAt         | number      | Slot number when the swap intent was created                        |
| swap\_intent.deposit           | number      | Deposit amount in lovelace (optional, defaults to protocol default) |

{% hint style="info" %}
UTxOs where `swap_intent` is `null` are present at the script address but do not contain a valid swap intent datum. These can be safely ignored by integrators.
{% endhint %}

***

### GET - Order Status

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

The order is still on-chain but has passed the 600-slot (\~10 minute) expiry window and is eligible for cancellation.

```json
{
  "txHash": "a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2",
  "outputIndex": 0,
  "status": "expired",
  "order": {
    "side": "sell",
    "symbol": "NIGHTUSDM",
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

| Field            | Type   | Description                                                                                             |
| ---------------- | ------ | ------------------------------------------------------------------------------------------------------- |
| txHash           | string | Transaction hash of the swap intent UTxO                                                                |
| outputIndex      | number | Output index of the swap intent UTxO                                                                    |
| status           | string | Order status: `on_book`, `processing`, `expired`, or `completed`                                        |
| order            | object | Order details (present for `on_book` and `expired` statuses)                                            |
| order.side       | string | `buy` or `sell`                                                                                         |
| order.symbol     | string | Trading pair symbol (e.g. `ADAUSDCx`)                                                                   |
| order.fromAmount | array  | Assets being swapped from (on-chain format: unit + quantity)                                            |
| order.toAmount   | array  | Minimum assets expected to receive (on-chain format: unit + quantity)                                   |
| order.price      | string | Effective price (quote per base)                                                                        |
| expiryTime       | number | Unix timestamp in milliseconds when the order becomes cancellable (present for `on_book` and `expired`) |
| settlementTxHash | string | Transaction hash of the settlement (present for `completed` status only)                                |

#### Order Status Lifecycle

| Status       | Description                                                                         |
| ------------ | ----------------------------------------------------------------------------------- |
| `on_book`    | Order is on-chain at the script address, within the 10-minute validity window       |
| `processing` | Operator has claimed the order and is actively settling it on L2                    |
| `expired`    | Order is on-chain but past the 10-minute validity window; eligible for cancellation |
| `completed`  | Order was successfully settled (visible for up to 1 hour after settlement)          |

***

### POST - Build Cancel Order

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

| Field       | Type   | Description                                                 |
| ----------- | ------ | ----------------------------------------------------------- |
| txHash      | string | Transaction hash of the swap intent UTxO (64-character hex) |
| outputIndex | number | Output index of the swap intent UTxO (non-negative integer) |

#### Response Fields

| Field | Type   | Description                                                                        |
| ----- | ------ | ---------------------------------------------------------------------------------- |
| txHex | string | Unsigned transaction CBOR hex. Sign this with the user's wallet before submitting. |

#### Error Responses

| Status | Error                                  | Description                                                    |
| ------ | -------------------------------------- | -------------------------------------------------------------- |
| 400    | Swap intent UTxO not found on-chain    | The UTxO does not exist at the script address                  |
| 400    | Invalid swap intent datum              | The UTxO does not contain a valid swap intent                  |
| 400    | Swap intent is already being processed | Another process (swap or cancel) has already claimed this UTxO |
| 422    | Validation error                       | Invalid txHash or outputIndex format                           |

***

### POST - Submit Cancel Order

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

| Field    | Type   | Description                                          |
| -------- | ------ | ---------------------------------------------------- |
| signedTx | string | User-signed transaction CBOR hex from the build step |

#### Response Fields

| Field  | Type   | Description                                          |
| ------ | ------ | ---------------------------------------------------- |
| txHash | string | Confirmed transaction hash of the cancel transaction |

#### Error Responses

| Status | Error                            | Description                                              |
| ------ | -------------------------------- | -------------------------------------------------------- |
| 400    | No cancel build found            | Must call `/cancel/build` first to build the transaction |
| 400    | Cancel transaction not confirmed | Transaction was submitted but not confirmed on-chain     |
| 422    | Validation error                 | Invalid signedTx format                                  |

***

### Cancel Flow

1. **Build** — Call `POST /cancel/build` with the UTxO reference. This reserves the order so it will not be processed by the swap operator.
2. **Sign** — Sign the returned `txHex` with the user's wallet (the wallet that created the swap intent).
3. **Submit** — Call `POST /cancel/submit` with the signed transaction. The operator co-signs and submits to the network.
4. **Confirmation** — The operator waits for on-chain confirmation and returns the confirmed transaction hash.

{% hint style="info" %}
You can build the cancel transaction before the expiry window passes, but the submit step will only succeed on-chain after \~10 minutes from order creation. This allows you to prepare the cancellation in advance.
{% endhint %}
