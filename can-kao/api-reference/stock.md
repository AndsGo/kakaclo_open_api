# Stock

## Stock Properties

| Parameter name | Type   | Remark                |
| -------------- | ------ | --------------------- |
| sku            | String | product unique code   |
| qty            | Int    | Inventory quantity    |
| countryCode    | String | Shipping country code |
| warehouseCode  | String | warehouse code        |
| total          | Int    | total data volume     |
| pageNumber     | Int    | page number           |
| pageSize       | Int    | Quantity per page     |

## Query stock

{% swagger method="get" path="/openapi/v1/product/stocks" baseUrl="" summary="get product stock" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="query" name="skus" type="Arrays" required="true" %}
Commodity SKU code collections, specify the commodity SKU code query, each time a maximum of 30, Three options are required.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="warehouseCode" type="String" required="false" %}
warehouse code
{% endswagger-parameter %}

{% swagger-parameter in="query" name="dateStartTime" type="String" required="true" %}
Inventory update start time, one of the three is required.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="dateEndTime" type="String" required="true" %}
Inventory update end time, one of the three is required.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="pageNumber" type="Int" required="false" %}
Page number, when querying according to the update time, PageNumber is required and greater than 0.
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
