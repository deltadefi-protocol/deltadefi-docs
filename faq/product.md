# Product

## Onboarding

<details>

<summary>Why do I have to create an account?</summary>

In DeltaDeFi, users conduct their trading on their trading accounts, which are derived from the users' wallet addresses. Therefore, the first step interacting with DeltaDeFi is indeed creating an account.

This step is indeed identical to how you interact with other Cardano DApps, where you try to connect your wallet.

</details>

<details>

<summary>Why are only limited wallets supported in the web app?</summary>

To protect users from signing malicious transactions, fellow Cardano wallets would try resolving inputs from the Cardano blockchain to display the entire transaction information to users at the time of signing. However, since DeltaDeFi conducts trades in Hydra, an L2 network, most wallets fail to resolve inputs from L1 and decide to block the transactions from being signed by users.&#x20;

Therefore, when placing trade through the web app, we can only support wallets that do not enforce the full resolution of inputs or have dedicated support for the Hydra network. Since Hydra is a relatively new technology, relatively few wallets do have the support in place and causing limited wallet support.

</details>

<details>

<summary>How exactly is my operation key generated?</summary>

All the users' operation key is generated using [Mesh SDK](https://meshjs.dev/apis/wallets/meshwallet#generateWallet), and then encrypted by the AES-GCM algorithm with an initialization vector size of 12 ([implementation](https://github.com/MeshJS/web3-sdk/blob/main/src/functions/crypto/encryption.ts#L4)). Then, in several programming languages, we have the equivalent decryption logic in:

* Typescript - [Mesh web3-sdk](https://github.com/MeshJS/web3-sdk/blob/main/src/functions/crypto/encryption.ts#L53)
* Rust - [whisky](https://github.com/sidan-lab/whisky/blob/master/packages/whisky-wallet/src/encryption/cipher.rs#L53)
* Golang - [rum](https://github.com/sidan-lab/rum/blob/main/cipher.go#L67)
* Python - [gin](https://github.com/sidan-lab/gin/blob/main/src/sidan_gin/encryption/cipher.py#L71)

Everything's open source and verifiable.

</details>

## Deposit & Withdrawal

<details>

<summary>What is the minimum amount of deposit and withdrawal?</summary>

Adhering to the Cardano blockchain protocol parameter, we enforced a minimum deposit and withdrawal of 2 ADA per transaction to ensure the minUTxO requirement is fulfilled.

</details>

<details>

<summary>How long does it take to deposit &#x26; withdraw?</summary>

Since all trading activities happen in Hydra, all deposit proceed has to be committed into Hydra before trading. Likewise, all the tradable value withdrawal has to be decommitted from Hydra back to Cardano L1.

Therefore, after you have placed the instruction to perform a deposit or withdrawal, the instructions are only fully performed when we close and re-open the active Hydra Head, which we call a "Hydra cycle". In future, when incremental commit and decommit mature, we can add deposit and withdrawal intervals between each Hydra cycle.

We are constantly accessing the optimal cycle length, which is currently a wide range like 30 minutes to 12 hours. Please refer to the application for the latest workflow.

</details>

## Trade

<details>

<summary>What is the minimum order size for trade?</summary>

DeltaDeFi technically supports all sizes of trading, as little as 0.1 ADA. However, we have imposed a minimum size of **5 ADA equivalent** as the minimum order size (unless particularly specified) to prevent spamming.

</details>



## Developer

<details>

<summary>How can I conduct trades using APIs?</summary>

Conducting trades with APIs is identical to placing orders on the website. For supported programming languages, you can directly use our official SDKs. For other languages, we also have open API specifications.

The only differences between using the web app and APIs to place orders are:

1. You have to load your wallet in the code base to conduct transaction signing.
2. It is possible to submit an order request through APIs with an incorrect payload, and the server will return errors accordingly (like missing price for limit order).

For details, please check out our developer documentation.

</details>

<details>

<summary>Why am I unable to place 2 market buy orders concurrently?</summary>

When conducting a market order, some value has to be locked up to prevent overspending the account balance. While we get a precise number of value to lock up for sell orders, which equals the order size, the value for buy market orders cannot be pre-determined since it is only finalized at the time of filling.

Therefore, particularly for market buy orders without maximum slippage configuration, within the moment after orders are placed and before matching, we will hold up entire balance for the selling token, which lead to concurrent buy market orders without maximum slippage failing. In that case, only the first order can be processed successfully and the rest would receive an error of insufficient balance.

If you need to optimize concurrent orders for your trading strategy, we recommend to simply use limit order or configure maximum slippage for your market order to have a more fine-grained control on your assets' availability.

</details>

<details>

<summary>Can I cancel orders programmatically?</summary>

Yes, it is the same as placing trades.

</details>

<details>

<summary>What are locked and free balances?</summary>

_**Free**_

This is the balance available to trade or to withdraw.

_**Locked**_

This is the balance that is in transition states, which are not available for trade or withdrawal. It represents all the statuses below:

1. Deposit in progress
2. Withdrawal in progress

3) Balance held up by active orders (e.g. limit orders on book)

</details>



