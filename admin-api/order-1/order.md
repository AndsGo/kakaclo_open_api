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
    "customOrderId":"KA10001",
    "channelType":"Standard"
}
```

{% hint style="info" %}
"channelCode" If no value is passed, the "Standard Shipping" logistics channel will be used by default
{% endhint %}

## Create order related information

<mark style="color:green;">`POST`</mark> `/openapi/v2/order/orders`

#### Request Body

| Name                                             | Type   | Description                                                                                                                                     |
| ------------------------------------------------ | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| orderAddress<mark style="color:red;">\*</mark>   | Object | Order Address Properties                                                                                                                        |
| orderItemsList<mark style="color:red;">\*</mark> | Array  | Order Items Properties                                                                                                                          |
| remark                                           | String | order notes                                                                                                                                     |
| salePlatform                                     | String | Amazon、Wish、eBay、Walmart、Groupon、IrobotBoxERP、Shopify、Aliexpress、OverStock、TopHatter、JoyBuy、Homedepot、Facebookshop、Mercari、Facebook Marketplace |
| channelCode                                      | String | From Logistics [channel API ](../order/channel.md#response-parameter-2)                                                                         |
| customOrderId                                    | String | custom order number                                                                                                                             |
| channelType<mark style="color:red;">\*</mark>    | String | Standard、Express                                                                                                                                |

{% tabs %}
{% tab title="200: OK " %}
```javascript
{
    "code": 10000,
    "message": "success",
    "data": 1000000371651
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

| Parameter name | Type        | Remark                                       |
| -------------- | ----------- | -------------------------------------------- |
| kkOrderId      | String\[32] | the order number is returned when successful |
