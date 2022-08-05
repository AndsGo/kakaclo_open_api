# Stock

## Query stock

{% swagger method="get" path="/v1/product/stocks" baseUrl="" summary="" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="query" name="skus" type="Arrays" %}
Commodity SKU code collections, specify the commodity SKU code query, each time a maximum of 30, Three options are required.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="warehouseCode" type="String" %}
arehouse code
{% endswagger-parameter %}

{% swagger-parameter in="query" name="countryCode" type="String" %}
hipping country
{% endswagger-parameter %}

{% swagger-parameter in="query" name="dateStartTime" type="Date" %}
Inventory update start time, one of the three is required.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="dateEndTime" type="Date" %}
Inventory update end time, one of the three is required.
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

| Parameter name | Type   | Remark                |
| -------------- | ------ | --------------------- |
| sku            | String | product unique code   |
| qty            | Int    | Inventory quantity    |
| countryCode    | String | Shipping country code |
| warehouseCode  | String | warehouse code        |