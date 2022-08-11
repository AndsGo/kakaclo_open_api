---
description: Query Order Refund Transaction Slip
---

# Query ReFund

Query Order Refund Transaction Slip

## Refund Status

| status               | Remark                 |   |
| -------------------- | ---------------------- | - |
| pending\_review      | Refund is under review |   |
| refund\_successfully | Refund successfully    |   |
| refund\_failed       | Refund failed          |   |

## Response Properties <a href="#response-parameter" id="response-parameter"></a>

| Parameter name | Type   | Remark              |
| -------------- | ------ | ------------------- |
| refundNo       | String | refund order number |
| id             | String | order id            |
| reason         | String | reason for return   |
| remark         | String | order notes         |
| refundStatus   | String | refund status       |

{% swagger method="get" path="/order/refund" baseUrl="" summary="" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="query" name="refundNo" %}
refund's Nos, please use comma as separator, for example 1000000065617,1000000065618
{% endswagger-parameter %}

{% swagger-parameter in="query" name="ids" %}
Order's IDs, please use comma as separator, for example 1000000065617,1000000065618
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}
