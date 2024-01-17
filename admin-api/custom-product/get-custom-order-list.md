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

<table><thead><tr><th>Properties</th><th width="109">Type</th><th width="89">Require</th><th width="177">Sample</th><th>Properties description</th></tr></thead><tbody><tr><td>productName</td><td>string</td><td>N</td><td>Bule Skirt</td><td></td></tr><tr><td>demandNos</td><td>[]string</td><td>N</td><td>["C202401164058"]</td><td>demandNo comes from the value in the response parameter data after the <a href="create-custom-order.md">Create Custom Order</a> interface is successful.</td></tr><tr><td>pageNumber</td><td>int</td><td>N</td><td>1</td><td>pageNumberstarts from 1, default is 1</td></tr><tr><td>pageSize</td><td>int</td><td>N</td><td>20</td><td>"page Size" represents the return list pagination, the number of custom order per page. Each page can retrieve up to 100 custom order records.default is 20</td></tr><tr><td>createDateGe</td><td>int</td><td>N</td><td>1694309208000</td><td><p>The fields "createDateGe" and "createDateLe" together constitute the filter condition for the creation date of the product. If you only fill in the "createDateLe", and the "createDateGe" is empty , then we will set the earliest date of the shop to the field "createDateGe" by default. If you only fill in the "createDateGe", and the "createDateLe" is empty , then we will set the current time to the field "createDateLe" by default.</p><p>The time search condition uses 13-digit millisecond timestamp.</p></td></tr><tr><td>createDateLe</td><td>int</td><td>N</td><td>1694319208000</td><td>Refer to the description of "createDateGe".</td></tr><tr><td>updateDateGe</td><td>int</td><td>N</td><td>1694319208000</td><td>The fields "updateDateGe" and "updateDateLe" together constitute the filter condition for the update date of the product. If you only fill in the "updateDateLe", and the "updateDateGe" is empty , then we will set the earliest date of the shop to the field "updateDateGe" by default. If you only fill in the "updateDateGe", and the "updateDateLe" is empty , then we will set the current time to the field "updateDateLe" by default.</td></tr><tr><td>updateDateLe</td><td>int</td><td>N</td><td>1694319208000</td><td>Refer to the description of "updateTtimeGe".</td></tr></tbody></table>

## &#x20;<a href="#response-parameter" id="response-parameter"></a>

### Response Body Properties&#x20;

<table><thead><tr><th width="179">Properties</th><th width="104">Type</th><th>Sample</th><th>Properties description</th></tr></thead><tbody><tr><td>code</td><td>int</td><td>10000</td><td>Operation status code, only 10000 represents success</td></tr><tr><td>message</td><td>string</td><td>success</td><td>Operation description</td></tr><tr><td><a href="get-custom-order-list.md#response-data-properties">data</a></td><td>object</td><td></td><td>Return custom order data</td></tr></tbody></table>

### Response Data Properties&#x20;

<table><thead><tr><th width="179">Properties</th><th width="104">Type</th><th>Sample</th><th>Properties description</th></tr></thead><tbody><tr><td><a href="get-custom-order-list.md#response-list-properties">list</a></td><td>[]object</td><td></td><td>Returns a list array of data</td></tr><tr><td>total</td><td>int</td><td>1</td><td>Total number of data items</td></tr></tbody></table>

### Response list Properties&#x20;

<table><thead><tr><th width="179">Properties</th><th width="104">Type</th><th>Sample</th><th>Properties description</th></tr></thead><tbody><tr><td>productName</td><td>string</td><td>blue skirt</td><td>Product name</td></tr><tr><td>id</td><td>int</td><td>1</td><td>Table primary key ID</td></tr><tr><td>imageUrl</td><td>string</td><td>1</td><td>Pictures for reference use in customized designs</td></tr><tr><td>demandNo</td><td>string</td><td>C202401164058</td><td>Demand number of the current task</td></tr><tr><td>modifyDate</td><td>int</td><td>1645242294000</td><td>Modify date</td></tr><tr><td>createDate</td><td>int</td><td>1645242294000</td><td>Create date</td></tr><tr><td>status</td><td>int</td><td>2</td><td>Demand status 1. Unreceived: The kaka system has not received it 2. Received: The kaka system has received it 3. Completed: The order has been completed 4. Canceled: The order has been canceled</td></tr><tr><td>customOrderId</td><td>string</td><td>KA00001</td><td>customer order id</td></tr><tr><td>channelType</td><td>string</td><td>Standard</td><td>Logistics type, for example: standard,express, expedited</td></tr><tr><td><a href="get-custom-order-list.md#response-orderdetail-properties">orderDetail</a></td><td>object</td><td></td><td>custom order detail</td></tr><tr><td>description</td><td>string</td><td></td><td>Description of custom order</td></tr></tbody></table>

### Response orderDetail Properties

<table><thead><tr><th width="179">Properties</th><th width="104">Type</th><th>Sample</th><th>Properties description</th></tr></thead><tbody><tr><td><a href="create-custom-order.md#response-parameter-3">orderAddresses</a></td><td>object</td><td></td><td>Order address information</td></tr><tr><td>remark</td><td>string</td><td>order remark</td><td>Order remark</td></tr><tr><td><a href="create-custom-order.md#response-parameter-4">orderItems</a></td><td>[]object</td><td></td><td>Order item array</td></tr></tbody></table>

## Reques Body  Example <a href="#response-parameter" id="response-parameter"></a>

```json
{
    "productName": "blue skirt",
    "pageNumber": 1,
    "pageSize": 20,
    "createDateGe": 1694309208000,
    "createDateLe": 1694319208000,
    "demandNos": [
        "C202401164058"
    ],
    "updateDateGe": 1694319208000,
    "updateDateLe": 1694319208000
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
                "modifyDate": 1645242794000,
                "createDate": 1645242294000,
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
        "total": 1
    },
    "message": "success"
}
```
