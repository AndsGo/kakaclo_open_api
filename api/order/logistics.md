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
}
</code></pre>

## Products Properties <a href="#response-parameter" id="response-parameter"></a>

| Parameter name | Type   | Remark                |
| -------------- | ------ | --------------------- |
| sku            | String | From the Products API |
| quantity       | number | number of sku         |

## &#x20;Properties <a href="#response-parameter" id="response-parameter"></a>

## Get current logistics channels

<mark style="color:green;">`POST`</mark> `https://test-developer.kakaclo.com/openapi/v1/order/logisticsChannel`

#### Request Body

| Name                                            | Type   | Description                                     |
| ----------------------------------------------- | ------ | ----------------------------------------------- |
| warehouseCode<mark style="color:red;">\*</mark> | String | Warehouse codes are used to match logistics     |
| province                                        | String | Province                                        |
| city                                            | String | City                                            |
| zipCode                                         | String | post code                                       |
| termini                                         | String | country of delivery                             |
| products                                        | array  | The sku information that needs to be calculated |

{% tabs %}
{% tab title="200: OK " %}
<pre class="language-javascript"><code class="lang-javascript"><strong>{
</strong>    "code":10000,
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
</code></pre>
{% endtab %}

{% tab title="401: Unauthorized Successfully query" %}
```javascript
{
    // Response
}
```
{% endtab %}
{% endtabs %}
