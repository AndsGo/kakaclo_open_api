---
description: View order related information
---

# Order List

## Order List Properties <a href="#response-parameter" id="response-parameter"></a>

| Parameter name                                     | Type                        | Remark                                                     |   |
| -------------------------------------------------- | --------------------------- | ---------------------------------------------------------- | - |
| shippingAddress                                    | object                      | address information                                        |   |
| id                                                 | number                      | order id                                                   |   |
| remark                                             | String                      | User comments                                              |   |
| status                                             | String                      | order status                                               |   |
| purchaseDate                                       | String                      | order time "2016-01-18T23:41:00Z"                          |   |
| payAt                                              | String                      | payment time "2016-01-18T23:41:00Z"                        |   |
| completedAt                                        | String                      | Complete time "2016-01-18T23:41:00Z"                       |   |
| cancelDate                                         | String                      | cancel time "2016-01-18T23:41:00Z"                         |   |
| refundDate                                         | String                      | refund time "2016-01-18T23:41:00Z"                         |   |
| warehouseId                                        | int\[16]                    | Order delivery warehouse, used for inventory replenishment |   |
| finalAmount                                        | BigDecimal                  | payment amount                                             |   |
| freightAmount                                      | BigDecimal                  | Order shipping amount                                      |   |
| skusAmount                                         | BigDecimal                  | total order item                                           |   |
| [orderItems](order-list.md#response-parameter-2)   | array of OrderItems objects | order sku information                                      |   |
| [fulfillments](order-list.md#response-parameter-1) | array of OrderItems objects | Order logistics information                                |   |
| createDate                                         | String                      | createAt time "2016-01-18T23:41:00Z"                       |   |
| updateDate                                         | String                      | updateAt time "2016-01-18T23:41:00Z"                       |   |

## Fulfillments Properties <a href="#response-parameter" id="response-parameter"></a>

| Parameter name                                   | Type                        | Remark                               |
| ------------------------------------------------ | --------------------------- | ------------------------------------ |
| id                                               | String                      | package id                           |
| deliveryTime                                     | String                      | delivery time "2016-01-18T23:41:00Z" |
| trackingCode                                     | String                      | order tracking number                |
| [orderItems](order-list.md#response-parameter-2) | array of OrderItems objects | Order logistics information          |
| logisticsProviders                               | String                      | order carrier                        |

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
| productNum     | int\[16]   | Sales volume                                                   |

## Shipping Address Properties <a href="#response-parameter" id="response-parameter"></a>

|           |        |                          |
| --------- | ------ | ------------------------ |
| country   | String | place an order country   |
| city      | String | place an order city      |
| phone     | String | place an order phone     |
| recipient | String | place an order recipient |
| street1   | String | place an order street1   |
| street2   | String | place an order street2   |
| province  | String | place an order province  |
| zip       | String | place an order zip       |
| vat       | String | place an order vat       |
| ioss      | String | place an order ioss      |

## Order Status

| status           | Remark                  |   |
| ---------------- | ----------------------- | - |
| waiting\_payment | Order pending payment   |   |
| cancel           | order cancelled         |   |
| waiting\_toship  | Order to be shipped     |   |
| refunding        | order refund            |   |
| refunded         | Order has been refunded |   |
| partial\_shipped | Order Partially Shipped |   |
| shipped          | Order shipped           |   |
| delivered        | order completed         |   |
| refund\_fail     | Order refund failed     |   |

{% swagger method="get" path="/openapi/v1/order/order" baseUrl="" summary="" %}
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
    "code":10000,
    "message":"kk.api.200",
    "data":{
        "list":[
          {     
      "id":124534634,
      "CustomOrderNumber":"123553453534",
      "remark":"",
      "status":"refund_fail",
      "purchaseDate": 2021,
      "payAt": 2021,
      "completedAt": 2021,
      "cancelDate": 1,
      "refundDate": 1,
    "shippingAddress": {
      "country": "CH",
      "city": "深圳",
      "phone": "137562586632",
      "recipient": "铁头男孩",
      "street1": "街道一",
      "street2": "街道二",
      "province": "湖南省",
      "zip": "邮编",
      "vat": "ssssaca",
      "ioss": ""
    },
      "warehouseCode": "pengd",
      "finalAmount": "15.01",
      "freightAmount": "15.03",
      "skusAmount": "15.03",
      "orderItems": [{
            "id":123456672,
            "imageUrl": "LKNASKONCOASNCLKNAS",
            "productName": "NC 女士缎面真丝睡衣..",
            "productNum": 2,
            "skuCode": "AMB00393",
            "option1": "red",
            "option2": "red",
            "option3": "red",
            "subtotal": 50,
            "purchasePrices": 50
          }],
"createAt":"",
"updateAt":"",
    "fulfillments": [
      {
        "deliveryTime": 137562586632,
        "trackingCode": "1ssdvsdv",
        "logisticsProviders": "小四快递",
        "orderItems": [
          {
            "id":123456672,
            "imageUrl": "LKNASKONCOASNCLKNAS",
            "productName": "NC 女士缎面真丝睡衣..",
            "productNum": 2,
            "skuCode": "AMB00393",
            "option1": "red",
            "option2": "red",
            "option3": "red",
            "subtotal": 50,
            "purchasePrices": 50
          }
        ],
        "id": ""
      }
    ]
}
        ],
        "total":"",
        "pageNumber":"",
        "pageSize":""
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
