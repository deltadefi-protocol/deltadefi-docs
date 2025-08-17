# Account

Every DeltaDeFi account is composed of 2 keys, the master key and the operation key. When you use your Cardano wallet to connect to DeltaDeFi, your wallet is the golden source of truth for your account. Once you have created an account, an operation key will be generated. Here is the difference between the two:

|                                | Master Key                                           | Operation Key                                                                                                                                                         |
| ------------------------------ | ---------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Where it comes from            | Your Cardano wallet                                  | Generated                                                                                                                                                             |
| Actions it can authorize       | All, including rotation of trade key                 | The master key owner can define the access right. In current design, it is by default only in app actions like placing order. Withdrawal is not allowed with this key |
| Information DeltaDeFi controls | The public key hash                                  | The public key hash and the encrypted key by user defined password with AES-GCM algorithm                                                                             |
| Value held by the key          | The key holds all value as it is your Cardano wallet | The key holds exactly empty value except user send funds to it outside of DeltaDeFi                                                                                   |
| Signing transactions           | Like how you perform signing anywhere else           | Use API Key to obtain the encrypted key decrypt it for programmatic signing                                                                                           |



When you first sign in DeltaDeFi and create an account, an operation key is generated on the client side and encrypted with your provided password. The encrypted operation key with public key hash information will be sent to DeltaDeFi's server to complete the account opening process.

After that, all the signatures needed for trading could then be obtained programmatically to enable a seamless user experience.



***

### Related FAQ

* [How do I get my API keys?](../../../start-trading/developers/introduction/auth.md)
* [How can I sign a Cardano transaction?](../../../faq/cardano.md#how-can-i-sign-a-cardano-transaction)
* [How exactly is my operation key generated?](../../../faq/product.md#how-exactly-is-my-operation-key-generated)
