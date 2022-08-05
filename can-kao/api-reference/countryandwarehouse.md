# CountryAndWarehouse

## Query shipping country and warehouse

{% hint style="info" %}
#### Response parameter
{% endhint %}

| Parameter name   | Type   | Remark                          |
| ---------------- | ------ | ------------------------------- |
| warehouseCode    | String | Shipping warehouse code         |
| warehouseName    | String | Shipping warehouse name         |
| warehouseNameExt | String | Shipping warehouse Chinese name |
| countryCode      | String | Shipping country code           |
| countryCn        | String | Shipping country name           |

{% swagger method="get" path="/v1/product/countryAndWarehouse" baseUrl="" summary="" %}
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
