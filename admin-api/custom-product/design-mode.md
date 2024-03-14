---
description: Get Design Mode list
---

# Design Mode

## Get Design Mode

<mark style="color:green;">`POST`</mark> /openapi/v1/product/custom/designMode/search

\<Description of the endpoint>

**Headers**

For common header, refer to [How to call KakaClo Shop APIs - Common Headers](https://docs.kakaclo.com/kuai-su-kai-shi)

```
curl --request POST
     --url 'https://developer.kakaclo.com/openapi/v1/product/custom/designMode/search'
     --header 'Content-Type: application/json'
     --header 'Authorization: Bearer YOU_ACCES-TOKEN'
```

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

**Body**

| Name   | Type   | Description      |
| ------ | ------ | ---------------- |
| `name` | string | Name of the user |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
  "id": 1,
  "name": "John",
  "age": 30
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
