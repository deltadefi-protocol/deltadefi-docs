---
description: >-
  Below documentation illustrate the key testing process of frontend & backend
  integration
---

# Frontend & Backend Integration Process and Functionalities Testing

<details>

<summary><strong>Sign in to Account</strong></summary>

After the user has pressed the connect wallet button and signed the wallet ownership verification message, frontend will send a signin request to backend using the `SignIn` API

### POST - SignIn (Status Code)

<figure><img src="../../.gitbook/assets/image (99).png" alt=""><figcaption></figcaption></figure>



The `200 status code` shows the api is being called and responded successfully

### POST - SignIn (Request params)

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>



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

After successful signin, user can press the deposit button and select the "Regular deposit" to deposit funds when next hydra open event occurs. After inputting the deposit amount per asset, the user can press confirm to build the deposit transaction.

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

<summary>Build Deposit Transaction (Fast Deposit)</summary>

After successful signin, user can press the deposit button and select the "Fast Deposit" to deposit funds shortly with aid of an operator. After inputting the deposit amount per asset, the user can press confirm to build the deposit transaction.

</details>

<details>

<summary>Get Deposit Records</summary>

After successful signin, user can visit the dashboard page to view the deposit records. Frontend will call the GET deposit-records API to retrieve the deposit records by the user.

### GET - Deposit-records (Status Code)

<figure><img src="../../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>



The `200 status code` shows the api is being called and responded successfully

### GET - Deposit-records (Response)

<figure><img src="../../.gitbook/assets/image (62).png" alt=""><figcaption></figcaption></figure>



The deposit records shown in dashboard page are aligned with the data returned by the backend API. The backend API response fields are aligned with the required response fields from the backend API

<figure><img src="../../.gitbook/assets/image (63).png" alt=""><figcaption></figcaption></figure>



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
