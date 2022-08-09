---
description: >-
  Creating orders will be grouped according to the location of the sku warehouse
  to generate multiple orders
---

# Order

Creating orders will be grouped according to the location of the sku warehouse to generate multiple orders

## Order Items Properties <a href="#response-parameter" id="response-parameter"></a>

| Parameter name | Type        | Remark                          |
| -------------- | ----------- | ------------------------------- |
| sku            | string\[64] | sku                             |
| quantity       | number      | Quantity must be greater than 0 |

## Order Address Properties <a href="#response-parameter" id="response-parameter"></a>

| Parameter name | Type        | Remark                              |
| -------------- | ----------- | ----------------------------------- |
| countryCode    | string\[32] | Shipping country shortcode required |
| phone          | string\[64] | address phone required              |
| street1        | string\[64] | address street1 optional            |
| street2        | string\[64] | address street2 optional            |
| recipient      | string\[32] | address recipient required          |
| province       | string\[32] | address province  required          |
| zip            | string\[32] | address zip optional                |
| ioss           | string\[32] | address ioss optional               |
| vat            | string\[32] | address vat optional                |
| city           | string\[64] | address city optional               |

## Request Properties <a href="#response-parameter" id="response-parameter"></a>

```
```

{% swagger method="post" path="/openapi/v1/order/order" baseUrl="" summary="Create order related information" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="orderAddress" type="Object" required="true" %}
Order Address Properties
{% endswagger-parameter %}

{% swagger-parameter in="body" type="" name="CustomOrderNumber" required="true" %}
User-defined tracking number
{% endswagger-parameter %}

{% swagger-parameter in="body" name="SalePlatform" required="true" %}
Third-party platform tracking number
{% endswagger-parameter %}

{% swagger-parameter in="body" name="orderItemsList" type="Array" required="true" %}
Order Items Properties
{% endswagger-parameter %}

{% swagger-parameter in="body" name="remark" %}
order notes
{% endswagger-parameter %}
{% endswagger %}
