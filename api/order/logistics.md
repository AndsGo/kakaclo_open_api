# logistics

Get the current product order logistics failure and shipping cost

## Products Properties <a href="#response-parameter" id="response-parameter"></a>

| Parameter name | Type   | Remark                |
| -------------- | ------ | --------------------- |
| sku            | String | From the Products API |
| quantity       | number | number of sku         |

## &#x20;Properties <a href="#response-parameter" id="response-parameter"></a>

{% swagger method="post" path="/openapi/v1/order/LogisticsChannel" baseUrl="" summary="Get current logistics channels" %}
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
    // Response
}
```
{% endswagger-response %}
{% endswagger %}
