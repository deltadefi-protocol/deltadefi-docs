# Python

### About

DeltaDeFi's Python SDK provides utility functions to interact with the API service and sign transactions with provided keys.

### Installation

The SDK is hosted on npmjs.com, so you can directly import it using your favorite package manager.

```python
pip3 install deltadefi
```

### Getting Started

Placing and canceling orders are as simple as below.

```python
import os

from deltadefi import ApiClient
from dotenv import load_dotenv

load_dotenv(".env", override=True)
api_key = os.environ.get("DELTADEFI_API_KEY")
password = os.environ.get("TRADING_PASSWORD")

api = ApiClient(api_key=api_key)
api.load_operation_key(password)
```

### Posting Order

```python
res = api.post_order(
    symbol="ADAUSDM",
    side="sell",
    type="limit",
    quantity=51,
    price=15,
)

print("Order submitted successfully.", res)
```

### Detailed SDK demo

[https://github.com/deltadefi-protocol/sdks-demo/tree/main/python](https://github.com/deltadefi-protocol/sdks-demo/tree/main/python)

