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
| categoryId     | Number | Category unique identifier Id,for example: 3600                                                   |
| name           | String | tegory name,for example: Kids                                                                     |
| parentId       | Number | The category id of the previous level, if it is the first level, the ParentId is 0,for example: 0 |
| level          | Number | category level,for example: 1                                                                     |
| fullCategoryId | String | The full path where the current category is located,for example: 3600/3516                        |
| child          | Arrays | Next-level category information, the parameters are the same as above                             |

## Query category

## get product category

<mark style="color:blue;">`GET`</mark> `/openapi/v1/product/category`

{% tabs %}
{% tab title="200: OK Successfully query" %}
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
{% endtab %}
{% endtabs %}
