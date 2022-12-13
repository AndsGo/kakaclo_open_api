---
description: Create a refund order
---

# Refund Order

Create a refund order。

Cancel the order and get a refund. you can only do this when the order has not been shipped. This operation is performed asynchronously, and you can get the latest status information through "[Query ReFund](query-refund.md)"

The refund status can be updated for a maximum of 24 hours. Generally, the status will be updated within 1 hour.

### **Request Body Parameter**

| Name     | Type   | Description       |
| -------- | ------ | ----------------- |
| itemId   | String | Item Id           |
| skuCode  | String | Sku code          |
| quantity | Int    | Refund sku number |

{% swagger method="post" path="/openapi/v2/order/orders/{id}/refund" baseUrl="" summary="" %}
{% swagger-description %}

{% endswagger-description %}

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

## Examples

#### Refund some items

{% tabs %}
{% tab title="Request" %}
{% code overflow="wrap" lineNumbers="true" %}
```shell
curl -d '{"orderItems":[{"itemId":"120001","skuCode":"FSZW08923_R_L_NUB","quantity":1},{"itemId":"120002","skuCode":"FSZW08923_R_L_NUB","quantity":2}]}' \
-X POST "https://test-developer.kakaclo.com/openapi/openapi/v2/order/orders/10001/refund" \
-H "Authorization: Bearer {YOU_ACCES_TOKEN}" \
-H "Content-Type: application/json"
```
{% endcode %}
{% endtab %}

{% tab title="Response" %}
{% code overflow="wrap" %}
```json
HTTP/1.1 200 ok
{
    "code": 10000,
    "message": "ok",
    "data":10002
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### Refund the entire order

{% tabs %}
{% tab title="Request" %}
{% code overflow="wrap" lineNumbers="true" %}
```shell
curl -d '{}' \
-X POST "https://test-developer.kakaclo.com/openapi/openapi/v2/order/orders/10001/refund" \
-H "Authorization: Bearer {YOU_ACCES_TOKEN}" \
-H "Content-Type: application/json"
```
{% endcode %}
{% endtab %}

{% tab title="Response" %}
```json
HTTP/1.1 200 ok
{
    "code": 10000,
    "message": "ok",
    "data":10002
}
```
{% endtab %}
{% endtabs %}

