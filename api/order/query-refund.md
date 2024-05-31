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
| remark         | String | order notes         |
| refundStatus   | String | refund status       |

<mark style="color:blue;">`GET`</mark> `https://test-developer.kakaclo.com/order/refund`

#### Query Parameters

| Name       | Type   | Description                                                                          |
| ---------- | ------ | ------------------------------------------------------------------------------------ |
| refundNo   | String | refund's Nos, please use comma as separator, for example 1000000065617,1000000065618 |
| ids        | String | Order's IDs, please use comma as separator, for example 1000000065617,1000000065618  |
| pageNumber | String |                                                                                      |
| pageSize   | String |                                                                                      |

{% tabs %}
{% tab title="200: OK " %}
```javascript
{
    // Response
}
```
{% endtab %}

{% tab title="200: OK " %}
```javascript
{
    // Response
}
```
{% endtab %}
{% endtabs %}
