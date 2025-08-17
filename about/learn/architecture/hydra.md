# Hydra

The (not a) secret sauce of DeltaDeFi to enable efficient trading is that we build with Hydra, a Cardano state channel L2 technology.

### Compressing App Information with Merkle Tree

Although inside Hydra we can theoretically do anything we want, releasing all the constraints we have on Cardano L1, we still have to consider the hard L1 protocol limitation at the time of committing UTxOs to and decommitting UTxOs from Hydra.

One obvious limitation is the size of app states. Hypothetically DeltaDeFi has 10,000 users, it will then be technically super difficult to carry all app information into and out of Hydra. Therefore, at the time of committing and decommitting UTxOs, we will compress all the information needed in a Merkle tree root to support indefinitely scalable DApp states.

Since inside Hydra we can relax execution units and transaction fee limitations, we can perform huge transactions once after UTxOs are committed to break down into many distinct UTxOs. From there, our exchange behaves like any other L1 order book DEX, except we can have less care on efficiency since every transaction has exactly 0 cost. At the time of decommitting UTxOs, we will perform the mirrored set of huge transactions to compress app states back into the Merkle root hash.

The limitation of this approach is that on L1, when we handle deposits and withdrawals, we have to follow the same rules as all other Cardano L1 transactions, performing transactions one by one to the script UTxO containing the affected Merkle root hash.

### Data Integrity of Merkle Tree Element

Since the Merkle tree root hash itself does not contain the records themselves, and losing the actual records poses a significant threat in terms of permanent lock of user funds, DeltaDeFi will make the entire Merkle tree operation record public to avoid this risk.



***

### Related FAQ

* [I have heard about the Hydra Head protocol being custodial. Is my fund deposited into DeltaDeFi safe?](../../../faq/general.md#i-have-heard-about-the-hydra-head-protocol-being-custodial.-is-my-fund-deposited-into-deltadefi-safe)

