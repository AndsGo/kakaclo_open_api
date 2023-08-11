---
description: >-
  Automatic Split Logistics Channel API provides information like logistics
  timeliness(channelType),delivery time, or freight.
---

# Automatic Split Logistics Channel

## Products Properties <a href="#response-parameter" id="response-parameter"></a>

| Parameter name | Type        | Remark                                             |
| -------------- | ----------- | -------------------------------------------------- |
| sku            | string\[64] | sku                                                |
| quantity       | int\[16]    | quantity must be greater than 0                    |
| shipToCountry  | string\[12] | ship to country,shortcode required.Examples: FR,US |

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

{% swagger method="post" path="/openapi/v2/order/orders/channel/automationSplit" baseUrl="" summary="" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="shipToCountry" required="true" %}
shipping country shortcode required FR,US
{% endswagger-parameter %}

{% swagger-parameter in="body" name="products" type="Array" required="true" %}
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

## Response Properties <a href="#response-parameter" id="response-parameter"></a>

| Parameter name           | Type   | Remark                                                                                                         |
| ------------------------ | ------ | -------------------------------------------------------------------------------------------------------------- |
| estimatedFreight         | String | Shipping amount                                                                                                |
| estimatedFreightCurrency | String | USD                                                                                                            |
| deliveryTime             | String | For example: 6\~10 Business Days                                                                               |
| channelType              | String | Channel type, 'Standard' is the standard logistics timeliness, 'Expedited' is the faster logistics timeliness. |

## Response Examples <a href="#response-parameter" id="response-parameter"></a>

```json
{
    "code": 10000,
    "data": [
        {
            "deliveryTime": "6~9 Business Days",
            "estimatedFreight": 6.1600,
            "channelType": "Express"
        },
        {
            "deliveryTime": "3~4 Business Days",
            "estimatedFreight": 24.2500,
            "channelType": "Expedited"
        },
        {
            "deliveryTime": "8~12 Business Days",
            "estimatedFreight": 5.0400,
            "channelType": "Standard"
        }
    ],
    "message": "Success!"
}
```

{% hint style="info" %}
data is sorted according to "deliveryTime " from small to large, deliveryTime the largest is "Standard Shipping".
{% endhint %}

{% hint style="info" %}
"estimatedFreight" is the shipping cost, mainly determined by weight (unit g) and "shipToCountry".The higher the weight, the higher the "estimatedFreight". "weight" is calculated by [sku's packageWeight](../api-reference/products.md#skulist) \*  "quantity"
{% endhint %}
