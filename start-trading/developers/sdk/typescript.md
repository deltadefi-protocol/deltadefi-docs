# Typescript

### About

DeltaDeFi's Typescript SDK provides utility functions to interact with the API service and sign transactions with provided keys.

### Installation

The SDK is hosted on npmjs.com, so you can directly import it using your favorite package manager.

```
npm i @deltadefi-protocol/typescript-sdk
```

```
yarn add @deltadefi-protocol/typescript-sdk
```

### Getting Started

Placing and canceling orders are as simple as below.

```typescript
import { AppWalletKeyType } from '@meshsdk/core';
import { ApiClient } from '@deltadefi-protocol/typescript-sdk';

// Obtain your API key through DeltaDeFi dashboard
const apiKey = process.env.API_KEY || '';

// Loading the wallet with seed phrase (same as your account obtaining API key)
// Documentation - https://meshjs.dev/apis/appwallet
const signingKey: AppWalletKeyType = {
    type: 'mnemonic',
    words: (process.env.MNEMONIC || '').split(',') || [],
};

// Initializing programmatic API client
const api = new ApiClient({ apiKey, signingKey, network: 'preprod' });
```

### Posting Order

```typescript
// Posting order instantly without fee
const buildRes = await api.postOrder({
    pair: 'ADAUSDX',
    side: 'sell',
    type: 'limit',
    quantity: 1000_000_000,
    price: 0.62,
});
```

### Cancel Order

<pre class="language-typescript"><code class="lang-typescript">// Canceling order instantly without fee
<strong>const cancelRes = await api.orders.cancelOrder(buildRes.order.order_id);
</strong>console.log('cancel order response', cancelRes);
</code></pre>



### Note

Current seed phrase wallet loading supports only the first account's first address (i.e. `m/1852'/1815'/0'/0/0` when you check inside your browser wallet), for example in Eternl's single address mode:

<figure><img src="../../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

If you are looking to connect a more dynamic account, please get in touch with the team for support.
