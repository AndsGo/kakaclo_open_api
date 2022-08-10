---
description: Product category list
---

# Category

{% hint style="info" %}
This interface is to provide a list of all categories of products. The corresponding category can be found by **categoryId**.
{% endhint %}

## Response parameter

| Parameter name | Type   | Remark                                                                                            |
| -------------- | ------ | ------------------------------------------------------------------------------------------------- |
| categoryId     | Int    | Category unique identifier Id,for example: 3600                                                   |
| name           | String | tegory name,for example: Kids                                                                     |
| parentId       | Int    | The category id of the previous level, if it is the first level, the ParentId is 0,for example: 0 |
| level          | Int    | category level,for example: 1                                                                     |
| fullCategoryId | String | The full path where the current category is located,for example: 3600/3516                        |
| child          | Arrays | Next-level category information, the parameters are the same as above                             |

## Query category

{% swagger method="get" path="/openapi/v1/product/category" baseUrl="" summary="get product category" %}
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
