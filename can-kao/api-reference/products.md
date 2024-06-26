# Products

{% hint style="info" %}
This interface provides querying product information based on parameters. There are multiple sku under each spu.
{% endhint %}

## Product Properties

| Parameter name                     | Type   | Remark                                                                                                                                                                                                                                     |
| ---------------------------------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| kkProductId                        | Long   | Product unique Id,for example: 1207904                                                                                                                                                                                                     |
| spu                                | String | Unique product name,for example: AMN00432                                                                                                                                                                                                  |
| productName                        | String | Product name,for example: Casual/ Comfortable And Stylishwomen'S Velvet Jacket Suit                                                                                                                                                        |
| description                        | String | Product Description,for example: Women'S Velvet Jacket                                                                                                                                                                                     |
| sizeImagePath                      | String | Product size picture,for example: [https://img.kakaclo.com/image%2FAMN00432%2FAMN00432\_G\_XXL%2Fe674a874a5bd0a1d2839dbe8ab84ce1d.jpg](https://img.kakaclo.com/image%2FAMN00432%2FAMN00432\_G\_XXL%2Fe674a874a5bd0a1d2839dbe8ab84ce1d.jpg) |
| spuStatus                          | Int    | Commodity spu on the shelf status, 0-off the shelf; 1-on the shelf,for example: 1                                                                                                                                                          |
| categoryId                         | Int    | product category id,for example: 3654                                                                                                                                                                                                      |
| createTime                         | Date   | creation time,for example: 2022-01-07T04:04:39Z                                                                                                                                                                                            |
| updateTime                         | Date   | update time,for example: 2022-01-07T04:04:39Z                                                                                                                                                                                              |
| [skuList](products.md#undefined)   | Arrays | sku collection                                                                                                                                                                                                                             |
| [skuImgUrl](products.md#skuimgurl) | Arrays | sku's picture collection                                                                                                                                                                                                                   |
| total                              | Int    | total data volume                                                                                                                                                                                                                          |
| pageNumber                         | Int    | current page number                                                                                                                                                                                                                        |
| pageSize                           | Int    | Quantity per page                                                                                                                                                                                                                          |

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
| price          | Decimal(2) | commodity sku price，Dollar,for example: 5.37                                                                                                                                                                                             |
| option1        | String     | sku attribute 1, contains size information, variable attribute,for example: {"name":"color","value":"Black"}                                                                                                                             |
| option2        | String     | sku attribute 2, contains color information, variable attribute,for example: {"name":"size","value":"XL"}                                                                                                                                |
| option3        | String     | sku attribute 3, including stamp information, variable attribute,for example: {"name":"print","value":"light blue new"}                                                                                                                  |
| material       | String     | Product sku material,for example: 95% Polyester,5% Spandex                                                                                                                                                                               |
| skuStatus      | Int        | The status of the product sku on the shelf, 0-off the shelf; 1-on the shelf,for example: 1                                                                                                                                               |

## Query Products

{% swagger baseUrl="" method="get" path="/openapi/v1/product/products" summary="get products" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="query" name="spus" type="Arrays" required="true" %}
the commodity SPU code query, each time a maximum of 30, and one of the four options is required.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="skus" type="Arrays" required="true" %}
the commodity SKU code query, each time a maximum of 30, and one of the four options is required.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="dateStartTime" type="String" required="true" %}
The start time of the update time, UTC time, cannot be greater than the end time, the time is accurate to the year, month, and day, and the hour, minute, and second are not verified, and one of the four options is required.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="dateEndTime" type="String" required="true" %}
The end time of the update time, UTC time, cannot be less than the start time, the time is accurate to the year, month, and day, and the hour, minute, and second are not checked. One of the four options is required.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="pageNumber" type="Int" required="false" %}
Page number, when querying according to the update time, PageNumber is required and greater than 0.
{% endswagger-parameter %}

{% swagger-response status="200" description="Successfully query" %}
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
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Permission denied" %}

{% endswagger-response %}
{% endswagger %}
