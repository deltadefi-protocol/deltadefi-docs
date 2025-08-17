# Order Book

Every order instruction will go into the single-threaded order book engine. However, DeltaDeFi's order book is indeed completely detached from the on-chain logic.&#x20;

### Order Book Engine

* Provide instructions on which order is matched or cancelled
* Ensuring the fairness of the DEX
* Purely off-chain

### On-chain Validators

* Safeguard value movement within DeltaDeFi
* Instructions are valid only when approved by the users' private key



We acknowledge that fairness is important to traders, therefore, we will make the market trading records available to the public. Such that any malicious behaviours can be detected by the community, posing a soft restriction on our team to behave honestly.

To learn more about the order book engine, please visit the whitepaper.
