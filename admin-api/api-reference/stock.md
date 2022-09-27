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
| pageNumber     | Number | Page number, when querying according to the update time, PageNumber is required and greater than 0. for example: 1                                                                           |

<details>

<summary>When querying according to skus, sku is required, and other parameters are optional, for example:</summary>

[https://developer.kakaclo.com/openapi/v1/product/stocks?skus=FSZW03961\_Y\_S\_NUB](https://test-developer.kakaclo.com/openapi/v1/product/stocks?skus=FSZW03961\_Y\_S\_NUB)

</details>

<details>

<summary>When querying based on the update time, either dateStartTime and dateEndTime are required, pageNumber is required, and other parameters are optional, for example:</summary>

[https://developer.kakaclo.com/openapi/v1/product/stocks?dateStartTime=2022-08-01T00:00:00Z\&pageNumber=1\&dateEndTime=2022-08-02T00:00:00Z](https://test-developer.kakaclo.com/openapi/v1/product/stocks?dateStartTime=2022-08-01T00:00:00Z\&pageNumber=1\&dateEndTime=2022-08-02T00:00:00Z)

</details>

## Response parameter

| Parameter name | Type   | Remark                                                                                               |
| -------------- | ------ | ---------------------------------------------------------------------------------------------------- |
| sku            | String | product unique code, for example: FSZW03961\_Y\_S\_NUB                                               |
| qty            | Number | Inventory quantity, for example: 20                                                                  |
| countryCode    | String | Country code of the country where the warehouse is located, for example: CN\_S                       |
| warehouseCode  | String | warehouse code, for example: G007                                                                    |
| total          | Number | The total number of query results(The total number of list data for paging query), for example: 1000 |
| pageNumber     | Number | page number, for example: 1                                                                          |
| pageSize       | Number | Quantity per page, for example: 30                                                                   |

{% hint style="info" %}
#### The countryCode and warehouseCode fields are reserved fields, and developers do not need to pay attention to the use of these two fields.
{% endhint %}

#### Response Example

```
{
    "code": 10000,
    "data": {
        "total": 1,
        "pageNumber": 1,
        "pageSize": 30,
        "list": [
            {
                "warehouseStockList": [
                    {
                        "countryCode": "CN_N",
                        "qty": 45,
                        "warehouseCode": "G006"
                    },
                    {
                        "countryCode": "CN_S",
                        "qty": 20,
                        "warehouseCode": "G007"
                    }
                ],
                "sku": "FSZW03961_Y_XL_NUB"
            }
        ]
    },
    "message": "Success！"
}
```

## Query stock

{% swagger method="get" path="/openapi/v1/product/stocks" baseUrl="" summary="get product stock" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="query" name="skus" type="String" required="true" %}
Commodity SKU code collections, specify the commodity SKU code query, each time a maximum of 30, Three options are required. for example:

**FSZW03961\_Y\_S\_NUB,FSZW03961\_Y\_XL\_NUB**
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

{% swagger-parameter in="query" name="pageNumber" type="Number" required="false" %}
Page number, when querying according to the update time, PageNumber is required and greater than 0. for example: 1
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Successfully query" %}
```json
{
    "code": 10000,
    "data": {
        "total": 2,
        "pageNumber": 1,
        "pageSize": 30,
        "list": [
            {
                "warehouseStockList": [
                    {
                        "countryCode": "CN_N",
                        "qty": 45,
                        "warehouseCode": "G006"
                    },
                    {
                        "countryCode": "CN_S",
                        "qty": 20,
                        "warehouseCode": "G007"
                    }
                ],
                "sku": "FSZW03961_Y_S_NUB"
            },
            {
                "warehouseStockList": [
                    {
                        "countryCode": "CN_N",
                        "qty": 45,
                        "warehouseCode": "G006"
                    },
                    {
                        "countryCode": "CN_S",
                        "qty": 20,
                        "warehouseCode": "G007"
                    }
                ],
                "sku": "FSZW03961_Y_XL_NUB"
            }
        ]
    },
    "message": "Success！"
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
