# Products

{% hint style="info" %}
This interface provides querying product information based on parameters. There are multiple sku under each spu.
{% endhint %}

## Product Properties

| Parameter name | Type   | Remark                                                             |
| -------------- | ------ | ------------------------------------------------------------------ |
| kkProductId    | Long   | Product unique Id                                                  |
| spu            | String | Unique product name                                                |
| productName    | String | Product name                                                       |
| description    | String | Product Description                                                |
| sizeImagePath  | String | Product size picture                                               |
| spuStatus      | Int    | Commodity spu on the shelf status, 0-off the shelf; 1-on the shelf |
| categoryId     | Int    | product category id                                                |
| createTime     | Date   | creation time                                                      |
| updateTime     | Date   | update time                                                        |
| skuList        | Arrays | sku collection                                                     |
| skuImgUrl      | Arrays | sku's picture collection                                           |
| total          | Int    | total data volume                                                  |
| pageNumber     | Int    | current page number                                                |
| skuImgUrl      | Arrays | sku's picture collection                                           |
| pageSize       | Int    | Quantity per page                                                  |

```
skuImgUrl
```

| Parameter name | Type   | Remark                                                                        |
| -------------- | ------ | ----------------------------------------------------------------------------- |
| skus           | Arrays | sku collection                                                                |
| imgUrl         | Arrays | Sku picture collection, this collection belongs to all sku of skus collection |

```
skuList
```

| Parameter name | Type    | Remark                                                                      |
| -------------- | ------- | --------------------------------------------------------------------------- |
| sku            | String  | product sku                                                                 |
| skuName        | String  | Product sku name                                                            |
| mainImg        | String  | Product sku main image                                                      |
| packageLength  | Decimal | Product length，unit(cm)                                                     |
| packageWidth   | Decimal | Product width，unit(cm)                                                      |
| packageHeight  | Decimal | Product height，unit(cm)                                                     |
| packageWeight  | Decimal | Product weight，unit(g)                                                      |
| cost           | Decimal | commodity sku cost, Dollar                                                  |
| price          | Decimal | commodity sku price，Dollar                                                  |
| option1        | String  | sku attribute 1, contains size information, variable attribute              |
| option2        | String  | sku attribute 2, contains color information, variable attribute             |
| option3        | String  | sku attribute 3, including stamp information, variable attribute            |
| material       | String  | Product sku material                                                        |
| skuStatus      | Int     | The status of the product sku on the shelf, 0-off the shelf; 1-on the shelf |

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
