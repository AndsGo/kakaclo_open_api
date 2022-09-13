---
description: Create a refund order
---

# Refund Order

Create a refund order

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
