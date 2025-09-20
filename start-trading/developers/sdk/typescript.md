# Typescript

### About

DeltaDeFi's Typescript SDK provides utility functions to interact with the API service and sign transactions with provided keys.

### Installation

The SDK is hosted on npmjs.com, so you can directly import it using your favorite package manager.

```
npm i @deltadefi-protocol/sdk
```

```
yarn add @deltadefi-protocol/sdk
```

### Getting Started

Placing and canceling orders are as simple as below.

```typescript
import { ApiClient } from "@deltadefi-protocol/sdk";

export const getApiClient = async (): Promise<ApiClient> => {
  const network = process.env.NETWORK;
  const apiKey = process.env.API_KEY;
  const operationKeyEncryptionPassword =
    process.env.OPERATION_KEY_ENCRYPTION_PASSWORD!;

  const apiClient = new ApiClient({
    network: network as "preprod" | "mainnet",
    apiKey: apiKey,
  });

  await apiClient.loadOperationKey(operationKeyEncryptionPassword);
  return apiClient;
};
```

### Posting Order

```typescript
// Posting order instantly without fee
export const orders = async () => {
  const apiClient = await getApiClient();

  const orderRequest: PostOrderRequest = {
    symbol: "ADAUSDM",
    side: "sell",
    type: "limit",
    quantity: 100,
    price: 16,
  };

  const res = await apiClient.postOrder(orderRequest);
  console.log("Post Order Response:", res);
};

```

### Cancel Order

```typescript
// Canceling order instantly without fee
const cancelRes = await apiClient.cancelOrder(res.order.order_id);
console.log("Cancel Order Response:", cancelRes);
```

### Detailed SDK demo

[https://github.com/deltadefi-protocol/sdks-demo/tree/main/typescript](https://github.com/deltadefi-protocol/sdks-demo/tree/main/typescript)

