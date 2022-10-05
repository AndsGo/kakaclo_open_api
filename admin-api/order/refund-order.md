---
description: Create a refund order
---

# Refund Order

Create a refund order。

Cancel the order and get a refund. you can only do this when the order has not been shipped. This operation is performed asynchronously, and you can get the latest status information through "[Query ReFund](query-refund.md)"

The current status of "Refund Order API" can be updated for a maximum of 24 hours. Generally, the status will be updated within 1 hour.

{% swagger method="post" path="/openapi/v1/order/orders/{id}/refund" baseUrl="" summary="" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="Remark" required="true" %}
Refund Notes
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="refund order number" %}
```javascript
{
    "code":10000,
    "message":"kk.api.200",
    "data":
        "111"
}
```
{% endswagger-response %}
{% endswagger %}
