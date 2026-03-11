# Services and Charges

### Operator Services

The L1 swap integration is processed by an operator which will take execution risk on DeltaDeFi's order book. That being said

The order will be processed if

1. The current order book depth can absorb the swap (use [api-market-depth.md](api-market-depth.md "mention") to check whether the book depth would fill the order)
2. The expiry time in datum has not passed

Therefore, to facilitate smooth order matching, we suggest adding an adequate buffer (max slippage tolerance) at building the swap intent datum. If the order instruction cannot be fulfilled by the time of arriving Cardano L1, we would skip processing in our core workflow. There are occassion we will trigger episodic order filling after core processing time initially and before expiry, however, we do not guarantee such case. Any expired orders can be cancelled in a fully non-custodial manner.



### Charges

The operator charges an additional 0.1% per swap processed. Therefore:

* For `ADAUSDM`, in total 0.2% will be charged (0.1% for DeltaDeFi trading fee)
* For `NIGHTADA`, in total 0.4% will be charged (0.2% for DeltaDeFi trading fee)

The charges are reflected in [api-market-depth.md](api-market-depth.md "mention"), so when you see the market depth from the API the fee is already taken into account.

We by default suggest a higher buffer / slippage tolerence at order placement. If there is significant buffer at order instruction, we will always capped the fee stated above (0.1% per swap processed) and the users will receive additional tokens than the amount specified at `toAmount`.

