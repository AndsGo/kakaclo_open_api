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
| [sortType](products.md#undefined) | String | Sort type, which can be sorted by different fields according to the given parameters. When not specified, the default is reversed by the update time. for example: salasVolume                                                                                                |
| sortBy                            | String | Sorting method, ascending order: **asc**, reverse order: **desc.** for example: desc                                                                                                                                                                                          |
| pageNumber                        | Number | Page number, when querying according to the update time, PageNumber is required and greater than 0.                                                                                                                                                                           |

#### sortType

| sort field  | definition          | field       |   |   |
| ----------- | ------------------- | ----------- | - | - |
| salasVolume | product salasVolume | salasVolume |   |   |
| stock       | product stock       | stock       |   |   |
| price       | product price       | price       |   |   |
| updateTime  | updateTime          | updateTime  |   |   |

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
| fullCategoryName                   | String     | Product classification full path, for example: Women/Activewear/Suit                                                                                                                                                                       |
| salesVolume                        | Number     | salesVolume. for example: 30                                                                                                                                                                                                               |
| attributesJson                     | String     | Product attribute fields. for example: {"style": "Grace", "season": "Spring-Summer", "pattern": "Floral print", "material": "Cotton blend", "sleeve\_type": "Puffed sleeve", "sleeve\_length": "Half sleeve"}                              |
| price                              | Decimal(2) | The minimum selling price of sku. for example: 15.30                                                                                                                                                                                       |
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

{% swagger baseUrl="" method="get" path="/openapi/v1/product/products" summary="get products" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="query" name="spus" type="String" required="true" %}
the commodity SPU code query, each time a maximum of 30, and one of the four options is required. for example: AMN00432,AMN00433
{% endswagger-parameter %}

{% swagger-parameter in="query" name="skus" type="String" required="true" %}
the commodity SKU code query, each time a maximum of 30, and one of the four options is required. for example: AMN00432_B_M,AMN00432_B_XL
{% endswagger-parameter %}

{% swagger-parameter in="query" name="categoryId" type="Number" required="true" %}
Category id, one of five is required, and pageNumber is required as a parameter. for example: 3654.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="dateStartTime" type="String" required="true" %}
The start time of the update time, UTC time, cannot be greater than the end time, the time is accurate to the year, month, and day, and the hour, minute, and second are not verified, and one of the four options is required. for example: 2022-01-07T04:04:39Z
{% endswagger-parameter %}

{% swagger-parameter in="query" name="sortType" type="String" %}
Sort type, which can be sorted by different fields according to the given parameters. When not specified, the default is reversed by the update time. for example: salasVolume
{% endswagger-parameter %}

{% swagger-parameter in="query" name="sortBy" type="String" %}
Sorting method, ascending order: 

**asc**

, reverse order: 

**desc.**

 for example: desc.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="dateEndTime" type="String" required="true" %}
The end time of the update time, UTC time, cannot be less than the start time, the time is accurate to the year, month, and day, and the hour, minute, and second are not checked. One of the four options is required. for example: 2022-01-08T04:04:39Z
{% endswagger-parameter %}

{% swagger-parameter in="query" name="pageNumber" type="Number" required="false" %}
Page number, when querying according to the update time, PageNumber is required and greater than 0.
{% endswagger-parameter %}

{% swagger-response status="200" description="Successfully query" %}
```javascript
{
    "code":10000,
    "data":{
        "list":[
            {
                "attributesJson":"{\"season\": \"Spring-Summer\", \"waistline\": \"Mid waist\"}",
                "kkProductId":1177295,
                "salesVolume":501,
                "spuStatus":1,
                "description":"Women'S Threaded Contrast Cropped Pantscomfortable Fabric/  Fashionable Style/  Casual And Versatile/  Suitable For Daily Wear/  School/  Leisure/  Vacation/  Date/  Party/  Club/  Etc/  Please Refer To The Left Size Picture Before Purchasing/  Due To Different Computer Display Colors/  The Actual Product Color May Be Slightly Different From The Picture Above",
                "updateTime":"2022-01-07T03:29:18Z",
                "productName":"Fashion All-Match Casual Women'S Threaded Contrast Cropped Pants",
                "createTime":"2022-01-07T03:29:18Z",
                "price":5.98,
                "fullCategoryName":"Women/Bottoms/Cropped Pants",
                "skuDetails":[
                    {
                        "mainImg":"https://img.kakaclo.com/image%2FAMN00769%2FAMN00769_DGR_S%2F87c26392683a1a34df19f3b2cfb053b6.jpg",
                        "cost":4.6,
                        "packageWeight":256,
                        "skuStatus":1,
                        "packageWidth":22,
                        "skuName":"Fashion All-Match Casual Women'S Threaded Contrast Cropped Pants",
                        "packageHeight":3,
                        "material":"100% Cotton",
                        "price":5.98,
                        "option3":"{\"name\":\"print\",\"value\":\"\"}",
                        "packageLength":32,
                        "option1":"{\"name\":\"color\",\"value\":\"Charcoal grey\"}",
                        "option2":"{\"name\":\"size\",\"value\":\"XL\"}",
                        "sku":"AMN00769_DGR_XL_AU",
                        "stock":20
                    }
                ],
                "sizeImagePath":"https://img.kakaclo.com/image%2FAMN00769%2FAMN00769_LGR_S%2Fd042f310fe9ac4115ba85a525ada61f4.jpg",
                "spu":"AMN00769",
                "stock":20,
                "categoryId":3658,
                "skuImgUrl":[
                    {
                        "imgUrl":[
                            "https://img.kakaclo.com/image%2FAMN00769%2FAMN00769_DGR_S%2F87c26392683a1a34df19f3b2cfb053b6.jpg"
                        ],
                        "skus":[
                            "AMN00769_DGR_XL_AU"
                        ]
                    }
                ]
            }
        ],
        "total":1,
        "pageNumber":1,
        "pageSize":1
    },
    "message":"Success！"
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Permission denied" %}

{% endswagger-response %}
{% endswagger %}
