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
    "data": {
        "total": 1,
        "pageNumber": 1,
        "pageSize": 10,
        "list": [
            {
                "purchaseDate": "2022-10-29T08:26:01Z",
                "completedAt": "2022-10-29T08:26:20Z",
                "payAt": "2022-10-29T08:26:20Z",
                "skusAmount": 3.7100,
                "freightAmount": 3.4800,
                "modifyDate": "2022-10-29T08:26:15Z",
                "orderItems": [
                    {
                        "productNum": 1,
                        "afterDiscountAmount": 3.7100,
                        "subtotal": 3.7100,
                        "imageUrl": "https://img.kakaclo.com/image%2FAMB01682%2FAMB01682_W_M_AU%2F6c3df5092b8bba370515d456e9c100b0.JPG",
                        "option3": "{\"name\":\"print\",\"value\":\"White Leopard\"}",
                        "purchasePrices": 7.4300,
                        "stockStatus": "normal",
                        "option1": "{\"name\":\"color\",\"value\":\"White Leopard\"}",
                        "id": "1105713",
                        "option2": "{\"name\":\"size\",\"value\":\"M\"}",
                        "promotionAmount": 3.7200,
                        "skuCode": "AMB01682_W_M_AU"
                    }
                ],
                "totalAmount": 7.1900,
                "warehouseId": 13,
                "shippingAddress": {
                    "zip": "vsvs00v30",
                    "country": "US",
                    "province": " de Lofasfasire",
                    "city": "Orlafasns",
                    "phone": "07 82 24 67 93",
                    "recipient": "Lffsollia Odfsdlena",
                    "street1": " 7 rue  Rabelais"
                },
                "id": "1000000506820",
                "status": "waiting_to_ship",
                "createDate": "2022-10-29T08:26:15Z"
            }
        ]
    },
    "message": "success"
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
