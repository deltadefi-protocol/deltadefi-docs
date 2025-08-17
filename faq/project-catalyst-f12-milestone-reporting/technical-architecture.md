---
description: >-
  Below technical architecture illustrates the system architecture, including
  both off-chain and on-chain components of DeltaDeFi.
---

# Technical Architecture

## System architecture, including both off-chain and on-chain components

Below system architecture illustrates both off-chain and on-chain components of DeltaDeFi. As shown in the architecture, only the matched orders will be submitted to blockchain, causing transaction fee. Otherwise, there will be no transaction fee caused for any order creation, modification, and cancellation. Immediate order response will be provided to user as well. The whole offchain part is below hosted in AWS cloud as shown in the diagram below while the interaction with the public blockchain is via cardano node API services.

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>



## Comprehensive Diagram illustrating the architecture, data flow, and component interactions

The off-chain components as shown below include the DeltaDeFi SDK, frontend application and backend application. The DeltaDeFi SDK are something we build to allow programmatic users to submit trading transactions without the need to understand all details about cardano transaction building, submission, etc. The frontend application and backend application are being hosted in AWS cloud. The redis database is being used to cache transactions. The AWS RDS database will store information including activities logs, order  information, users information. The breakdown of the elastic container services show how we group the backend services into different microservices including API server, order management system and order server. Once any order is being matched with another order, API server will submit the offchain order onchain using some Cardano node API services. The Cardano node API services are being used as the middleware to allow the offchain components to interact with the onchain components e.g. smart contract and cardano node.

<figure><img src="../../.gitbook/assets/DeltaDeFi Technical Architecture.png" alt=""><figcaption></figcaption></figure>
