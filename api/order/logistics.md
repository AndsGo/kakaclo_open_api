# logistics

Calculate the logistics channels supported by the sku that currently needs to place an order, and use the specified logistics channel to generate an order

## Response Properties <a href="#response-parameter" id="response-parameter"></a>

| Parameter name   | Type       | Remark          |
| ---------------- | ---------- | --------------- |
| deliveryTime     | String     | delivery time   |
| estimatedFreight | BigDecimal | Shipping amount |
| companyName      | String     | carrier name    |

## Request Properties <a href="#response-parameter" id="response-parameter"></a>

<pre><code>{
      "warehouseCode": "",
      "province": "",
      "city": "",
<strong>      "zipCode": "",
</strong>      "termini": "",
      "products": [
        {
          "skuCode": "",
          "quantity": 1
        }
      ]
}</code></pre>

## Products Properties <a href="#response-parameter" id="response-parameter"></a>

| Parameter name | Type   | Remark                |
| -------------- | ------ | --------------------- |
| sku            | String | From the Products API |
| quantity       | number | number of sku         |

## &#x20;Properties <a href="#response-parameter" id="response-parameter"></a>

{% swagger method="post" path="/openapi/v1/order/logisticsChannel" baseUrl="" summary="Get current logistics channels" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="warehouseCode" required="true" %}
Warehouse codes are used to match logistics
{% endswagger-parameter %}

{% swagger-parameter in="body" name="province" %}
Province
{% endswagger-parameter %}

{% swagger-parameter in="body" name="city" %}
City
{% endswagger-parameter %}

{% swagger-parameter in="body" name="zipCode" %}
post code
{% endswagger-parameter %}

{% swagger-parameter in="body" name="termini" %}
country of delivery
{% endswagger-parameter %}

{% swagger-parameter in="body" name="products" type="array" %}
The sku information that needs to be calculated
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "code":10000,
    "message":"kk.api.200",
    "data":{
        "list":[
            {
                "deliveryTime":"",
                "estimatedFreight":"",
                "companyName":""
            }
        ]
    }
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Successfully query" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}
