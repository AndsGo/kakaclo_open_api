# CountryAndWarehouse

## Response Properties <a href="#response-parameter" id="response-parameter"></a>

| Parameter name  | Type   | Remark                          |
| --------------- | ------ | ------------------------------- |
| warehouseCode   | String | Shipping warehouse code         |
| warehouseName   | String | Shipping warehouse name         |
| arehouseNameExt | String | Shipping warehouse Chinese name |
| countryCode     | String | Shipping country code           |
| countryCn       | String | Shipping country name           |

## Query shipping country and warehouse

{% swagger method="get" path="/openapi/v1/product/countryAndWarehouse" baseUrl="" summary="get country and warehouse" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successfully query" %}
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

{% swagger-response status="400: Bad Request" description="" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}
