---
description: View order related information
---

# Order List

## Order List Properties <a href="#response-parameter" id="response-parameter"></a>

| Parameter name    | Type                        | Remark                                                     |   |
| ----------------- | --------------------------- | ---------------------------------------------------------- | - |
| shippingAddress   | object                      | address information                                        |   |
| id                | number                      | order id                                                   |   |
| CustomOrderNumber | String                      | Customer-defined tracking number                           |   |
| remark            | String                      | User comments                                              |   |
| status            | String                      |                                                            |   |
| purchaseDate      | String                      | order time "2016-01-18T23:41:00Z"                          |   |
| payAt             | String                      | payment time "2016-01-18T23:41:00Z"                        |   |
| completedAt       | String                      | Complete time  "2016-01-18T23:41:00Z"                      |   |
| cancelDate        | String                      | cancel time  "2016-01-18T23:41:00Z"                        |   |
| refundDate        | String                      | refund time "2016-01-18T23:41:00Z"                         |   |
| warehouseCode     | String\[64]                 | Order delivery warehouse, used for inventory replenishment |   |
| finalAmount       | BigDecimal                  | payment amount                                             |   |
| freightAmount     | BigDecimal                  | Order shipping amount                                      |   |
| skusAmount        | BigDecimal                  | total order item                                           |   |
| orderItems        | array of OrderItems objects | order sku information                                      |   |
| createAt          | String                      | createAt time  "2016-01-18T23:41:00Z"                      |   |
| updateAt          | String                      | updateAt time  "2016-01-18T23:41:00Z"                      |   |

## Order Items Properties <a href="#response-parameter" id="response-parameter"></a>

| Parameter name | Type       | Remark                                                         |
| -------------- | ---------- | -------------------------------------------------------------- |
| id             | number     | item id                                                        |
| imageUrl       | String     | product picture                                                |
| productName    | String     | product name                                                   |
| skuCode        | String     | sku                                                            |
| subtotal       | BigDecimal | purchasePrices  \*productNum                                   |
| purchasePrices | BigDecimal | sku sales unit price                                           |
| option1        | String     | sku attribute 1, contains size information, variable attribute |
| option2        | String     | sku attribute 2, contains size information, variable attribute |
| option3        | String     | sku attribute 3, contains size information, variable attribute |
| productNum     | Number     | Sales volume                                                   |
|                |            |                                                                |

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

{% swagger method="get" path="/openapi/v1/order/order" baseUrl="" summary="" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="query" name="status" %}
order status, please use comma as separator, for example  waiting_payment,cancel
{% endswagger-parameter %}

{% swagger-parameter in="query" name="createdAtMin" %}
filter orders created at or before date, for example: 

`2016-01-18T23:41:00Z`
{% endswagger-parameter %}

{% swagger-parameter in="query" name="createdAtMax" %}
filter orders created at or before date, for example: 

`2016-01-18T23:41:00Z`
{% endswagger-parameter %}

{% swagger-parameter in="query" name="updatedAtMin" %}
filter orders last updated at or after date, for example: 

`"2016-01-18T23:41:00Z"`
{% endswagger-parameter %}

{% swagger-parameter in="query" name="updatedAtMax" %}
filter orders last updated at or before date, for example: 

`2016-01-18T23:41:00Z`
{% endswagger-parameter %}

{% swagger-parameter in="query" name="ids" %}
Order's IDs, please use comma as separator, for example 1000000065617,1000000065618
{% endswagger-parameter %}

{% swagger-parameter in="query" name="pageNumber" type="number" %}
page numberlimit per page, default: 

`10`

, maximum: 

`250`
{% endswagger-parameter %}

{% swagger-parameter in="query" name="pageSize" type="number" %}

{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Returns an array of Order objects" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}
