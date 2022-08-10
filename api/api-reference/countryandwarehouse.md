---
description: Country and warehouse relations
---

# CountryAndWarehouse



{% hint style="info" %}
This interface is to obtain the corresponding relationship between country and warehouse. Our [stock](stock.md) is placed in different countries and warehouses, you can obtain [stock](stock.md) through different countries and warehouses.
{% endhint %}

## Response parameter

| Parameter name   | Type   | Remark                                                          |
| ---------------- | ------ | --------------------------------------------------------------- |
| warehouseCode    | String | Shipping warehouse code,for example: G004                       |
| warehouseName    | String | Shipping warehouse name,for example: Warehouse 8 in South China |
| warehouseNameExt | String | Shipping warehouse Chinese name,for example: 东莞-独立站             |
| countryCode      | String | Shipping country code,for example: CN\_S                        |
| countryCn        | String | Shipping country name,for example: South China                  |

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
