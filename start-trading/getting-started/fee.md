# Fee

### Interacting with DeltaDeFi

The table below summarizes all potential actions interacting with DeltaDeFi.&#x20;

<table><thead><tr><th width="175.52734375">Actions</th><th width="150.09765625">DeltaDeFi Fees</th><th width="150.2421875">Other Fees</th><th>Remarks</th></tr></thead><tbody><tr><td>Fast Deposit</td><td>-</td><td>L1 tx fees</td><td>Min size applies<sup>1</sup></td></tr><tr><td>Regular Deposit</td><td>-</td><td>L1 tx fees</td><td>Min size applies<sup>1</sup></td></tr><tr><td>Place Order</td><td>-</td><td>-</td><td>Min size applies<sup>2</sup></td></tr><tr><td>Cancel Order</td><td>-</td><td>-</td><td>-</td></tr><tr><td>Fill Order</td><td>Trading fee applies</td><td>-</td><td>-</td></tr><tr><td>Fast Withdrawal</td><td>1 ADA</td><td>-</td><td>Min size applies<sup>1</sup></td></tr><tr><td>Regular Withdrawal</td><td>1 ADA</td><td>-</td><td>Min size applies<sup>1</sup></td></tr></tbody></table>

<sup>1</sup> For deposit and withdrawal events, min size of `2 + 0.5 * number of types of token` applies.

<sup>2</sup> For orders placement, minimal 5 USD equiv min order size applies.

### Trading Fee

We apply trading fees to all executed orders.

| Tiers           | Maker | Taker |
| --------------- | ----- | ----- |
| Standard        | 0.1%  | 0.1%  |
| Advance Tiering | TBC   | TBC   |

