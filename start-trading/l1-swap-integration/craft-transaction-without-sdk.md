# Craft Transaction without SDK

### Create Swap Intent

Building a swap intent is straightforward - you just need to create a transaction output at the swap intent script address, locking `fromAmount + deposit` with a valid `SwapIntentDatum`.

<table><thead><tr><th width="161.8687744140625">Network</th><th>Address (to deposit and place swap intent)</th></tr></thead><tbody><tr><td>Mainnet</td><td><code>addr1zyjg3n7aut48cgfy8s974uc79sfm985jvlend7nng9cq5ekll0mlqdcg2cee0s4ea9vaa9u79xmftptm8akvk55yslks48uca3</code></td></tr><tr><td>Preprod</td><td><code>addr_test1zrulf7dqhh92neevg7rlx64029fqy3yk750pwwqrc9hvdwkll0mlqdcg2cee0s4ea9vaa9u79xmftptm8akvk55yslksh40p2w</code></td></tr></tbody></table>

{% hint style="warning" %}
Minimum Order Value: Order value must be at least 10 USDM / USDCx equivalent.
{% endhint %}

#### SwapIntentDatum Structure

```rust
// Aiken
pub type SwapIntentDatum {
  account_address: Address, // User's address to receive output tokens
  from_amount: MValue, // Assets user is selling
  to_amount: MValue, // Minimum assets user expects to receive
  created_at: Int, // Slot number (used for cancellation timing)
  deposit: Lovelace, // Min UTxO deposit in lovelace (typically 2000000)
}

pub type MValue = Pairs<PolicyId, Pairs<AssetName, Int>>
```

```typescript
// Type definition (imported from @meshsdk/core)
type SwapIntentDatum = ConStr0<
  [
    PubKeyAddress | ScriptAddress, // account_address
    Pairs<PolicyId, Pairs<AssetName, Integer>>, // from_amount (MValue)
    Pairs<PolicyId, Pairs<AssetName, Integer>>, // to_amount (MValue)
    Integer, // created_at (slot)
    Lovelace, // deposit
  ]
>;

// Constructor function that builds a SwapIntentDatum for on-chain storage
const datum = swapIntentDatum({
  accountAddress: "addr_test1...",
  fromAmount: [{ unit: config.tokens.night, quantity: "100000000" }],
  toAmount: [{ unit: config.tokens.usdm, quantity: "5000000" }],
  createdAt: 12345678,
  deposit: 2000000, // optional, default 2 ADA
});
```

#### The transaction must

1. Create output at swap intent script address with:
   * Value: `fromAmount + deposit`
   * Inline datum: `SwapIntentDatum`

#### Example Datum

* SELL 50 ADA for 12.5 USDCx

```json
{
  "accountAddress": "addr_test1...",
  "fromAmount": [{ "unit": "lovelace", "quantity": "50000000" }],
  "toAmount": [{ "unit": "c69b981db7a65e339a6d783755f85a2e03afa1cece9714c55fe4c9135553444d", "quantity": "12500000" }],
  "createdAt": 12345678,
  "deposit": 2000000
}
```

* BUY 60 ADA with 15 USDCx

```json
{
  "accountAddress": "addr_test1...",
  "fromAmount": [{ "unit": "c69b981db7a65e339a6d783755f85a2e03afa1cece9714c55fe4c9135553444d", "quantity": "15000000" }],
  "toAmount": [{ "unit": "lovelace", "quantity": "60000000" }],
  "createdAt": 12345678,
  "deposit": 2000000
}
```

***

### Cancel Swap Intent

Cancellation is only allowed after the intent expires (\~10 minutes from `createdAt`).

{% hint style="warning" %}
Cancellation Timing: Users can only cancel their swap intent 10+ minutes after creation.
{% endhint %}

#### CancelIntent Redeemer

```rust
// Aiken
pub type SpendRedeemer {
  ProcessSwap
  CancelIntent
  SpamPrevention
}
```

```typescript
// Type definition (imported from @meshsdk/core)
export type CancelIntent = ConStr1<[]>;

// Constructor function that builds a CancelIntent
const redeemer = cancelIntent();
```

#### The transaction must

1. Reference the oracle UTxO (read-only)
2. Spend the swap intent UTxO with redeemer `CancelIntent`
3. Set `invalidBefore` to `createdAt + 600` slot (\~10 minutes)
4. Either
   * Must set `extra_signatories` with `accountAddress`'s payment key hash, OR
   * Input value sent back to `accountAddress`
