---
description: >-
  Logistics Channel API provide information like tracking company
  (channelNameEn) or freight
---

# Logistics Channel

## Products Properties <a href="#response-parameter" id="response-parameter"></a>

| Parameter name | Type        | Remark                          |
| -------------- | ----------- | ------------------------------- |
| sku            | string\[64] | sku                             |
| quantity       | int\[16]    | quantity must be greater than 0 |
| shipToCountry  | string\[12] | ship to country                 |

## Request Properties <a href="#response-parameter" id="response-parameter"></a>

```
{
            "products": [
                {
                    "sku": "FSZW06578_P_L_NUB",
                    "quantity": 1
                }
            ],
       
    "shipToCountry": "US"
}
```

## Response Properties <a href="#response-parameter" id="response-parameter"></a>

| Parameter name           | Type   | Remark                           |
| ------------------------ | ------ | -------------------------------- |
| channelCode              | String | Logistics channel code           |
| channelNameEn            | String | channel name                     |
| estimatedFreight         | String | Shipping amount                  |
| estimatedFreightCurrency | String | USD                              |
| deliveryTime             | String | For example: 6\~10 Business Days |

{% swagger method="post" path="/openapi/v1/order/orders/channel" baseUrl="" summary="" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="shipToCountry" required="true" %}
shipping country shortcode required FR,US
{% endswagger-parameter %}

{% swagger-parameter in="body" name="products" type="Array" %}
Product information
{% endswagger-parameter %}

{% swagger-response status="401: Unauthorized" description="" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "code": 10000,
    "message": "success",
    "data": [
        {
            "channelCode": "WB004",
            "channelNameEn": "PP",
            "estimatedFreight": 4.83,
            "estimatedFreightCurrency": "USD",
            "deliveryTime": "3~5 Business Days"
        },
        {
            "channelCode": "WB001",
            "channelNameEn": "Wb clothing line （general goods ）",
            "estimatedFreight": 3.61,
            "estimatedFreightCurrency": "USD",
            "deliveryTime": "6~10 Business Days"
        }
    ]
}
```
{% endswagger-response %}
{% endswagger %}
