---
description: Get the list of sample clothing model category
---

# Get Design Category List

Endpoint

<mark style="color:green;">`POST`</mark> `/`openapi/v1/product/custom/designCategory/search

\<Description of the endpoint>

**Headers**

For common header, refer to [How to call KakaClo Shop APIs - Common Headers](https://docs.kakaclo.com/kuai-su-kai-shi)

```
curl --request POST
     --url 'https://developer.kakaclo.com/openapi/v1/product/custom/designModel/search'
     --header 'Content-Type: application/json'
     --header 'Authorization: Bearer YOU_ACCES-TOKEN'
```

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

**Response Body**

| Name       | Type     | Description                |
| ---------- | -------- | -------------------------- |
| categoryId | int\[64] | Category ID                |
| parentId   | int\[32] | Category's Parent ID       |
| enName     | string   | Category's English Name    |
| enContent  | string   | Category's English Content |

{% tabs %}
{% tab title="200" %}
```json
{
    "code": 10000,
    "data": {
        "list": [
            {
                "categoryId": 5,
                "enContent": "Women's bags, men's bags, children's bags",
                "enName": "bag",
                "parentId": 0
            },
            {
                "categoryId": 1,
                "enContent": "Men's clothing, women's clothing, children's clothing",
                "enName": "clothing",
                "parentId": 0
            },
            {
                "categoryId": 24,
                "enContent": "Handbags, lunch bags, shoulder bags, canvas bags",
                "enName": "handbag",
                "parentId": 5
            }
            ....
        ],
        "total": 38
    },
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
