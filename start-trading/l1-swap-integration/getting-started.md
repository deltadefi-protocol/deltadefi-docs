# Getting Started

### Configuration

```
npm install @deltadefi-protocol/khor@1.0.6
```

Obtain constants for creating transactions

```typescript
import { BlockfrostProvider, MeshWallet } from "@meshsdk/core";
import { KhorConstants, SwapIntentTx } from "@deltadefi-protocol/khor";

// Setup
const blockfrost = new BlockfrostProvider("YOUR_BLOCKFROST_API_KEY");
const wallet = new MeshWallet({
  networkId: 0,
  fetcher: blockfrost,
  submitter: blockfrost,
  key: { type: "mnemonic", words: "your 24 words here".split(" ") },
});

// Get all required variables
const userAddress = await wallet.getChangeAddress();
const utxos = await wallet.getUtxos();
const collateral = (await wallet.getCollateral())[0];

// Create swap intent
const config = new KhorConstants("preprod");
const swapIntentTx = new SwapIntentTx(config);
```

### Create Swap Intent

Create a new swap intent to place a limit order on L1.

{% hint style="warning" %}
Minimum Order Value: Order value must be at least 10 USDCx equivalent.
{% endhint %}

```typescript
const result = await swapIntentTx.createSwapIntent(
  {
    utxos,
    collateral,
    changeAddress: userAddress,
    accountAddress: userAddress,
    fromAmount: [{ unit: config.tokens.usdm, quantity: "100000000" }], // 100 NIGHT
    toAmount: [{ unit: config.tokens.usdm, quantity: "5000000" }], // 5 USDCx
    // Optional parameters:
    // deposit: 2_000_000,        // default: 2 ADA
    // expiry: 10 * 60 * 1000,    // default: 10 mins (in milliseconds)
  },
  blockfrost
);

// Sign and submit
const signedTx = await wallet.signTx(result.txHex);
const txHash = await wallet.submitTx(signedTx);
```

### Cancel Swap Intent

Cancel an existing swap intent and reclaim locked assets.

{% hint style="warning" %}
Cancellation Timing: Users can only cancel their swap intent 10+ minutes after creation.
{% endhint %}

```typescript
// Get user's swap intents
const myIntents = await swapIntentTx.fetchSwapIntentUtxosByAddress(blockfrost, userAddress);
const intentToCancel = myIntents[0];

// Check if cancellable
if (!swapIntentTx.isCancellable(intentToCancel)) {
  const cancellableAt = swapIntentTx.getCancellableAt(intentToCancel);
  throw new Error(`Intent not cancellable yet. Try again at ${new Date(cancellableAt!)}`);
}

// Cancel swap intent
const result = await swapIntentTx.cancelSwapIntent(
  {
    utxos,
    collateral,
    changeAddress: userAddress,
    oracleUtxo: config.oracleUtxo,
    swapIntentUtxo: intentToCancel,
  },
  blockfrost
);

// Sign and submit
const signedTx = await wallet.signTx(result.txHex);
const txHash = await wallet.submitTx(signedTx);
```

### Open Source

The full Aiken contract that processed the swap and its off-chain SDK can be accessed at [https://github.com/deltadefi-protocol/khor](https://github.com/deltadefi-protocol/khor).

Network parameters and constants can also be found in the SDK.



### Supported Pairs

* `ADAUSDCx`
* `NIGHTUSDCx`
* `NIGHTADA`
