---
description: >-
  Creating orders will be grouped according to the location of the sku warehouse
  to generate multiple orders
---

# Order

## Order Item  Properties <a href="#response-parameter" id="response-parameter"></a>

| Parameter name    | Type        | Remark                                                                                                                                                                                                      |
| ----------------- | ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| sku               | string\[64] | sku                                                                                                                                                                                                         |
| quantity          | int\[16]    | quantity must be greater than 0                                                                                                                                                                             |
| ~~channelCode~~   | string\[32] | Channel code,This value is obtained by calling the Logistics Channel api. It is not required. If no value is passed or the channel is not matched, the standard channel will be used automatically.         |
| ~~warehouseCode~~ | string\[32] | Warehouse code,This value is obtained by calling the CountryAndWarehouse api, and it is not required. If no value is passed or the warehouse is not matched, the G007 warehouse will be used automatically. |
| channelType       | string\[16] | Channel type,This value defaults to 'Standard' as the standard logistics speed, if you need a faster logistics speed, you need to change the value to 'Express'.                                            |

## Order Address Properties <a href="#response-parameter" id="response-parameter"></a>

| Parameter name | Type        | Remark                                    |
| -------------- | ----------- | ----------------------------------------- |
| country        | string\[32] | shipping country shortcode required FR,US |
| phone          | string\[64] | address phone required                    |
| street1        | string\[64] | address street1 optional                  |
| street2        | string\[64] | address street2 optional                  |
| city           | string\[64] | address city optional                     |
| recipient      | string\[32] | address recipient required                |
| province       | string\[32] | address province required                 |
| zip            | string\[32] | address zip optional                      |
| ioss           | string\[32] | address ioss optional                     |
| vat            | string\[32] | address vat optional                      |

## Request Properties <a href="#response-parameter" id="response-parameter"></a>

```
{
    "orderAddresses": {
    "country": "US",
    "city": "Orlafasns",
    "phone": "07 82 24 67 93",
    "recipient": "Lffsollia Odfsdlena",
    "street1": " 7 rue  Rabelais",
    "province": " de Lofasfasire",
    "zip": "vsvs00v30"
  },
    "remark": "best order",
        "orderItemsList": [
          {
            "sku": "AMB01682_W_M_AU",
            "quantity": 1
          }
        ],
    "salePlatform": "KA",
    "customOrderId":"KA10001"
    "channelCode":"H008--Proactive",
    "warehouseCode":"H008"
}
```

{% hint style="info" %}
"channelCode" If no value is passed, the "Standard Shipping" logistics channel will be used by default
{% endhint %}

{% swagger method="post" path="/openapi/v2/order/orders" baseUrl="" summary="Create order related information" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="orderAddress" type="Object" required="true" %}
Order Address Properties
{% endswagger-parameter %}

{% swagger-parameter in="body" name="orderItemsList" type="Array" required="true" %}
Order Items Properties
{% endswagger-parameter %}

{% swagger-parameter in="body" name="remark" required="false" %}
order notes
{% endswagger-parameter %}

{% swagger-parameter in="body" name="salePlatform" %}
Amazon、Wish、eBay、Walmart、Groupon、IrobotBoxERP、Shopify、Aliexpress、OverStock、TopHatter、JoyBuy、Homedepot、Facebookshop、Mercari、Facebook Marketplace
{% endswagger-parameter %}

{% swagger-parameter in="body" name="customOrderId" %}
custom order number
{% endswagger-parameter %}

{% swagger-parameter in="body" name="channelCode" %}
From Logistics 

[channel API ](../order/channel.md#response-parameter-2)


{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "code": 10000,
    "message": "success",
    "data": 1000000371651
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

| Parameter name | Type        | Remark                                       |
| -------------- | ----------- | -------------------------------------------- |
| kkOrderId      | String\[32] | the order number is returned when successful |
