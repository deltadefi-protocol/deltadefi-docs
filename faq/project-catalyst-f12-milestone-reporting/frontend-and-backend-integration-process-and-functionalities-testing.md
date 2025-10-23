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

To be supplemented after latest testnet deployment



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
