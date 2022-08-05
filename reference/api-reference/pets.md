# Product

## Query Products

{% swagger baseUrl="" method="get" path="/v1/product/products" summary="" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="spus" required="false" type="Arrays" %}
Commodity SPU code collections, specify the commodity SPU code query, each time a maximum of 30, and one of the four options is required.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="skus" required="false" type="Arrays" %}
Commodity SKU code collections, specify the commodity SKU code query, each time a maximum of 30, and one of the four options is required.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="dateStartTime" required="false" type="Date" %}
The start time of the update time, UTC time, cannot be greater than the end time, the time is accurate to the year, month, and day, and the hour, minute, and second are not verified, and one of the four options is required.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="dateEndTime" required="false" type="Date" %}
The end time of the update time, UTC time, cannot be less than the start time, the time is accurate to the year, month, and day, and the hour, minute, and second are not checked. One of the four options is required.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="pageNumber" type="Int" %}
Page number, when querying according to the update time, PageNumber is required and greater than 0.
{% endswagger-parameter %}

{% swagger-response status="200" description="successfully query" %}
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
                "fullCategoryId":"",
                "fullCategoryName":"",
                "createTime":"",
                "updateTime":"",
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
                        "skuStatus":"",
                        "imgUrl":[

                        ]
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

{% hint style="info" %}
**Good to know:** This API method was created using the API Method block, it's how you can build out an API method documentation from scratch. Have a play with the block and you'll see you can do some nifty things like add and reorder parameters, document responses, and give your methods detailed descriptions.
{% endhint %}

## Query stock

{% swagger method="get" path="/v1/product/stocks" baseUrl="" summary="" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="skus" type="Arrays" required="false" %}
Commodity SKU code collections, specify the commodity SKU code query, each time a maximum of 30, Three options are required.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="warehouseCode" type="String" %}
warehouse code
{% endswagger-parameter %}

{% swagger-parameter in="body" name="countryCode" type="String" %}
Shipping country
{% endswagger-parameter %}

{% swagger-parameter in="body" name="dateStartTime" type="Date" %}
Inventory update start time, one of the three is required.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="dateEndTime" type="Date" %}
Inventory update end time, one of the three is required.
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="successfully query" %}
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

{% hint style="info" %}
**Good to know:** This API method was auto-generated from an example Swagger file. You'll see that it's not editable – that's because the contents are synced to an URL! Any time the linked file changes, the documentation will change too.


{% endhint %}

## Query category

{% swagger method="get" path="/v1/product/category" baseUrl="" summary="" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="successfully query" %}
```javascript
{
    "code":10000,
    "message":"kk.api.200",
    "data":{
        "list":[
            {
                "categoryId":"",
                "parentId":"",
                "level":"",
                "fullCategoryId":"",
                "imgUrl":"",
                "name":"",
                "child":[
                    {

                    }
                ]
            }
        ]
    }
}
```
{% endswagger-response %}
{% endswagger %}

| Parameter name | Type   | Remark                                                                             |
| -------------- | ------ | ---------------------------------------------------------------------------------- |
| categoryId     | Long   | Category unique identifier Id                                                      |
| parentId       | Long   | The category id of the previous level, if it is the first level, the ParentId is 0 |
| level          | Int    | category level                                                                     |
| fullCategoryId | String | The full path where the current category is located                                |
| imgUrl         | String | Category pictures                                                                  |
| name           | String | Category name                                                                      |
| child          | Arrays | Next-level category information, the parameters are the same as above              |

## Query shipping country and warehouse

{% swagger method="get" path="/v1/product/countryAndWarehouse" baseUrl="" summary="" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="successfully query" %}
```javascript
{
    "code":10000,
    "message":"kk.api.200",
    "data":{
        "list":[
            {
                "warehouseCode":"",
                "warehouseName":"",
                "warehouseNameExt":"",
                "countryCode":"",
                "countryCn":""
            }
        ]
    }
}
```
{% endswagger-response %}
{% endswagger %}

| Parameter name   | Type   | Remark                          |
| ---------------- | ------ | ------------------------------- |
| warehouseCode    | String | Shipping warehouse code         |
| warehouseName    | String | Shipping warehouse name         |
| warehouseNameExt | String | Shipping warehouse Chinese name |
| countryCode      | String | Shipping country code           |
| countryCn        | String | Shipping country name           |
