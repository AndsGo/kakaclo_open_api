---
description: Get all category names of POD customized clothing styles
---

# Get Design Category Name List

Endpoint

<mark style="color:green;">`GET`</mark> `/`openapi/v1/product/custom/modelCategoryName/search

**Headers**

For common header, refer to [How to call KakaClo Shop APIs - Common Headers](https://docs.kakaclo.com/kuai-su-kai-shi)

```
curl --request POST
     --url 'https://developer.kakaclo.com/openapi/v1/product/custom/modelCategoryName/search'
     --header 'Content-Type: application/json'
     --header 'Authorization: Bearer YOU_ACCES-TOKEN'
```

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

**Response Body**

| Name   | Type   | Require | Sample | Description                                                                                                                  |
| ------ | ------ | ------- | ------ | ---------------------------------------------------------------------------------------------------------------------------- |
| status | string | true    | 1,4    | Design model status: 0-off the shelf; 1-on the shelf; 4-out of stock, Use English "," to separate multiple items with commas |

{% tabs %}
{% tab title="200" %}
```json
{
  "code": 10000,
  "data": [
    "Fishing Clothes",
    "Hoodie",
    "Jacket",
    "Kimono",
    "Pants",
    "Pet Suit",
    "Polo Shirt",
    "Retro",
    "Shirt",
    "Skirt",
    "Sports",
    "Suit",
    "Swimsuit",
    "T-shirt",
    "Underwear",
    "Vest"
  ],
  "message": "Success!"
}
```
{% endtab %}

{% tab title="400" %}
```json
{
  "error": "Invalid request"
}
```
{% endtab %}
{% endtabs %}
