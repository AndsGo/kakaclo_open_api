---
description: Query Order Refund Transaction Slip
---

# Query ReFund

Query Order Refund Transaction Slip

{% swagger method="get" path="/openapi/v2/order/orders/refund" baseUrl="" summary="" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "code": 10000,
    "data": {
        "total": 1,
        "pageNumber": 1,
        "pageSize": 10,
        "list": [
            {
                "refundNo": "1560897343230267394",
                "refundStatus": "refund_successfully",
                "id": "1000000387523"
            }
        ]
    },
    "message": "success"
}
```
{% endswagger-response %}
{% endswagger %}

## Response Properties <a href="#response-parameter" id="response-parameter"></a>

| Parameter name                                | Type   | Remark              |
| --------------------------------------------- | ------ | ------------------- |
| refundNo                                      | String | refund order number |
| id                                            | String | order id            |
| remark                                        | String | order notes         |
| [refundStatus](query-refund.md#refund-status) | String | refund status       |

## Refund Status

| status               | Remark                 |   |
| -------------------- | ---------------------- | - |
| pending\_review      | Refund is under review |   |
| refund\_successfully | Refund successfully    |   |
| refund\_failed       | Refund failed          |   |
