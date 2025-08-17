# Intent and Process

DeltaDeFi has reproduced the account-based model in UTxOs for abstracting the UTxO model complexity in building the DApp. With that notion, most user actions in DeltaDeFi start with initializing an intent:

* It requires the account's signature (either master key or operation key) to produce the intent
* DeltaDeFi will process the intents in a queue to prevent UTxO contention
* Applicable to L1 deposit and all Hydra actions



### Sacrifying Decentralization?

DeltaDeFi software system is crucial to make the entire product work. However, with such design, one thing that we will never sacrifice is the users' fund safety. To put in simple terms:

* Without users' signature, value can never transfer to other accounts
* Without DeltaDeFi software, the DEX cannot function in an efficient way



### Emergency Actions

That being said, we still want to keep our DEX as decentralized as possible. One line that we hold strongly is that users have a route to withdraw assets out of the system without DeltaDeFi's permission. Any users, in case of any emergency incidents such as an official software disruption, can perform emergency withdrawal by crafting a valid Cardano transaction themselves.&#x20;

However, any emergency actions without coordinating with DeltaDeFi's software might affect other users' experience, such as failing to fill an order supposed to be as instructed by the order book engine. To prevent such an abuse, the emergency actions have been enforced with a time lag, such that in case of misuse, DeltaDeFi can have a sufficient time window to account for the self-initiated emergency actions without affecting other normal users' experience.
