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

## Body  Properties <a href="#response-parameter" id="response-parameter"></a>

<table><thead><tr><th>Properties</th><th width="109">Type</th><th width="89">Require</th><th width="177">Sample</th><th>Properties description</th></tr></thead><tbody><tr><td>productName</td><td>string</td><td>N</td><td>Bule Skirt</td><td></td></tr><tr><td>demandNos</td><td>string array</td><td>N</td><td>["C202401164058"]</td><td>demandNo comes from the value in the response parameter data after the <a href="create-custom-order.md">Create Custom Order</a> interface is successful.</td></tr><tr><td>pageNumber</td><td>int</td><td>N</td><td>1</td><td>pageNumberstarts from 1, default is 1</td></tr><tr><td>pageSize</td><td>int</td><td>N</td><td>20</td><td>"page Size" represents the return list pagination, the number of custom order per page. Each page can retrieve up to 100 custom order records.default is 20</td></tr><tr><td>createTimeGe</td><td>int</td><td>N</td><td>1694309208</td><td><p>The fields "createTimeGe" and "createTimeLe" together constitute the filter condition for the creation time of the product. If you only fill in the "createTimeLe", and the "createTimeGe" is empty , then we will set the earliest time of the shop to the field "createTimeGe" by default. If you only fill in the "createTimeGe", and the "createTimeLe" is empty , then we will set the current time to the field "createTimeLe" by default.</p><p>The time search condition uses Unix timestamp in GMT (UTC+00:00).</p></td></tr><tr><td>createTimeLe</td><td>int</td><td>N</td><td>1694319208</td><td>Refer to the description of "createTimeGe".</td></tr><tr><td>updateTimeGe</td><td>int</td><td>N</td><td>1694319208</td><td>The fields "updateTimeGe" and "updateTimeLe" together constitute the filter condition for the update time of the product. If you only fill in the "updateTimeLe", and the "updateTimeGe" is empty , then we will set the earliest time of the shop to the field "updateTimeGe" by default. If you only fill in the "updateTimeGe", and the "updateTimeLe" is empty , then we will set the current time to the field "updateTimeLe" by default.</td></tr><tr><td>updateTimeLe</td><td>int</td><td>N</td><td>1694319208</td><td>Refer to the description of "updateTtimeGe".</td></tr></tbody></table>

## Reques Body  Example <a href="#response-parameter" id="response-parameter"></a>



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
                "modifyDate": 1645242794,
                "create_date": 1645242294,
                "productName": "prdouct_name",
                "paymentStatus": 2,
                "status": 2,
                "podStyle": "1,2",
                "type": 1,
                "customOrderId": "KA10001",
                "channelType": "Standard",
                "orderDetail": {
                    "orderAddresses": {
                        "country": "US",
                        "city": "Orlafasns",
                        "phone": "07 82 24 67 93",
                        "recipient": "Lffsollia Odfsdlena",
                        "street1": " 7 rue  Rabelais",
                        "province": "de Lofasfasire",
                        "zip": "vsvs00v30"
                    },
                    "remark": "best order",
                    "orderItemsList": [
                        {
                            "customerSku": "FSZW11087_P_FREESIZE_NUB",
                            "quantity": 1,
                            "importImage": [
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
