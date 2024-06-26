---
description: >-
  Creating orders will be grouped according to the location of the sku warehouse
  to generate multiple orders
---

# Order

## Order Item Properties <a href="#response-parameter" id="response-parameter"></a>

| Parameter name | Type        | Remark                          |
| -------------- | ----------- | ------------------------------- |
| sku            | string\[64] | sku                             |
| quantity       | int\[16]    | Quantity must be greater than 0 |

## Order Address Properties <a href="#response-parameter" id="response-parameter"></a>

| Parameter name | Type        | Remark                                    |
| -------------- | ----------- | ----------------------------------------- |
| country        | string\[32] | Shipping country shortcode required FR,US |
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
    "country": "FR",
    "city": "Orlafasns",
    "phone": "07 82 24 67 93",
    "recipient": "Lffsollia Odfsdlena",
    "street1": " 7 rue  Rabelais",
    "province": " de Lofasfasire",
    "zip": "vsvs00v30"
  },
    "remark": "I don't want this order",
        "orderItemsList": [
          {
            "sku": "FWXW00290_WHT_M",
            "quantity": 1
          }
        ],
    "CustomOrderNumber": "111",
    "SalePlatform": "KA"
 
}
```

## Response Properties <a href="#response-parameter" id="response-parameter"></a>

| Parameter name | Type        | Remark                                       |
| -------------- | ----------- | -------------------------------------------- |
| kkOrderId      | String\[32] | The order number is returned when successful |

## Create order related information

<mark style="color:green;">`POST`</mark> `/openapi/v1/order/order`

#### Request Body

| Name                                             | Type   | Description              |
| ------------------------------------------------ | ------ | ------------------------ |
| orderAddress<mark style="color:red;">\*</mark>   | Object | Order Address Properties |
| orderItemsList<mark style="color:red;">\*</mark> | Array  | Order Items Properties   |
| remark                                           | String | order notes              |

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
