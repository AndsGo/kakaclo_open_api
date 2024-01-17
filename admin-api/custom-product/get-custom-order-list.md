---
description: >-
  The Get Custom Order List interface can query the custom order list created
  through the interface or page.
---

# Get Custom Order List

### Endpoint



{% swagger method="post" path="s/search" baseUrl="/openapi/v1/product/custom/order" summary="" %}
{% swagger-description %}

{% endswagger-description %}
{% endswagger %}

## Header <a href="#response-parameter" id="response-parameter"></a>

For common header, refer to [How to call KakaClo Shop APIs - Common Headers](../../kuai-su-kai-shi.md)

```
curl --request POST
     --url 'https://developer.kakaclo.com/openapi/v1/product/custom/orders/search'
     --header 'Accept: application/json'
     --header 'Authorization: Bearer YOU_ACCES-TOKEN'
```

## Request Body  Properties <a href="#response-parameter" id="response-parameter"></a>

<table><thead><tr><th>Properties</th><th width="109">Type</th><th width="89">Require</th><th width="177">Sample</th><th>Properties description</th></tr></thead><tbody><tr><td>productName</td><td>string</td><td>N</td><td>Bule Skirt</td><td></td></tr><tr><td>demandNos</td><td>[]string</td><td>N</td><td>["C202401164058"]</td><td>demandNo comes from the value in the response parameter data after the <a href="create-custom-order.md">Create Custom Order</a> interface is successful.</td></tr><tr><td>pageNumber</td><td>int</td><td>N</td><td>1</td><td>pageNumberstarts from 1, default is 1</td></tr><tr><td>pageSize</td><td>int</td><td>N</td><td>20</td><td>"page Size" represents the return list pagination, the number of custom order per page. Each page can retrieve up to 100 custom order records.default is 20</td></tr><tr><td>createTimeGe</td><td>int</td><td>N</td><td>1694309208</td><td><p>The fields "createTimeGe" and "createTimeLe" together constitute the filter condition for the creation time of the product. If you only fill in the "createTimeLe", and the "createTimeGe" is empty , then we will set the earliest time of the shop to the field "createTimeGe" by default. If you only fill in the "createTimeGe", and the "createTimeLe" is empty , then we will set the current time to the field "createTimeLe" by default.</p><p>The time search condition uses Unix timestamp in GMT (UTC+00:00).</p></td></tr><tr><td>createTimeLe</td><td>int</td><td>N</td><td>1694319208</td><td>Refer to the description of "createTimeGe".</td></tr><tr><td>updateTimeGe</td><td>int</td><td>N</td><td>1694319208</td><td>The fields "updateTimeGe" and "updateTimeLe" together constitute the filter condition for the update time of the product. If you only fill in the "updateTimeLe", and the "updateTimeGe" is empty , then we will set the earliest time of the shop to the field "updateTimeGe" by default. If you only fill in the "updateTimeGe", and the "updateTimeLe" is empty , then we will set the current time to the field "updateTimeLe" by default.</td></tr><tr><td>updateTimeLe</td><td>int</td><td>N</td><td>1694319208</td><td>Refer to the description of "updateTtimeGe".</td></tr></tbody></table>

## &#x20;<a href="#response-parameter" id="response-parameter"></a>

### Response Body Properties&#x20;

<table><thead><tr><th width="179">Properties</th><th width="104">Type</th><th>Sample</th><th>Properties description</th></tr></thead><tbody><tr><td>code</td><td>int</td><td>10000</td><td>Operation status code, only 10000 represents success</td></tr><tr><td>message</td><td>string</td><td>success</td><td>Operation description</td></tr><tr><td><a href="get-custom-order-list.md#response-data-properties">data</a></td><td>object</td><td></td><td>Return custom order data</td></tr></tbody></table>

### Response Data Properties&#x20;

<table><thead><tr><th width="179">Properties</th><th width="104">Type</th><th>Sample</th><th>Properties description</th></tr></thead><tbody><tr><td><a href="get-custom-order-list.md#response-list-properties">list</a></td><td>[]object</td><td></td><td>Returns a list array of data</td></tr><tr><td>total</td><td>int</td><td>1</td><td>Total number of data items</td></tr><tr><td>pageNumber</td><td>int</td><td>1</td><td>page number</td></tr><tr><td>pageSize</td><td>int</td><td>20</td><td>page size</td></tr></tbody></table>

### Response list Properties&#x20;

<table><thead><tr><th width="179">Properties</th><th width="104">Type</th><th>Sample</th><th>Properties description</th></tr></thead><tbody><tr><td>productName</td><td>string</td><td>blue skirt</td><td>Product name</td></tr><tr><td>id</td><td>int</td><td>1</td><td>Table primary key ID</td></tr><tr><td>imageUrl</td><td>string</td><td>1</td><td>Pictures for reference use in customized designs</td></tr><tr><td>demandNo</td><td>string</td><td>C202401164058</td><td>demand number of the current task</td></tr><tr><td>modifyTime</td><td>int</td><td>1645242294</td><td>modify time</td></tr><tr><td>createTime</td><td>int</td><td>1645242294</td><td>create time</td></tr><tr><td>status</td><td>int</td><td>2</td><td>Demand status 1. Unreceived: The kaka system has not received it 2. Received: The kaka system has received it 3. Completed: The order has been completed 4. Canceled: The order has been canceled</td></tr><tr><td>customOrderId</td><td>string</td><td>KA00001</td><td>customer order id</td></tr><tr><td>channelType</td><td>string</td><td>Standard</td><td>Logistics type, for example: standard,express, expedited</td></tr><tr><td><a href="get-custom-order-list.md#response-orderdetail-properties">orderDetail</a></td><td>object</td><td></td><td>custom order detail</td></tr><tr><td>description</td><td>string</td><td></td><td>Description of custom order</td></tr></tbody></table>

### Response orderDetail Properties

<table><thead><tr><th width="179">Properties</th><th width="104">Type</th><th>Sample</th><th>Properties description</th></tr></thead><tbody><tr><td><a href="create-custom-order.md#response-parameter-3">orderAddresses</a></td><td>object</td><td></td><td>Order address information</td></tr><tr><td>remark</td><td>string</td><td>order remark</td><td>Order remark</td></tr><tr><td><a href="create-custom-order.md#response-parameter-4">orderItems</a></td><td>[]object</td><td></td><td>Order item array</td></tr></tbody></table>

## Reques Body  Example <a href="#response-parameter" id="response-parameter"></a>

```json
{
    "productName": "blue skirt",
    "pageNumber": 1,
    "pageSize": 20,
    "createTimeGe": 1694309208,
    "createTimeLe": 1694319208,
    "demandNos": [
        "C202401164058"
    ],
    "updateTimeGe": 1694319208,
    "updateTimeLe": 1694319208
}
```

## Response Body  Example <a href="#response-parameter" id="response-parameter"></a>

```json
{
    "code": 10000,
    "data": {
        "list": [
            {
                "demandNo": "C202401164058",
                "id": 5,
                "imageUrl": "https://hbo-shenzhen.oss-cn-shenzhen.aliyuncs.com/image/FSZW02472/FSZW02472_A_3XL_NUB/0d012644aa46048d4ddfbb105edc3767.jpg",
                "modifyTime": 1645242794,
                "createTime": 1645242294,
                "productName": "prdouct_name",
                "status": 2,
                "customOrderId": "KA10001",
                "channelType": "Standard",
                "description": "custom order description~~",
                "orderDetail": {
                    "orderAddresses": {
                        "country": "US",
                        "city": "Orlafasns",
                        "phone": "07 82 24 67 93",
                        "recipient": "Lffsollia Odfsdlena",
                        "street1": "7 rue  Rabelais",
                        "street2": "",
                        "province": "de Lofasfasire",
                        "zip": "vsvs00v30"
                    },
                    "remark": "best order",
                    "orderItems": [
                        {
                            "customerSku": "FSZW11087_P_FREESIZE_NUB",
                            "quantity": 1,
                            "imageUrls": [
                                "https://img.kakaclo.com/image%2FFSZW11087%2FFSZW11087_P_FREESIZE_NUB%2Fda299fa3e37b65654bc5153c325b8b00.jpg"
                            ],
                            "remark": "test custom order",
                            "color": "Pink",
                            "size": "XL",
                            "print": "Positioning printing",
                            "material": "Acrylic",
                            "printUniqueCode": "",
                            "customerBarcode": "FSZW11087_P_FREESIZE_NUB",
                            "uniqueCodeType": "3"
                        }
                    ]
                }
            }
        ],
        "pageNumber": 1,
        "pageSize": 20,
        "total": 1
    },
    "message": "success"
}
```
