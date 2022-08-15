---
description: Create a refund order
---

# refund order

Create a refund order

{% swagger method="post" path="/AddRefundOrder" baseUrl="" summary="" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="OrderNo" required="true" %}
order id
{% endswagger-parameter %}

{% swagger-parameter in="body" name="Reason" required="true" %}
reason for return
{% endswagger-parameter %}

{% swagger-parameter in="body" name="Remark" %}
Refund Notes
{% endswagger-parameter %}

{% swagger-parameter in="body" name="Contacts" %}
Contact for follow-up notifications
{% endswagger-parameter %}

{% swagger-parameter in="body" name="Phone" %}
contact number
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="refund order number" %}
```javascript
{
    "code":10000,
    "message":"kk.api.200",
    "data":{
        "RefundNo":[
        "111","1111"
        ]
    }
}
```
{% endswagger-response %}
{% endswagger %}
