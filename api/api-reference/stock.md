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

## Response parameter

| Parameter name | Type   | Remark                                                 |
| -------------- | ------ | ------------------------------------------------------ |
| sku            | String | product unique code, for example: FSZW03961\_Y\_S\_NUB |
| qty            | Number | Inventory quantity, for example: 20                    |
| countryCode    | String | Shipping country code, for example: CN\_S              |
| warehouseCode  | String | warehouse code, for example: G007                      |
| total          | Number | total data volume, for example: 1000                   |
| pageNumber     | Number | page number, for example: 1                            |
| pageSize       | Number | Quantity per page, for example: 30                     |

## Query stock

## get product stock

<mark style="color:blue;">`GET`</mark> `/openapi/v1/product/stocks`

#### Query Parameters

| Name                                            | Type   | Description                                                                                                                                                                                                  |
| ----------------------------------------------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| skus<mark style="color:red;">\*</mark>          | String | <p>Commodity SKU code collections, specify the commodity SKU code query, each time a maximum of 30, Three options are required. for example:</p><p><strong>FSZW03961_Y_S_NUB,FSZW03961_Y_XL_NUB</strong></p> |
| warehouseCode                                   | String | warehouse code. for example: G007                                                                                                                                                                            |
| dateStartTime<mark style="color:red;">\*</mark> | String | Inventory update start time, one of the three is required. for example: 2022-03-25T04:00:30Z                                                                                                                 |
| dateEndTime<mark style="color:red;">\*</mark>   | String | Inventory update end time, one of the three is required. for example: 2022-03-26T04:00:30Z                                                                                                                   |
| pageNumber                                      | Number | Page number, when querying according to the update time, PageNumber is required and greater than 0. for example: 1                                                                                           |

{% tabs %}
{% tab title="200: OK Successfully query" %}
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
{% endtab %}

{% tab title="400: Bad Request " %}
```javascript
{
    // Response
}
```
{% endtab %}
{% endtabs %}
