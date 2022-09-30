---
description: View order related information
---

# Query Order

## Order List Properties <a href="#response-parameter" id="response-parameter"></a>

| Parameter name                          | Type                        | Remark                                                     |   |
| --------------------------------------- | --------------------------- | ---------------------------------------------------------- | - |
| shippingAddress                         | object                      | address information                                        |   |
| id                                      | number                      | order id                                                   |   |
| remark                                  | String                      | user comments                                              |   |
| status                                  | String                      | order status                                               |   |
| purchaseDate                            | String                      | order time "2016-01-18T23:41:00Z"                          |   |
| payAt                                   | String                      | payment time "2016-01-18T23:41:00Z"                        |   |
| completedAt                             | String                      | complete time "2016-01-18T23:41:00Z"                       |   |
| cancelDate                              | String                      | cancel time "2016-01-18T23:41:00Z"                         |   |
| refundDate                              | String                      | refund time "2016-01-18T23:41:00Z"                         |   |
| warehouseId                             | int\[16]                    | order delivery warehouse, used for inventory replenishment |   |
| finalAmount                             | BigDecimal                  | payment amount                                             |   |
| freightAmount                           | BigDecimal                  | Order shipping amount                                      |   |
| skusAmount                              | BigDecimal                  | total order item                                           |   |
| [orderItems](./#response-parameter-2)   | array of OrderItems objects | order sku information                                      |   |
| [fulfillments](./#response-parameter-1) | array of OrderItems objects | order logistics information                                |   |
| createDate                              | String                      | createAt time "2016-01-18T23:41:00Z"                       |   |
| updateDate                              | String                      | updateAt time "2016-01-18T23:41:00Z"                       |   |

## Fulfillments Properties <a href="#response-parameter" id="response-parameter"></a>

| Parameter name                        | Type                        | Remark                                                                                                     |   |
| ------------------------------------- | --------------------------- | ---------------------------------------------------------------------------------------------------------- | - |
| id                                    | String                      | package id                                                                                                 |   |
| deliveryTime                          | String                      | delivery time "2016-01-18T23:41:00Z"                                                                       |   |
| trackingCode                          | String                      | order tracking number                                                                                      |   |
| [orderItems](./#response-parameter-2) | array of OrderItems objects | order logistics information                                                                                |   |
| logisticsSearchUrl                    | String                      | [https://t.17track.net/en?v=2#nums=WNBAA0202970436YQ](https://t.17track.net/en?v=2#nums=WNBAA0202970436YQ) |   |
| carrier                               | String                      | order carrier                                                                                              |   |

## Order Items Properties <a href="#response-parameter" id="response-parameter"></a>

| Parameter name | Type       | Remark                                                         |
| -------------- | ---------- | -------------------------------------------------------------- |
| id             | number     | item id                                                        |
| imageUrl       | String     | product picture                                                |
| productName    | String     | product name                                                   |
| skuCode        | String     | sku                                                            |
| subtotal       | BigDecimal | purchasePrices \*productNum                                    |
| purchasePrices | BigDecimal | sku sales unit price                                           |
| option1        | String     | sku attribute 1, contains size information, variable attribute |
| option2        | String     | sku attribute 2, contains size information, variable attribute |
| option3        | String     | sku attribute 3, contains size information, variable attribute |
| productNum     | int\[16]   | sales volume                                                   |

## Shipping Address Properties <a href="#response-parameter" id="response-parameter"></a>

| Parameter name | Type   | Remark                   |
| -------------- | ------ | ------------------------ |
| country        | String | place an order country   |
| city           | String | place an order city      |
| phone          | String | place an order phone     |
| recipient      | String | place an order recipient |
| street1        | String | place an order street1   |
| street2        | String | place an order street2   |
| province       | String | place an order province  |
| zip            | String | place an order zip       |
| vat            | String | place an order vat       |
| ioss           | String | place an order ioss      |

## Order Status

| Value               | Remark                  |   |
| ------------------- | ----------------------- | - |
| waiting\_payment    | order pending payment   |   |
| cancel              | order cancelled         |   |
| waiting\__to\__ship | order to be shipped     |   |
| refunding           | order refund            |   |
| refunded            | order has been refunded |   |
| partial\_shipped    | order Partially Shipped |   |
| shipped             | order shipped           |   |
| delivered           | order completed         |   |

{% swagger method="get" path="/openapi/v1/order/orders" baseUrl="" summary="" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="query" name="status" required="false" %}
order status, please use comma as separator, for example waiting_payment,cancel
{% endswagger-parameter %}

{% swagger-parameter in="query" name="createStartTime" required="false" %}
filter orders created at or before date, for example:

`2016-01-18T23:41:00Z`
{% endswagger-parameter %}

{% swagger-parameter in="query" name="createEndTime" required="false" %}
filter orders created at or before date, for example:

`2016-01-18T23:41:00Z`
{% endswagger-parameter %}

{% swagger-parameter in="query" name="updateStartTime" required="false" %}
filter orders last updated at or after date, for example:

`"2016-01-18T23:41:00Z"`
{% endswagger-parameter %}

{% swagger-parameter in="query" name="updateEndTime" required="false" %}
filter orders last updated at or before date, for example:

`2016-01-18T23:41:00Z`
{% endswagger-parameter %}

{% swagger-parameter in="query" name="ids" required="false" %}
Order's IDs, please use comma as separator, for example 1000000065617,1000000065618
{% endswagger-parameter %}

{% swagger-parameter in="query" name="pageNumber" type="number" required="false" %}
page numberlimit per page, default:

`10`

, maximum:

`250`
{% endswagger-parameter %}

{% swagger-parameter in="query" name="pageSize" type="number" required="false" %}
Default is 1
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Returns an array of Order objects" %}
```javascript
{
    "code": 10000,
    "message": "success",
    "data": {
        "vo": null,
        "list": [
            {
                "id": "1000000462144",
                "remark": null,
                "status": "shipped",
                "purchaseDate": "2022-09-28T03:32:17Z",
                "payAt": "2022-09-28T03:32:23Z",
                "completedAt": "2022-09-28T03:32:23Z",
                "cancelDate": null,
                "refundDate": null,
                "shippingAddress": {
                    "country": "VE",
                    "city": "Orleans",
                    "phone": "07 82 20 10 93",
                    "recipient": "Lollia Olena222",
                    "street1": " 7 rue Francois Rabelais",
                    "street2": null,
                    "province": "dddssssd",
                    "zip": "11111",
                    "vat": null,
                    "ioss": null
                },
                "warehouseId": 1,
                "totalAmount": 35.9800,
                "freightAmount": 22.8700,
                "skusAmount": 13.1100,
                "orderItems": [
                    {
                        "id": "1094003",
                        "imageUrl": "https://img.kakaclo.com/image%2FAMN01214%2FAMN01214_B_L%2F08e2ee632ea20d8925755d05530abb19.jpg",
                        "productName": null,
                        "productNum": 1,
                        "skuCode": "AMN01214_B_S_AK",
                        "option1": "{\"name\":\"color\",\"value\":\"Black\"}",
                        "option2": "{\"name\":\"size\",\"value\":\"PAT2\"}",
                        "option3": null,
                        "subtotal": 7.4300,
                        "purchasePrices": 7.4300
                    },
                    {
                        "id": "1094004",
                        "imageUrl": "https://img.kakaclo.com/image%2FFSZW07844%2FFSZW07844_NB_S_NUB%2Fc7f22ba71ef71427d2287cdab3b67703.jpg",
                        "productName": null,
                        "productNum": 1,
                        "skuCode": "FSZW07844_NB_S_NUB",
                        "option1": "{\"name\":\"color\", \"value\":\"Champlain color\"}",
                        "option2": "{\"name\":\"size\", \"value\":\"S\"}",
                        "option3": null,
                        "subtotal": 5.6800,
                        "purchasePrices": 5.6800
                    }
                ],
                "fulfillments": [
                    {
                        "deliveryTime": "2022-09-29T03:25:02Z",
                        "trackingCode": "RU948852435NL",
                        "id": "KA2022092811300049_1",
                        "carrier": "Post NL",
                        "logisticsSearchUrl": "http://193.112.127.239:8082",
                        "items": [
                            {
                                "id": "1094004",
                                "imageUrl": "https://img.kakaclo.com/image%2FFSZW07844%2FFSZW07844_NB_S_NUB%2Fc7f22ba71ef71427d2287cdab3b67703.jpg",
                                "productName": null,
                                "productNum": 1,
                                "skuCode": "FSZW07844_NB_S_NUB",
                                "option1": "{\"name\":\"color\", \"value\":\"Champlain color\"}",
                                "option2": "{\"name\":\"size\", \"value\":\"S\"}",
                                "option3": null,
                                "subtotal": 5.6800,
                                "purchasePrices": 5.6800
                            },
                            {
                                "id": "1094003",
                                "imageUrl": "https://img.kakaclo.com/image%2FAMN01214%2FAMN01214_B_L%2F08e2ee632ea20d8925755d05530abb19.jpg",
                                "productName": null,
                                "productNum": 1,
                                "skuCode": "AMN01214_B_S_AK",
                                "option1": "{\"name\":\"color\",\"value\":\"Black\"}",
                                "option2": "{\"name\":\"size\",\"value\":\"PAT2\"}",
                                "option3": null,
                                "subtotal": 7.4300,
                                "purchasePrices": 7.4300
                            }
                        ]
                    }
                ],
                "createDate": "2022-09-28T03:22:16Z",
                "modifyDate": "2022-09-29T08:27:21Z"
            }
        ],
        "total": 1,
        "pageNumber": 1,
        "pageSize": 10,
        "totalPageNumber": null,
        "modifyDate": null,
        "nextId": null
    }
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
