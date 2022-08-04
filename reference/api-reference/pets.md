# Product

## Query Products

{% swagger baseUrl="" method="post" path="/v1/product/QueryProduct" summary="" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="Spus" required="false" type="Arrays" %}
Commodity SPU code collections, specify the commodity SPU code query, each time a maximum of 30, and one of the four options is required.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="Skus" required="false" type="Arrays" %}
Commodity SKU code collections, specify the commodity SKU code query, each time a maximum of 30, and one of the four options is required.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="DateStartTime" required="false" type="Date" %}
The start time of the update time, UTC time, cannot be greater than the end time, the time is accurate to the year, month, and day, and the hour, minute, and second are not verified, and one of the four options is required.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="DateEndTime" required="false" type="Date" %}
The end time of the update time, UTC time, cannot be less than the start time, the time is accurate to the year, month, and day, and the hour, minute, and second are not checked. One of the four options is required.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="PageNumber" type="Int" %}
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
                "KkProductId":"",
                "Spu":"",
                "ProductName":"",
                "Description":"",
                "SizeImagePath":"",
                "SpuStatus":"",
                "FullCategoryId":"",
                "FullCategoryName":"",
                "CreateTime":"",
                "UpdateTime":"",
                "SkuList":[
                    {
                        "Sku":"",
                        "SkuName":"",
                        "MainImg":"",
                        "PackageLength":"",
                        "PackageWidth":"",
                        "PackageHeight":"",
                        "PackageWeight":"",
                        "Cost":"",
                        "Price":"",
                        "Option1":"",
                        "Option2":"",
                        "Option3":"",
                        "Material":"",
                        "SkuStatus":"",
                        "ImgUrl":[

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

{% swagger method="post" path="/v1/product/QueryStock" baseUrl="" summary="" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="Skus" type="Arrays" required="true" %}
Commodity SKU code collections, specify the commodity SKU code query, each time a maximum of 30.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="WarehouseCode" type="String" %}
warehouse code
{% endswagger-parameter %}

{% swagger-parameter in="body" name="Country" type="String" %}
Shipping country
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="successfully query" %}
```javascript
{
    "code":10000,
    "message":"kk.api.200",
    "data":{
        "list":[
            {
                "Sku":"",
                "WarehouseInventoryList":[
                    {
                        "WarehouseCode":"",
                        "Inventory":"",
                        "Country":""
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
