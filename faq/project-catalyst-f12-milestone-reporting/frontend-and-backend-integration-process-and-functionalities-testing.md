---
description: >-
  Below documentation illustrate the key testing process of frontend & backend
  integration
---

# Frontend & Backend & Smart Contract Integration Process and Functionalities Testing

## Frontend & Backend Integration Verification

<details>

<summary><strong>Sign in to Account</strong></summary>

After the user has pressed the connect wallet button and signed the wallet ownership verification message, frontend will send a signin request to backend using the `SignIn` API

### POST - SignIn (Status Code)

<figure><img src="../../.gitbook/assets/image (99).png" alt=""><figcaption></figcaption></figure>



The `200 status code` shows the api is being called and responded successfully

### POST - SignIn (Request params)

<figure><img src="../../.gitbook/assets/image (14) (1).png" alt=""><figcaption></figcaption></figure>



The request param is aligned with the required request param from the backend API

<figure><img src="../../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>



### POST - SignIn (Response)

<figure><img src="../../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>



The response fields are aligned with the required response fields from the backend API

<figure><img src="../../.gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>



</details>

<details>

<summary>Get Spot Account Information</summary>

After the user has performed a successful sign-in, frontend will call the GET spot-account API to retrieve necessary account information related to the user account

### GET - Spot-account (Status Code)

<figure><img src="../../.gitbook/assets/image (58).png" alt=""><figcaption></figcaption></figure>



The `200 status code` shows the api is being called and responded successfully

### GET - Spot-account (Response)

<figure><img src="../../.gitbook/assets/image (59).png" alt=""><figcaption></figcaption></figure>



The response fields are aligned with the required response fields from the backend API

<figure><img src="../../.gitbook/assets/image (60).png" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary>Build Deposit Transaction (Regular Deposit)</summary>

After successful signin, user can press the deposit button and select the "Regular deposit" to deposit funds when next hydra open event occurs. After inputting the deposit amount per asset, the user can press confirm to build the deposit transaction. User's wallet signature is required to authorized the deposit transaction. Smart contract is being integrated in this action as well (Please see the smart contract integration part below for more information).

### POST - /accounts/deposit/build (Status Code)

<figure><img src="../../.gitbook/assets/image (100).png" alt=""><figcaption></figcaption></figure>



The `200 status code` shows the api is being called and responded successfully

### POST - /accounts/deposit/build (Request params)

<figure><img src="../../.gitbook/assets/image (101).png" alt=""><figcaption></figcaption></figure>



The request param is aligned with the required request param from the backend API

<figure><img src="../../.gitbook/assets/image (102).png" alt=""><figcaption></figcaption></figure>



### POST - /accounts/deposit/build (Response)

<figure><img src="../../.gitbook/assets/image (103).png" alt=""><figcaption></figcaption></figure>



The response fields are aligned with the required response fields from the backend API

<figure><img src="../../.gitbook/assets/image (104).png" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary>Submit Deposit Transaction (Regular Deposit)</summary>

Continuing from the Build Deposit Transaction, frontend will submit the user-signed deposit transaction to the Cardano blockchain. The transaction must have been previously built using the /accounts/deposit/build endpoint and signed with the user's wallet

### POST - /accounts/deposit/submit (Status Code)

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

The `200 status code` shows the api is being called and responded successfully



### POST - /accounts/deposit/submit (Request params)

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>



The request param is aligned with the required request param from the backend API

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>



### POST - /accounts/deposit/submit (Response)

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>



The response fields are aligned with the required response fields from the backend API

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>



</details>

<details>

<summary>Build Transferral Transaction (Fast Deposit)</summary>

After successful signin, user can press the deposit button and select the "Fast Deposit" to deposit funds shortly with aid of an operator. After inputting the deposit amount per asset, the user can press confirm to build the deposit transaction.



### POST - /accounts/transferal/build (Status Code)

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>



The `200 status code` shows the api is being called and responded successfully



### POST - /accounts/transferal/build (Request params)

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>



The request param is aligned with the required request param from the backend API

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>



### POST - /accounts/transferal/build (Response)

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>



The response fields are aligned with the required response fields from the backend API

<figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>



</details>

<details>

<summary>Build Request Transferral Transaction (Fast Withdrawal)</summary>

After successful signin, user can press the deposit button and select the "Fast Withdrawal" to withdrawfunds shortly with aid of an operator. After inputting the withdraw amount per asset, the user can press confirm to build the deposit transaction.



### POST - /accounts/request-transferal/build (Status Code)

<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

The `200 status code` shows the api is being called and responded successfully



### POST - /accounts/transferal/build (Request params)

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>



The request param is aligned with the required request param from the backend API

<figure><img src="../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>



### POST - /accounts/transferal/build (Response)

<figure><img src="../../.gitbook/assets/image (121).png" alt=""><figcaption></figcaption></figure>



The response fields are aligned with the required response fields from the backend API

<figure><img src="../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary>Submit Request Transferral Transaction (Fast Withdrawal)</summary>

Continuing from the Build Request Transferral Transaction, the frontend submits a user-signed request transferal transaction to the Cardano blockchain.&#x20;



### POST - /accounts/request-transferal/submit (Status Code)

<figure><img src="../../.gitbook/assets/image (123).png" alt=""><figcaption></figcaption></figure>



The `200 status code` shows the api is being called and responded successfully



### POST - /accounts/transferal/submit (Request params)

<figure><img src="../../.gitbook/assets/image (124).png" alt=""><figcaption></figcaption></figure>



The request param is aligned with the required request param from the backend API

<figure><img src="../../.gitbook/assets/image (125).png" alt=""><figcaption></figcaption></figure>



### POST - /accounts/transferal/submit (Response)

<figure><img src="../../.gitbook/assets/image (126).png" alt=""><figcaption></figcaption></figure>



The response fields are aligned with the required response fields from the backend API

<figure><img src="../../.gitbook/assets/image (127).png" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary>Get Deposit Records</summary>

After successful signin, user can visit the dashboard page to view the regular deposit records. Frontend will call the GET deposit-records API to retrieve the regular deposit records by the user.

### GET - Deposit-records (Status Code)

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>



The `200 status code` shows the api is being called and responded successfully



### GET - Deposit-records (Response)

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>



The deposit records shown in dashboard page are aligned with the data returned by the backend API. The backend API response fields are aligned with the required response fields from the backend API

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>



</details>

<details>

<summary>Get Transferral Records (To Get Fast Deposit and Withdrawal records)</summary>

After successful signin, user can visit the dashboard page to view the fast deposit records. Frontend will call the GET transferl-records API to retrieve the fast deposit records by the user.

### GET - transferal-records (Status Code)

<figure><img src="../../.gitbook/assets/image (128).png" alt=""><figcaption></figcaption></figure>



The `200 status code` shows the api is being called and responded successfully



### GET - transferal-records (Response)

<figure><img src="../../.gitbook/assets/image (129).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../../.gitbook/assets/image (130).png" alt=""><figcaption></figcaption></figure>



The transferal records shown in dashboard page are aligned with the data returned by the backend API. The backend API response fields are aligned with the required response fields from the backend API



<figure><img src="../../.gitbook/assets/image (131).png" alt=""><figcaption></figcaption></figure>



</details>

<details>

<summary>Get Account Balance</summary>

After successful signin, user can visit the trading page to view the account's available balance. Frontend will call the GET account-balance API to retrieve the account balance by the user.

### GET - account-balance (Status Code)

<figure><img src="../../.gitbook/assets/image (64).png" alt=""><figcaption></figcaption></figure>



The `200 status code` shows the api is being called and responded successfully

### GET - account-balance (Response)

<figure><img src="../../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>



The available balance shown in trading page are aligned with the api response from backend. The response fields are aligned with the required response fields from the backend API

<figure><img src="../../.gitbook/assets/image (66).png" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary>Get Order Records (by Open Order)</summary>

After successful signin, user can visit the trading page to view the open order records. Frontend will call the GET order-records API filtered by status (openOrder) to retrieve the open order records by the user.

### GET - order-records (Status Code)

<figure><img src="../../.gitbook/assets/image (67).png" alt=""><figcaption></figcaption></figure>



The `200 status code` shows the api is being called and responded successfully



### GET - order-records (Response)

<figure><img src="../../.gitbook/assets/image (68).png" alt=""><figcaption></figcaption></figure>



The open order records shown in trading page are aligned with the api response from backend. The response fields are aligned with the required response fields from the backend API

<figure><img src="../../.gitbook/assets/image (69).png" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary>Get Order Records (by Order History)</summary>

After successful signin, user can visit the trading page to view the order history records. Frontend will call the GET order-records API filtered by status (orderHistory) to retrieve the order history records by the user.

### GET - order-records (Status Code)

<figure><img src="../../.gitbook/assets/image (70).png" alt=""><figcaption></figcaption></figure>



The `200 status code` shows the api is being called and responded successfully

### GET - order-records (Response)

<figure><img src="../../.gitbook/assets/image (71).png" alt=""><figcaption></figcaption></figure>



The order history records shown in trading page are aligned with the api response from backend. The response fields are aligned with the required response fields from the backend API

<figure><img src="../../.gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary>Get Order Records (by Trade History)</summary>

After successful signin, user can visit the trading page to view the trade history records. Frontend will call the GET order-records API filtered by status (tradeHistory) to retrieve the trade history records by the user.

### GET - order-records (Status Code)

<figure><img src="../../.gitbook/assets/image (73).png" alt=""><figcaption></figcaption></figure>



The `200 status code` shows the api is being called and responded successfully

### GET - order-records (Response)

<figure><img src="../../.gitbook/assets/image (74).png" alt=""><figcaption></figcaption></figure>

The trade history records shown in trading page are aligned with the api response from backend. The response fields are aligned with the required response fields from the backend API

<figure><img src="../../.gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary>Get API Key</summary>

After successful signin, user can visit the dashboard page to view the api-key. Frontend will call the GET api-key API to retrieve the api key by the user.

### GET - api-key (Status Code)

<figure><img src="../../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>



The `200 status code` shows the api is being called and responded successfully

### GET - api-key (Response)

<figure><img src="../../.gitbook/assets/image (77).png" alt=""><figcaption></figcaption></figure>



The api key shown in dashboard page is aligned with the api response from backend. The response fields are aligned with the required response fields from the backend API

<figure><img src="../../.gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary>Build Place Order Transaction</summary>

After successful signin, user can visit the trading page to place order. Frontend will call the POST order/build API to construct an unsigned Cardano transaction for placing a limit or market order. The transaction must be signed by the user's operation key and then submitted using the /order/submit endpoint.

### POST - order/build (Status Code)

<figure><img src="../../.gitbook/assets/image (79).png" alt=""><figcaption></figcaption></figure>



The `200 status code` shows the api is being called and responded successfully

### POST - order/build (Request Parameters)

<mark style="color:red;">To be updated</mark>



The request param's fields are aligned with the required request params from the backend API

<figure><img src="../../.gitbook/assets/image (81).png" alt=""><figcaption></figcaption></figure>



### POST - order/build (Response)

<figure><img src="../../.gitbook/assets/image (82).png" alt=""><figcaption></figcaption></figure>



The response fields are aligned with the required response fields from the backend API

<figure><img src="../../.gitbook/assets/image (83).png" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary>Submit Place Order Transaction</summary>

Continue from the Build Place Order Transaction section, frontend submits a signed order transaction to hydra. Use this endpoint after signing the transaction hex returned from /order/build

### POST - order/submit (Status Code)

<figure><img src="../../.gitbook/assets/image (84).png" alt=""><figcaption></figcaption></figure>



The `200 status code` shows the api is being called and responded successfully

### POST - order/submit (Request Parameters)

<figure><img src="../../.gitbook/assets/image (85).png" alt=""><figcaption></figcaption></figure>



The request param's fields are aligned with the required request params from the backend API

<figure><img src="../../.gitbook/assets/image (86).png" alt=""><figcaption></figcaption></figure>



### POST - order/submit (Response)

<figure><img src="../../.gitbook/assets/image (87).png" alt=""><figcaption></figcaption></figure>



The response fields are aligned with the required response fields from the backend API

<figure><img src="../../.gitbook/assets/image (88).png" alt=""><figcaption></figcaption></figure>



</details>

<details>

<summary>Build Cancel Order Transaction</summary>

After successful signin, user can visit the trading page to cancel order. Frontend will call the DELETE order/{id}/build API to construct an unsigned Cardano transaction for cancelling a specific order by its ID. The transaction must be signed by the user's operation key and then submitted using the /order/submit endpoint.

### DELETE - order/{id}/build (Status Code)

<figure><img src="../../.gitbook/assets/image (89).png" alt=""><figcaption></figcaption></figure>



The `200 status code` shows the api is being called and responded successfully

### DELETE - order/{id}/build (Response)

<figure><img src="../../.gitbook/assets/image (91).png" alt=""><figcaption></figcaption></figure>



The response field is aligned with the required response's field from the backend API

<figure><img src="../../.gitbook/assets/image (92).png" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary>Submit Cancel Order Transaction</summary>

Continue from the Build Cancel Order Transaction section, frontend submits a signed order transaction to hydra. Use this endpoint after signing the transaction hex returned from /order/{id}/build

### DELETE - order/submit (Status Code)

<figure><img src="../../.gitbook/assets/image (93).png" alt=""><figcaption></figcaption></figure>



The `200 status code` shows the api is being called and responded successfully



### DELETE - order/submit (Request params)

<figure><img src="../../.gitbook/assets/image (94).png" alt=""><figcaption></figcaption></figure>



The request param's fields are aligned with the required request params from the backend API

<figure><img src="../../.gitbook/assets/image (95).png" alt=""><figcaption></figcaption></figure>



### DELETE - order/submit (Response)

<figure><img src="../../.gitbook/assets/image (96).png" alt=""><figcaption></figcaption></figure>



The response field is aligned with the required response's field from the backend API

<figure><img src="../../.gitbook/assets/image (97).png" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary>Get Withdrawal Records</summary>

After successful signin, user can visit the dashboard page to view the regular withdrawal records. Frontend will call the GET withdrawal-records API to retrieve the regular withdrawal records by the user.

### GET - Withdrawal-records (Status Code)

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>



The `200 status code` shows the api is being called and responded successfully

### GET - Withdrawal-records (Response)

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

The withdrawal records shown in dashboard page are aligned with the data returned by the backend API. The backend API response fields are aligned with the required response fields from the backend API

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>



</details>



## Smart Contract Integration Verification

To validate our scripts, user would need to make a regular deposit and assess the deposit transaction according to below steps:

<details>

<summary>Step 1: Assess the datum in User's deposit transaction to start looking into the details of the relevant smart contracts</summary>

After signing and submitting the deposit transaction, user will be able to find the deposit transaction in browser wallet (e.g. eternl, vespr, etc.). User view the deposit transaction in Cardano Explorer and browse the "Reference Input" section. Click to expand the datum information for further verification in [https://cardananium.github.io/cquisitor/](https://cardananium.github.io/cquisitor/) (A tool supporting decode by CSL to verify all involved script information)



<figure><img src="../../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>





</details>

<details>

<summary>Step 2: Get the detailed script information in Cquisitor using the identified datum</summary>

Copy the full datum found in step 1 to [https://cardananium.github.io/cquisitor/](https://cardananium.github.io/cquisitor/). Select `Decode by CSL` as the tool, `PlutusData` as the CSL type, `preprod` as network type, `BasicConversions` as Schema



<figure><img src="../../.gitbook/assets/image (9) (1).png" alt=""><figcaption></figcaption></figure>



</details>

<details>

<summary>Step 3: Cross check the script hashes shown in Cquisitor, Cardano Explorer, team's disclosed script transaction id and team's open-sourced smart contract</summary>

AppOracle will always be taken as the reference input in all L1 transactions to pass the validation of each script. It acts as a bridge to connect every scripts all together and shares the policyId and script address info among them. The output's field sequence shown in the JSON in cquisitor is according to team's open-source smart contract's pub type AppOracleDatum:

Visit [https://github.com/deltadefi-protocol/aiken-virtual-dex/blob/staging/lib/hydra\_dex/types.ak](https://github.com/deltadefi-protocol/aiken-virtual-dex/blob/staging/lib/hydra_dex/types.ak) and locate the `pub type AppOracleDatum`:

```
pub type WithdrawalScriptHashes {
  app_deposit: ScriptHash,
  app_withdrawal: ScriptHash,
  emergency_cancel_order: ScriptHash,
}

pub type AppOracleDatum {
  operation_key: VerificationKeyHash,
  stop_key: VerificationKeyHash,
  oracle_nft: PolicyId,
  oracle_address: Address,
  app_vault_address: Address,
  app_deposit_request_token: PolicyId,
  app_deposit_request_address: Address,
  dex_account_balance_token: PolicyId,
  dex_account_balance_address: Address,
  dex_order_book_token: PolicyId,
  dex_order_book_address: Address,
  emergency_cancel_order_request_token: PolicyId, // Not used in MVP
  emergency_cancel_order_request_address: Address, // Not used in MVP
  emergency_withdrawal_request_token: PolicyId, // Not used in MVP
  emergency_withdrawal_request_address: Address, // Not used in MVP
  all_withdrawal_script_hashes: WithdrawalScriptHashes,
  hydra_info: HydraInfo,
}
```



For example, since `app_vault_address` is located as the 5th field of AppOracleDatum, it will be shown as the `4th field` in the JSON outputted by cquisitor.



For the MVP, the team has only deployed below scripts with the corresponding `transaction hashes` :

1. APPVAULT\_SPEND: `57854b8511b1a50871ca963ec484dced2e2f7f896d30151539f199009627697f`
2. APPDEPOSITREQUEST\_MINT: `cf70f97385098d8c4731e087b5c19d57eb5a0722020bca23c2dd500bba52bb42`
3. APPDEPOSITREQUEST\_SPEND: `a7411fbcef4165796e0c8eb398fab1114b63f9919a368e1b8fb1fa80744b41b4`
4. DEXACCOUNTBALANCE\_SPEND: `46986417bb211c7150eba6853e10ef23216712a108250b0a4a924e76be07caa4`
5. DEXORDERBOOK\_SPEND: `1e21600cc5e1886981ce99b6fc78789634c2900abf4bc9038511cc8449a171b1`
6. ACCOUNTOPERATION\_APPDEPOSIT: `6d98e85b02713a9847c76befaef89f87480e75e136900719b5fe4ef982aba813`
7. ACCOUNTOPERATION\_APPWITHDRAWAL: `9bb2b01da61f67625f658839a49c6e869a285d65fc9437a1ce3d8c0702259183`



</details>

<details>

<summary>Step 3.1: Verify the APPVAULT_SPEND script</summary>

tx id: `57854b8511b1a50871ca963ec484dced2e2f7f896d30151539f199009627697f`&#x20;



Search the trasnaction by tx id in Cardano explorer and locate the `script hash` in Outputs

<figure><img src="../../.gitbook/assets/image (12) (1).png" alt=""><figcaption></figcaption></figure>



Validated the identified script hash with the output shown in cquisitor

<figure><img src="../../.gitbook/assets/image (13) (1).png" alt=""><figcaption></figcaption></figure>



</details>

<details>

<summary>Step 3.2: Verify the APPDEPOSITREQUEST_MINT script</summary>

tx id:  `cf70f97385098d8c4731e087b5c19d57eb5a0722020bca23c2dd500bba52bb42`&#x20;



Search the trasnaction by tx id in Cardano explorer and locate the `script hash` in Outputs

<figure><img src="../../.gitbook/assets/image (105).png" alt=""><figcaption></figcaption></figure>



Validated the identified script hash with the output shown in cquisitor

<figure><img src="../../.gitbook/assets/image (106).png" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary>Step 3.3: Verify the APPDEPOSITREQUEST_SPEND script</summary>

Txid: `a7411fbcef4165796e0c8eb398fab1114b63f9919a368e1b8fb1fa80744b41b4`&#x20;



Search the trasnaction by tx id in Cardano explorer and locate the `script hash` in Outputs

<figure><img src="../../.gitbook/assets/image (107).png" alt=""><figcaption></figcaption></figure>



Validated the identified script hash with the output shown in cquisitor

<figure><img src="../../.gitbook/assets/image (108).png" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary>Step 3.4: Verify the DEXACCOUNTBALANCE_SPEND script </summary>

Txid: `46986417bb211c7150eba6853e10ef23216712a108250b0a4a924e76be07caa4`&#x20;



Search the trasnaction by tx id in Cardano explorer and locate the `script hash` in Outputs

<figure><img src="../../.gitbook/assets/image (109).png" alt=""><figcaption></figcaption></figure>



Validated the identified script hash with the output shown in cquisitor

<figure><img src="../../.gitbook/assets/image (110).png" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary>Step 3.5: Verify the DEXORDERBOOK_SPEND script </summary>

Txid: `1e21600cc5e1886981ce99b6fc78789634c2900abf4bc9038511cc8449a171b1`&#x20;



Search the trasnaction by tx id in Cardano explorer and locate the `script hash` in Outputs

<figure><img src="../../.gitbook/assets/image (112).png" alt=""><figcaption></figcaption></figure>



Validated the identified script hash with the output shown in cquisitor

<figure><img src="../../.gitbook/assets/image (113).png" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary>Step 3.6: Verify the ACCOUNTOPERATION_APPDEPOSIT script</summary>

Txid: `6d98e85b02713a9847c76befaef89f87480e75e136900719b5fe4ef982aba813`&#x20;



Search the trasnaction by tx id in Cardano explorer and locate the `script hash` in Outputs

<figure><img src="../../.gitbook/assets/image (116).png" alt=""><figcaption></figcaption></figure>



Validated the identified script hash with the output shown in cquisitor

<figure><img src="../../.gitbook/assets/image (118).png" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary>Step 3.7: Verify the ACCOUNTOPERATION_APPWITHDRAWAL script</summary>

Txid: `9bb2b01da61f67625f658839a49c6e869a285d65fc9437a1ce3d8c0702259183`



Search the trasnaction by tx id in Cardano explorer and locate the `script hash` in Outputs

<figure><img src="../../.gitbook/assets/image (119).png" alt=""><figcaption></figcaption></figure>



Validated the identified script hash with the output shown in cquisitor

<figure><img src="../../.gitbook/assets/image (120).png" alt=""><figcaption></figcaption></figure>

</details>
