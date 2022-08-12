# Stock

{% hint style="info" %}
This interface is to query sku inventory. The same sku may belong to different repositories.
{% endhint %}

## Request parameter

| Parameter name | Type   | Remark                                                                                                                                                                                       |
| -------------- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| skus           | String | Commodity SKU code collections, specify the commodity SKU code query, each time a maximum of **30**, Three options are required. for example: **FSZW03961\_Y\_S\_NUB,FSZW03961\_Y\_XL\_NUB** |
| warehouseCode  | String | warehouse code. for example: **G007**                                                                                                                                                        |
| dateStartTime  | String | Inventory update start time, one of the three is required. for example: **2022-03-25T04:00:30Z**                                                                                             |
| dateEndTime    | String | Inventory update end time, one of the three is required. for example: **2022-03-26T04:00:30Z**                                                                                               |
| pageNumber     | Int    | Page number, when querying according to the update time, PageNumber is required and greater than 0. for example: 1                                                                           |

## Response parameter

| Parameter name | Type   | Remark                                                 |
| -------------- | ------ | ------------------------------------------------------ |
| sku            | String | product unique code, for example: FSZW03961\_Y\_S\_NUB |
| qty            | Int    | Inventory quantity, for example: 20                    |
| countryCode    | String | Shipping country code, for example: CN\_S              |
| warehouseCode  | String | warehouse code, for example: G007                      |
| total          | Int    | total data volume, for example: 1000                   |
| pageNumber     | Int    | page number, for example: 1                            |
| pageSize       | Int    | Quantity per page, for example: 30                     |

## Query stock

{% swagger method="get" path="/openapi/v1/product/stocks" baseUrl="" summary="get product stock" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="query" name="skus" type="String" required="true" %}
Commodity SKU code collections, specify the commodity SKU code query, each time a maximum of 30, Three options are required. for example: 

**FSZW03961_Y_S_NUB,FSZW03961_Y_XL_NUB**
{% endswagger-parameter %}

{% swagger-parameter in="query" name="warehouseCode" type="String" required="false" %}
warehouse code. for example: G007
{% endswagger-parameter %}

{% swagger-parameter in="query" name="dateStartTime" type="String" required="true" %}
Inventory update start time, one of the three is required. for example: 2022-03-25T04:00:30Z
{% endswagger-parameter %}

{% swagger-parameter in="query" name="dateEndTime" type="String" required="true" %}
Inventory update end time, one of the three is required. for example: 2022-03-26T04:00:30Z
{% endswagger-parameter %}

{% swagger-parameter in="query" name="pageNumber" type="Int" required="false" %}
Page number, when querying according to the update time, PageNumber is required and greater than 0. for example: 1
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Successfully query" %}
```javascript
{
    "code":10000,
    "message":"kk.api.200",
    "data":{
        "list":[
            {
                "sku":"",
                "warehouseStockList":[
                    {
                        "warehouseCode":"",
                        "qty":"",
                        "countryCode":""
                    }
                ]
            }
        ]
    }
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}
