---
description: View order related information
---

# Query Order

## Order List Properties <a href="#response-parameter" id="response-parameter"></a>

<table><thead><tr><th>Parameter name</th><th>Type</th><th>Remark</th><th data-hidden></th></tr></thead><tbody><tr><td>shippingAddress</td><td>object</td><td>address information</td><td></td></tr><tr><td>id</td><td>number</td><td>order id</td><td></td></tr><tr><td>customOrderId</td><td>String</td><td>custom order id</td><td></td></tr><tr><td>remark</td><td><code>String</code></td><td>user comments</td><td></td></tr><tr><td>status</td><td>String</td><td>order status</td><td></td></tr><tr><td>purchaseDate</td><td>String</td><td>order time "2016-01-18T23:41:00Z"</td><td></td></tr><tr><td>payAt</td><td>String</td><td>payment time "2016-01-18T23:41:00Z"</td><td></td></tr><tr><td>completedAt</td><td>String</td><td>complete time "2016-01-18T23:41:00Z"</td><td></td></tr><tr><td>cancelDate</td><td>String</td><td>cancel time "2016-01-18T23:41:00Z"</td><td></td></tr><tr><td>refundDate</td><td>String</td><td>refund time "2016-01-18T23:41:00Z"</td><td></td></tr><tr><td>warehouseId</td><td>int[16]</td><td>order delivery warehouse, used for inventory replenishment</td><td></td></tr><tr><td>finalAmount</td><td>BigDecimal</td><td>payment amount</td><td></td></tr><tr><td>freightAmount</td><td>BigDecimal</td><td>Order shipping amount</td><td></td></tr><tr><td>skusAmount</td><td>BigDecimal</td><td>total order item</td><td></td></tr><tr><td><a href="./#response-parameter-2">orderItems</a></td><td>array of OrderItems objects</td><td>order sku information</td><td></td></tr><tr><td><a href="./#response-parameter-1">fulfillments</a></td><td>array of OrderItems objects</td><td>order logistics information</td><td></td></tr><tr><td>createDate</td><td>String</td><td>createAt time "2016-01-18T23:41:00Z"</td><td></td></tr><tr><td>updateDate</td><td>String</td><td>updateAt time "2016-01-18T23:41:00Z"</td><td></td></tr></tbody></table>

## Fulfillments Properties <a href="#response-parameter" id="response-parameter"></a>

<table><thead><tr><th>Parameter name</th><th>Type</th><th>Remark</th><th data-hidden></th></tr></thead><tbody><tr><td>id</td><td>String</td><td>package id</td><td></td></tr><tr><td>deliveryTime</td><td>String</td><td>delivery time "2016-01-18T23:41:00Z"</td><td></td></tr><tr><td>trackingCode</td><td>String</td><td>order tracking number</td><td></td></tr><tr><td><a href="./#response-parameter-2">orderItems</a></td><td>array of OrderItems objects</td><td>order logistics information</td><td></td></tr><tr><td>logisticsSearchUrl</td><td>String</td><td><a href="https://t.17track.net/en?v=2#nums=WNBAA0202970436YQ">https://t.17track.net/en?v=2#nums=WNBAA0202970436YQ</a></td><td></td></tr><tr><td>carrier</td><td>String</td><td>order carrier</td><td></td></tr></tbody></table>

## Order Items Properties <a href="#response-parameter" id="response-parameter"></a>

| Parameter name  | Type       | Remark                                                         |
| --------------- | ---------- | -------------------------------------------------------------- |
| id              | number     | item id                                                        |
| imageUrl        | String     | product picture                                                |
| productName     | String     | product name                                                   |
| skuCode         | String     | sku                                                            |
| subtotal        | BigDecimal | purchasePrices \*productNum                                    |
| purchasePrices  | BigDecimal | sku sales unit price                                           |
| option1         | String     | sku attribute 1, contains size information, variable attribute |
| option2         | String     | sku attribute 2, contains size information, variable attribute |
| option3         | String     | sku attribute 3, contains size information, variable attribute |
| promotionAmount | String     | sku sales unit  promotionAmount                                |
| stockStatus     | String     | normal,sold\_out                                               |
| productNum      | int\[16]   | sales volume                                                   |

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
                "purchaseDate": "2022-11-01T06:21:20Z",
                "completedAt": "2022-11-01T06:21:21Z",
                "payAt": "2022-11-01T06:21:21Z",
                "skusAmount": 9.3200,
                "freightAmount": 10.8000,
                "modifyDate": "2022-11-01T06:21:12Z",
                "customOrderId": "sdasddfsdfdsf",
                "orderItems": [
                    {
                        "subtotal": 9.3200,
                        "imageUrl": "https://img.kakaclo.com/image%2FFSZW08517%2FFSZW08517_PEB_S_NUB%2Fd87cb7ffcb2c692367ef1c4a521a1c93.jpg",
                        "option3": "{\"name\":\"print\", \"value\":\"\"}",
                        "purchasePrices": 4.6600,
                        "stockStatus": "normal",
                        "option1": "{\"name\":\"color\", \"value\":\"Peacock blue\"}",
                        "id": "1108502",
                        "productNum": 2,
                        "option2": "{\"name\":\"size\", \"value\":\"XXL\"}",
                        "promotionAmount": 0.5000,
                        "skuCode": "FSZW08517_PEB_XXL_NUB"
                    }
                ],
                "totalAmount": 20.1200,
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
                "id": "1000000515397",
                "status": "waiting_to_ship",
                "createDate": "2022-11-01T06:21:12Z"
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
