---
description: View order related information
---

# Query Order

{% swagger method="get" path="/openapi/v2/order/orders" baseUrl="" summary="" %}
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

## Order List Properties <a href="#response-parameter" id="response-parameter"></a>

<table><thead><tr><th>Parameter name</th><th>Type</th><th>Remark</th><th data-hidden></th></tr></thead><tbody><tr><td>id</td><td>number</td><td>order id</td><td></td></tr><tr><td>customOrderId</td><td>String</td><td>custom order id</td><td></td></tr><tr><td><a href="./#order-status">status</a></td><td>String</td><td>abnormal_order,waiting_payment,processing,completed,cancel</td><td></td></tr><tr><td><a href="./#financial-status">financialStatus</a></td><td>String</td><td>NULL,waiting,paid</td><td></td></tr><tr><td><a href="./#fulfillment-status">fulfillmentStatus</a></td><td>String</td><td>Logistics status: NULL,waiting_to_ship,fully_shipped,partially_shipped</td><td></td></tr><tr><td>refundStatus</td><td>String</td><td>NULL,refunding,partial_refund,refunded</td><td></td></tr><tr><td>purchaseDate</td><td>String</td><td>order time "2016-01-18T23:41:00Z"</td><td></td></tr><tr><td>payDate</td><td>String</td><td>payment time "2016-01-18T23:41:00Z"</td><td></td></tr><tr><td>completedDate</td><td>String</td><td>complete time "2016-01-18T23:41:00Z"</td><td></td></tr><tr><td>cancelDate</td><td>String</td><td>cancel time "2016-01-18T23:41:00Z"</td><td></td></tr><tr><td>refundDate</td><td>String</td><td>refund time "2016-01-18T23:41:00Z"</td><td></td></tr><tr><td>warehouseId</td><td>int[16]</td><td>order delivery warehouse, used for inventory replenishment</td><td></td></tr><tr><td>currencyCode</td><td>String</td><td>The default currency is USD</td><td></td></tr><tr><td>finalAmount</td><td>BigDecimal</td><td>payment amount</td><td></td></tr><tr><td>freightAmount</td><td>BigDecimal</td><td>order shipping amount</td><td></td></tr><tr><td>skusAmount</td><td>BigDecimal</td><td>total order item</td><td></td></tr><tr><td>promotionAmount</td><td>BigDecimal</td><td>discount amount</td><td></td></tr><tr><td>refundableAmount</td><td>BigDecimal</td><td>order allowable refund amount</td><td></td></tr><tr><td>refundedAmount</td><td>BigDecimal</td><td>the amount of the refunded portion of the item in the order</td><td></td></tr><tr><td><a href="./#response-parameter-1">fulfillments</a></td><td>array of OrderItems objects</td><td>order logistics information</td><td></td></tr><tr><td><a href="./#response-parameter-3">shippingAddress</a></td><td>object</td><td>address information</td><td></td></tr><tr><td><a href="./#response-parameter-2">orderItems</a></td><td>array of OrderItems objects</td><td>order sku information</td><td></td></tr><tr><td>remark</td><td>String</td><td>user comments</td><td></td></tr><tr><td>createDate</td><td>String</td><td>createAt time "2016-01-18T23:41:00Z"</td><td></td></tr><tr><td>updateDate</td><td>String</td><td>updateAt time "2016-01-18T23:41:00Z"</td><td></td></tr></tbody></table>

## Fulfillments Properties <a href="#response-parameter" id="response-parameter"></a>

<table><thead><tr><th>Parameter name</th><th>Type</th><th>Remark</th><th data-hidden></th></tr></thead><tbody><tr><td>id</td><td>String</td><td>package id</td><td></td></tr><tr><td>carrier</td><td>String</td><td>order carrier</td><td></td></tr><tr><td>carrierType</td><td>String</td><td>latest or last</td><td></td></tr><tr><td>trackingCode</td><td>String</td><td>order tracking number</td><td></td></tr><tr><td>logisticsSearchUrl</td><td>String</td><td><a href="https://t.17track.net/en?v=2#nums=WNBAA0202970436YQ">https://t.17track.net/en?v=2#nums=WNBAA0202970436YQ</a></td><td></td></tr><tr><td>deliveryTime</td><td>String</td><td>delivery time "2016-01-18T23:41:00Z"</td><td></td></tr><tr><td>i<a href="./#response-parameter-2">tems</a></td><td>array of OrderItems objects</td><td>order logistics information</td><td></td></tr><tr><td><a href="./#trackinginfo">trackingInfos</a></td><td>array of TrackingInfo objects</td><td>tracking Info list.<br>contains all the tracking information, the latest one being the first in the array</td><td></td></tr></tbody></table>

### Tracking Info

| Parameter name | Type   | Remark                |
| -------------- | ------ | --------------------- |
| carrier        | String | order carrier         |
| trackingCode   | String | order tracking number |

## Order Items Properties <a href="#response-parameter" id="response-parameter"></a>

| Parameter name                             | Type       | Remark                                                         |
| ------------------------------------------ | ---------- | -------------------------------------------------------------- |
| id                                         | number     | item id                                                        |
| itemId                                     | String     | item id                                                        |
| imageUrl                                   | String     | product picture                                                |
| productName                                | String     | product name                                                   |
| skuCode                                    | String     | sku                                                            |
| finalAmount                                | BigDecimal | unit sku payment amount                                        |
| promotionAmount                            | BigDecimal | sku sales unit  discount deduction amount                      |
| productNum                                 | int\[16]   | sales volume                                                   |
| subtotal                                   | BigDecimal | finalAmount\*productNum                                        |
| option1                                    | String     | sku attribute 1, contains size information, variable attribute |
| option2                                    | String     | sku attribute 2, contains size information, variable attribute |
| option3                                    | String     | sku attribute 3, contains size information, variable attribute |
| stockStatus                                | String     | normal,sold\_out                                               |
| [financialStatus](./#financial-status)     | String     | NULL,wating,paid                                               |
| [fulfillmentStatus](./#fulfillment-status) | String     | Logistics status: NULL,waiting\_to\_ship,completed             |
| [refundStatus](./#refund-status)           | String     | NULL,refunding,refunded                                        |

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

### Order Status

<table><thead><tr><th>Value</th><th>Remark</th><th data-hidden></th></tr></thead><tbody><tr><td>abnormal_order</td><td>an exception occurred in the order</td><td></td></tr><tr><td>waiting_payment</td><td>order pending payment</td><td></td></tr><tr><td>processing</td><td>the order is in processing</td><td></td></tr><tr><td>completed</td><td>order has been completed</td><td></td></tr><tr><td>cancel</td><td>order cancelled</td><td></td></tr></tbody></table>

### Financial Status

| Value   | Remark              |
| ------- | ------------------- |
| NULL    | initial empty state |
| waiting | waiting to pay      |
| paid    | paid                |

### Fulfillment Status

| Value              | Remark                                                                     |
| ------------------ | -------------------------------------------------------------------------- |
| NULL               | initial empty state                                                        |
| waiting\_to\_ship  | waiting to be shipped                                                      |
| partially\_shipped | part of the order has been shipped （the package does not have this status） |
| fully\_shipped     | all packages of the order have been shipped                                |
| completed          | the order confirms that the package has been received                      |

### Refund Status

| Value           | Remark                                                                 |
| --------------- | ---------------------------------------------------------------------- |
| NULL            | initial empty state                                                    |
| refunding       | the refund has been submitted and is waiting for the agency's response |
| partial\_refund | some items in the order have been refunded                             |
| refund          | the entire order has been refunded successfully                        |

