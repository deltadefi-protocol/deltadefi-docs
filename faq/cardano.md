# Cardano

## How can I get UTxOs from my wallet address?

If you want to get UTxO information for testing out APIs, you can find the UTxO information from various wallet interfaces:

<figure><img src="../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption><p>Example: Getting UTxO information from Eternl wallet</p></figcaption></figure>

If you want wallet UTxO information programmatically, the UTxO type accepted by our APIs is identical to the [Mesh](https://meshjs.dev/) type (Typescript SDK) and other SIDAN Lab tool chains:

* Rust - [whisky](https://github.com/sidan-lab/whisky)
* Golang - [rum](https://github.com/sidan-lab/rum)
* Python - [gin](https://github.com/sidan-lab/gin)



If you use an SDK like Mesh, there are [utility functions](https://meshjs.dev/providers/blockfrost#fetchAddressUtxos) to get address information directly to the type. Alternatively, you can directly use several Cardano service providers like Blockfrost or Maestro and parse the return type to the one compatible to our API request schema.

***

## How can I sign a Cardano transaction?

For interacting with DeltaDeFi APIs, we suggest signing the Cardano transactions through our DeltaDeFi SDKs, which are built on top of the Mesh and SIDAN Lab open source tool chain.

* [Typescript SDK](https://github.com/deltadefi-protocol/typescript-sdk) - [Mesh](https://meshjs.dev/)
* [Rust SDK](https://github.com/deltadefi-protocol/rust-sdk) - [whisky](https://github.com/sidan-lab/whisky)
* [Golang SDK](https://github.com/deltadefi-protocol/go-sdk) - [rum](https://github.com/sidan-lab/rum)
* [Python SDK](https://github.com/deltadefi-protocol/python-sdk) - [gin](https://github.com/sidan-lab/gin)

For signing the transaction with your [operation key](../about/learn/architecture/account.md), you first obtain the encrypted key with your API Key then decrypt it to the private key so that you can use the same tool chain above to perform transaction signing. There are also [end-to-end examples](https://github.com/deltadefi-protocol/sdks-demo) of integrating these SDKs to perform trades, which can help you speed up enjoying trading on DeltaDeFi.
