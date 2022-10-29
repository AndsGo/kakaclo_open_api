---
description: View order related information
---

# Query Order

## Order List Properties <a href="#response-parameter" id="response-parameter"></a>

<table><thead><tr><th>Parameter name</th><th>Type</th><th>Remark</th><th data-hidden></th></tr></thead><tbody><tr><td>shippingAddress</td><td>object</td><td>address information</td><td></td></tr><tr><td>id</td><td>number</td><td>order id</td><td></td></tr><tr><td>remark</td><td>String</td><td>user comments</td><td></td></tr><tr><td>status</td><td>String</td><td>order status</td><td></td></tr><tr><td>purchaseDate</td><td>String</td><td>order time "2016-01-18T23:41:00Z"</td><td></td></tr><tr><td>payAt</td><td>String</td><td>payment time "2016-01-18T23:41:00Z"</td><td></td></tr><tr><td>completedAt</td><td>String</td><td>complete time "2016-01-18T23:41:00Z"</td><td></td></tr><tr><td>cancelDate</td><td>String</td><td>cancel time "2016-01-18T23:41:00Z"</td><td></td></tr><tr><td>refundDate</td><td>String</td><td>refund time "2016-01-18T23:41:00Z"</td><td></td></tr><tr><td>warehouseId</td><td>int[16]</td><td>order delivery warehouse, used for inventory replenishment</td><td></td></tr><tr><td>finalAmount</td><td>BigDecimal</td><td>payment amount</td><td></td></tr><tr><td>freightAmount</td><td>BigDecimal</td><td>Order shipping amount</td><td></td></tr><tr><td>skusAmount</td><td>BigDecimal</td><td>total order item</td><td></td></tr><tr><td><a href="./#response-parameter-2">orderItems</a></td><td>array of OrderItems objects</td><td>order sku information</td><td></td></tr><tr><td><a href="./#response-parameter-1">fulfillments</a></td><td>array of OrderItems objects</td><td>order logistics information</td><td></td></tr><tr><td>createDate</td><td>String</td><td>createAt time "2016-01-18T23:41:00Z"</td><td></td></tr><tr><td>updateDate</td><td>String</td><td>updateAt time "2016-01-18T23:41:00Z"</td><td></td></tr></tbody></table>

## Fulfillments Properties <a href="#response-parameter" id="response-parameter"></a>

<table><thead><tr><th>Parameter name</th><th>Type</th><th>Remark</th><th data-hidden></th></tr></thead><tbody><tr><td>id</td><td>String</td><td>package id</td><td></td></tr><tr><td>deliveryTime</td><td>String</td><td>delivery time "2016-01-18T23:41:00Z"</td><td></td></tr><tr><td>trackingCode</td><td>String</td><td>order tracking number</td><td></td></tr><tr><td><a href="./#response-parameter-2">orderItems</a></td><td>array of OrderItems objects</td><td>order logistics information</td><td></td></tr><tr><td>logisticsSearchUrl</td><td>String</td><td><a href="https://t.17track.net/en?v=2#nums=WNBAA0202970436YQ">https://t.17track.net/en?v=2#nums=WNBAA0202970436YQ</a></td><td></td></tr><tr><td>carrier</td><td>String</td><td>order carrier</td><td></td></tr></tbody></table>

## Order Items Properties <a href="#response-parameter" id="response-parameter"></a>

| Parameter name      | Type       | Remark                                                         |
| ------------------- | ---------- | -------------------------------------------------------------- |
| id                  | number     | item id                                                        |
| imageUrl            | String     | product picture                                                |
| productName         | String     | product name                                                   |
| skuCode             | String     | sku                                                            |
| subtotal            | BigDecimal | purchasePrices \*productNum                                    |
| purchasePrices      | BigDecimal | sku sales unit price                                           |
| option1             | String     | sku attribute 1, contains size information, variable attribute |
| option2             | String     | sku attribute 2, contains size information, variable attribute |
| option3             | String     | sku attribute 3, contains size information, variable attribute |
| promotionAmount     | String     | promotionAmount                                                |
| afterDiscountAmount | String     | afterDiscountAmount                                            |
| stockStatus         | String     | normal,sold\_out                                               |
| productNum          | int\[16]   | sales volume                                                   |

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

<table><thead><tr><th>Value</th><th>Remark</th><th data-hidden></th></tr></thead><tbody><tr><td>waiting_payment</td><td>order pending payment</td><td></td></tr><tr><td>cancel</td><td>order cancelled</td><td></td></tr><tr><td>waiting_<em>to_</em>ship</td><td>order to be shipped</td><td></td></tr><tr><td>refunding</td><td>order refund</td><td></td></tr><tr><td>refunded</td><td>order has been refunded</td><td></td></tr><tr><td>partial_shipped</td><td>order Partially Shipped</td><td></td></tr><tr><td>shipped</td><td>order shipped</td><td></td></tr><tr><td>delivered</td><td>order completed</td><td></td></tr></tbody></table>

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
