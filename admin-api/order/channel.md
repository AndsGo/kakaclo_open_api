---
description: >-
  Logistics Channel API provides information like shipping method
  (channelNameEn), channel code, delivery time, or freight.
---

# Logistics Channel

## Products Properties <a href="#response-parameter" id="response-parameter"></a>

| Parameter name | Type        | Remark                                                                                                                                                                                                      |
| -------------- | ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| sku            | string\[64] | sku                                                                                                                                                                                                         |
| quantity       | int\[16]    | quantity must be greater than 0                                                                                                                                                                             |
| shipToCountry  | string\[12] | ship to country,shortcode required.Examples: FR,US                                                                                                                                                          |
| warehouseCode  | string\[32] | Warehouse code,This value is obtained by calling the CountryAndWarehouse api, and it is not required. If no value is passed or the warehouse is not matched, the G007 warehouse will be used automatically. |

## Request Properties <a href="#response-parameter" id="response-parameter"></a>

```
{
    "products": [
      {
       "sku": "FSZW06578_P_L_NUB",
       "quantity": 1
      }
    ],
    "shipToCountry": "US",
    "warehouseCode":"H008"
}
```

## Response Properties <a href="#response-parameter" id="response-parameter"></a>

| Parameter name           | Type   | Remark                                                                                                                               |
| ------------------------ | ------ | ------------------------------------------------------------------------------------------------------------------------------------ |
| channelCode              | String | Logistics channel code,This value is used on the [channelCode](order.md#response-parameter-2) parameter in the [Order API](order.md) |
| channelNameEn            | String | channel name(shipping method)                                                                                                        |
| estimatedFreight         | String | Shipping amount                                                                                                                      |
| estimatedFreightCurrency | String | USD                                                                                                                                  |
| deliveryTime             | String | For example: 6\~10 Business Days                                                                                                     |
| channelType              | String | channelType                                                                                                                          |

## Response Examples <a href="#response-parameter" id="response-parameter"></a>

```
{
    "code": 10000,
    "message": "success",
    "data": [
        {
            "channelCode": "WB004",
            "channelNameEn": "PP",
            "estimatedFreight": 6.45,
            "estimatedFreightCurrency": "USD",
            "deliveryTime": "3~5 Business Days",
            "channelType": "Standard"
        },
        {
            "channelCode": "WB001",
            "channelNameEn": "Wb clothing line （general goods ）",
            "estimatedFreight": 4.77,
            "estimatedFreightCurrency": "USD",
            "deliveryTime": "6~10 Business Days",
            "channelType": "Expedited"
        }
    ]
}
```

{% hint style="info" %}
data is sorted according to "deliveryTime " from small to large, deliveryTime the largest is "Standard Shipping".
{% endhint %}

{% hint style="info" %}
"estimatedFreight" is the shipping cost, mainly determined by weight (unit g) and "shipToCountry".The higher the weight, the higher the "estimatedFreight". "weight" is calculated by [sku's packageWeight](../api-reference/products.md#skulist) \*  "quantity"
{% endhint %}

<mark style="color:green;">`POST`</mark> `/openapi/v1/order/orders/channel`

#### Request Body

| Name                                            | Type   | Description                               |
| ----------------------------------------------- | ------ | ----------------------------------------- |
| shipToCountry<mark style="color:red;">\*</mark> | String | shipping country shortcode required FR,US |
| products<mark style="color:red;">\*</mark>      | Array  | Product information                       |

{% tabs %}
{% tab title="200: OK " %}
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
{% endtab %}

{% tab title="401: Unauthorized " %}
```javascript
{
    // Response
}
```
{% endtab %}
{% endtabs %}
