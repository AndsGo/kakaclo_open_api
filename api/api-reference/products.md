# Products

{% hint style="info" %}
This interface provides querying product information based on parameters. There are multiple sku under each spu.
{% endhint %}

## Request parameter

| Parameter name                    | Type   | Remark                                                                                                                                                                                                                                                                        |
| --------------------------------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| spus                              | String | the commodity SPU code query, each time a maximum of **30**, and one of the four options is required. for example: **AMN00432,AMN00433**                                                                                                                                      |
| skus                              | String | the commodity SKU code query, each time a maximum of **30**, and one of the four options is required. for example: **AMN00432\_B\_M,AMN00432\_B\_XL**                                                                                                                         |
| categoryId                        | Number | Category id, one of five is required, and pageNumber is required as a parameter. for example: **3654**                                                                                                                                                                        |
| dateStartTime                     | String | The start time of the **update time**, **UTC time**, cannot be greater than the end time, the time is accurate to the year, month, and day, and the hour, minute, and second are not verified, and one of the four options is required. for example: **2022-01-07T04:04:39Z** |
| dateEndTime                       | String | The end time of the **update time**, **UTC time**, cannot be less than the start time, the time is accurate to the year, month, and day, and the hour, minute, and second are not checked. One of the four options is required. for example: **2022-01-08T04:04:39Z**         |
| [sortType](products.md#undefined) | Number | Sort type, which can be sorted by different fields according to the given parameters. When not specified, the default is reversed by the update time. for example: 10                                                                                                         |
| sortBy                            | String | Sorting method, ascending order: **asc**, reverse order: **desc.** for example: desc                                                                                                                                                                                          |
| pageNumber                        | Number | Page number, when querying according to the update time, PageNumber is required and greater than 0.                                                                                                                                                                           |

#### sortType

| code | description |   |   |
| ---- | ----------- | - | - |
| 10   | salasVolume |   |   |
| 20   | stock       |   |   |
| 30   | price       |   |   |
| 40   | updateTime  |   |   |

## Response parameter

| Parameter name                     | Type       | Remark                                                                                                                                                                                                                                     |
| ---------------------------------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| kkProductId                        | Number     | Product unique Id,for example: 1207904                                                                                                                                                                                                     |
| spu                                | String     | Unique product name,for example: AMN00432                                                                                                                                                                                                  |
| productName                        | String     | Product name,for example: Casual/ Comfortable And Stylishwomen'S Velvet Jacket Suit                                                                                                                                                        |
| description                        | String     | Product Description,for example: Women'S Velvet Jacket                                                                                                                                                                                     |
| sizeImagePath                      | String     | Product size picture,for example: [https://img.kakaclo.com/image%2FAMN00432%2FAMN00432\_G\_XXL%2Fe674a874a5bd0a1d2839dbe8ab84ce1d.jpg](https://img.kakaclo.com/image%2FAMN00432%2FAMN00432\_G\_XXL%2Fe674a874a5bd0a1d2839dbe8ab84ce1d.jpg) |
| spuStatus                          | Number     | Commodity spu on the shelf status, 0-off the shelf; 1-on the shelf,for example: 1                                                                                                                                                          |
| categoryId                         | Number     | product category id,for example: 3654                                                                                                                                                                                                      |
| salesVolume                        | Number     | salesVolume. for example: 30                                                                                                                                                                                                               |
| minPrice                           | Decimal(2) | The minimum selling price of sku. for example: 15.30                                                                                                                                                                                       |
| stock                              | Number     | sku total inventory. for example: 1000                                                                                                                                                                                                     |
| createTime                         | Date       | creation time,for example: 2022-01-07T04:04:39Z                                                                                                                                                                                            |
| updateTime                         | Date       | update time,for example: 2022-01-07T04:04:39Z                                                                                                                                                                                              |
| [skuList](products.md#undefined)   | Arrays     | sku collection                                                                                                                                                                                                                             |
| [skuImgUrl](products.md#skuimgurl) | Arrays     | sku's picture collection                                                                                                                                                                                                                   |
| total                              | Number     | total data volume                                                                                                                                                                                                                          |
| pageNumber                         | Number     | current page number                                                                                                                                                                                                                        |
| pageSize                           | Number     | Quantity per page                                                                                                                                                                                                                          |

#### skuImgUrl

| Parameter name | Type   | Remark                                                                                                                                                                                                                                                                                             |
| -------------- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| skus           | Arrays | sku collection,for example: \[AMN00432\_B\_M,AMN00432\_B\_XL]                                                                                                                                                                                                                                      |
| imgUrl         | Arrays | Sku picture collection, this collection belongs to all sku of skus collection,for example: \[[https://img.kakaclo.com/image%2FAMN00432%2FAMN00432\_B\_S%2F5c4a540d4006e222a9a20bbc5b7b2d67.jpg](https://img.kakaclo.com/image%2FAMN00432%2FAMN00432\_B\_S%2F5c4a540d4006e222a9a20bbc5b7b2d67.jpg)] |

#### skuList

| Parameter name | Type       | Remark                                                                                                                                                                                                                                   |
| -------------- | ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| sku            | String     | product sku,for example: AMN00432\_B\_M                                                                                                                                                                                                  |
| skuName        | String     | Product sku name,for example: crossover design T-shirt                                                                                                                                                                                   |
| mainImg        | String     | Product sku main image,for example: [https://img.kakaclo.com/image%2FAMN00094%2FAMN00094\_B\_S%2F9f7aa16dec9b73ba46dda3b74f0f03eb.jpg](https://img.kakaclo.com/image%2FAMN00094%2FAMN00094\_B\_S%2F9f7aa16dec9b73ba46dda3b74f0f03eb.jpg) |
| packageLength  | Decimal(2) | Product length(CM),for example: 199.00                                                                                                                                                                                                   |
| packageWidth   | Decimal(2) | Product width(CM),for example: 32.00                                                                                                                                                                                                     |
| packageHeight  | Decimal(2) | Product height(CM),for example: 22.00                                                                                                                                                                                                    |
| packageWeight  | Decimal(2) | Product weight(CM),for example: 2.00                                                                                                                                                                                                     |
| cost           | Decimal(2) | commodity sku cost, Dollar,for example: 4.13                                                                                                                                                                                             |
| price          | Decimal(2) | commodity sku price，Dollar. for example: 5.37                                                                                                                                                                                            |
| stock          | Number     | sku inventory. for example: 100                                                                                                                                                                                                          |
| option1        | String     | sku attribute 1, contains size information, variable attribute,for example: {"name":"color","value":"Black"}                                                                                                                             |
| option2        | String     | sku attribute 2, contains color information, variable attribute,for example: {"name":"size","value":"XL"}                                                                                                                                |
| option3        | String     | sku attribute 3, including stamp information, variable attribute,for example: {"name":"print","value":"light blue new"}                                                                                                                  |
| material       | String     | Product sku material,for example: 95% Polyester,5% Spandex                                                                                                                                                                               |
| skuStatus      | Number     | The status of the product sku on the shelf, 0-off the shelf; 1-on the shelf,for example: 1                                                                                                                                               |

## Query Products

## get products

<mark style="color:blue;">`GET`</mark> `/openapi/v1/product/products`

#### Query Parameters

| Name                                            | Type   | Description                                                                                                                                                                                                                                                       |
| ----------------------------------------------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| spus<mark style="color:red;">\*</mark>          | String | the commodity SPU code query, each time a maximum of 30, and one of the four options is required. for example: AMN00432,AMN00433                                                                                                                                  |
| skus<mark style="color:red;">\*</mark>          | String | the commodity SKU code query, each time a maximum of 30, and one of the four options is required. for example: AMN00432\_B\_M,AMN00432\_B\_XL                                                                                                                     |
| categoryId<mark style="color:red;">\*</mark>    | Number | Category id, one of five is required, and pageNumber is required as a parameter. for example: 3654.                                                                                                                                                               |
| dateStartTime<mark style="color:red;">\*</mark> | String | The start time of the update time, UTC time, cannot be greater than the end time, the time is accurate to the year, month, and day, and the hour, minute, and second are not verified, and one of the four options is required. for example: 2022-01-07T04:04:39Z |
| sortType                                        | Number | Sort type, which can be sorted by different fields according to the given parameters. When not specified, the default is reversed by the update time. for example: 10.                                                                                            |
| sortBy                                          | String | <p>Sorting method, ascending order:</p><p><strong>asc</strong></p><p>, reverse order:</p><p><strong>desc.</strong></p><p>for example: desc.</p>                                                                                                                   |
| dateEndTime<mark style="color:red;">\*</mark>   | String | The end time of the update time, UTC time, cannot be less than the start time, the time is accurate to the year, month, and day, and the hour, minute, and second are not checked. One of the four options is required. for example: 2022-01-08T04:04:39Z         |
| pageNumber                                      | Number | Page number, when querying according to the update time, PageNumber is required and greater than 0.                                                                                                                                                               |

{% tabs %}
{% tab title="200 Successfully query" %}
```javascript
{
    "code":10000,
    "message":"kk.api.200",
    "data":{
        "list":[
            {
                "kkProductId":"",
                "spu":"",
                "productName":"",
                "description":"",
                "sizeImagePath":"",
                "spuStatus":"",
                "categoryId":"",
                "salesVolume":"",
                "minPrice":"",
                "stock":"",
                "createTime":"",
                "updateTime":"",
                "skuImgUrl":[
                    {
                        "skus":[],
                        "imgUrl":[]
                    }
                ]
                "skuList":[
                    {
                        "sku":"",
                        "skuName":"",
                        "mainImg":"",
                        "packageLength":"",
                        "packageWidth":"",
                        "packageHeight":"",
                        "packageWeight":"",
                        "cost":"",
                        "price":"",
                        "stock":"",
                        "option1":"",
                        "option2":"",
                        "option3":"",
                        "material":"",
                        "skuStatus":""
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
{% endtab %}

{% tab title="400: Bad Request Permission denied" %}

{% endtab %}
{% endtabs %}