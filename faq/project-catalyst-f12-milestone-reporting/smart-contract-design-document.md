---
description: >-
  Below session illustrates the detailed logic, structure, pseudocode, and flow
  diagram of the DeltaDeFi smart contract
---

# Smart Contract Design Document

## Detailed Logic, Structure & Pseudocode of the Smart Contract

Below 2 validators illustrate the detailed logic, structures and pseudocode code of the smart contract of DeltaDeFi

### Take Orders Validator

#### Parameters:

* `oracle_nft`: The policy id of `OracleNFT`
* `param_long_token`: The long side of token in trading pairs
* `param_short_token`: The short side of token in trading pairs

#### Datum:

* `account_address`: The address of the account number of the owner
* `is_long`: If the current order is for buying long token (`buy_token`)
* `list_price_times_10k`: Order exchange in a rate of `list_price` \* `lot_size` = quantity of `param_short_token`
* `lot_size` : Quantity of `sell token` in this order
* `owner:` The pub key hash of owner of the order

#### User Action:

1. Core logic of taking orders - Redeemer `TakeOrders`
   1. Withdrawal script of `take_orders` validating
2. Cancelling order which is mistakenly listed onchain - Redeemer `CancelOrder`
   1. Whole value spent to `Account` with correct owner in datum
   2. signed by both `operating_key` and owner

#### Pseudocode:

<pre><code>validator virtual_dex_take_orders(oracle_nft, param_long_token, param_short_token)

Purpose of the validator:
- To validate whether the wallet can Withdraw stake rewards; AND
- To validate whether the wallet can publish delegation certificate

// Validation logic:
Accumulate proceeds supposed send to order creators, check output value to them:
1. Look through all inputs -> if from same address -> get (account_address, change_account_address, receive_value)
2. Merge all results above with same account_address
3. Check each unique account_address, if outputs to trade_account + change_account >= to_receive
<strong>
</strong><strong>return true if the above validations are passed. Otherwise, return false.
</strong></code></pre>

### Virtual DEX Validator

#### Parameters:

* `oracle_nft`: The policy id of `OracleNFT`
* `take_orders`: The script hash of `take_orders` withdrawal script

#### User Action:

1. `Normal operation`:
   1. Reference to oracle utxo
   2. Accumulate proceeds supposed send to order creators, check output value to them
   3. Signed by operation key

#### Pseudocode:

<pre><code>validator virtual_dex(oracle_nft, take_orders)

<strong>// Purpose of the validator:
</strong>- To validate whether the wallet can spend of transaction output 

// Validation logic:
- Perform the validation based on the specified TakeOrders or CancelOrder redeemer
- For TakeOrder: validate transaction has sufficient signatures
- For CancelOrder: validate if the order value is returned and operation key is signed

return true if either above validation is passed. Otherwise, return false.
</code></pre>



## Flow Diagram

The flow diagram shows the flows for different scenarios. The first scenario illustrates an ADA seller creates an order and the order matches another subsequent order requesting to sell USD stablecoin. After the validation of the smart contract, the smart contract will unlock the funds and execute the transactions shown per user wallet. The expected output to each user wallet ("account'") is shown in the diagram for the first scenario. The second scenario is basically the reverse situation compared to first scenario.

<figure><img src="../../.gitbook/assets/DeltaDeFi Smart Contract Pseudocode and Flow Diagram.png" alt=""><figcaption></figcaption></figure>

