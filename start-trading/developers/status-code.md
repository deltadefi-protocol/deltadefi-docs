# Status code

## 🚨 API Error Codes

### Response Format

All API errors return a consistent JSON structure with both human-readable messages and machine-readable codes for programmatic handling.

{% tabs %}
{% tab title="Response Structure" %}
```json
  {
    "error": "Invalid request data",
    "code": 4000
  }
```
{% endtab %}

{% tab title="Typescript" %}
```typescript
  interface ErrorResponse {
    error: string;
    code: number;
  }
```
{% endtab %}

{% tab title="Go" %}
```go
  type ErrorResponse struct {
      Error string `json:"error"`
      Code  int16  `json:"code"`
  }
```
{% endtab %}
{% endtabs %}

***

📊 Error Code Reference

| Error code |                   Message                   |
| :--------: | :-----------------------------------------: |
|    4000    |             Invalid request data            |
|    4010    |             Unauthorized access             |
|    4050    |     Insufficient balance to place order     |
|    4100    |      Order size must be at least 5 ADA      |
|    4101    |      Order price must be greater then 0     |
|    4102    |   Price must have at most 4 decimal places  |
|    4103    | Quantity must have at most 4 decimal places |
|    4200    |               Order not found               |
|    4201    |              Order is not open              |
|    4202    |            Order State in invalid           |
|    4290    | Rate limit exceeded, please try again later |
|    4300    |   Transaction expired, please build again   |
|    4400    |                User not found               |
|    4402    |            Transaction not found            |
|    4404    |           Invalid status paramter           |
|    4405    |          Invalid interval paramter          |
|    4406    |  Account is missing required operation key  |
|    4407    |          Failed to sign transaction         |
|    5000    |            Internal Server Error            |
|    5001    |   System resources temporaily unavailable   |
