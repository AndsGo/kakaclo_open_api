---
description: Get the list of sample clothing model that can be designed by the system.
---

# Get Design Model List

Endpoint

<mark style="color:green;">`POST`</mark> /openapi/v1/product/custom/designModel/search

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

### Request Body Properties <a href="#response-parameter-1" id="response-parameter-1"></a>

| Properties      | Type    | Require | Sample                    | Properties description               |
| --------------- | ------- | ------- | ------------------------- | ------------------------------------ |
| categoryIds     | \[]long | N       | \[10,1483258449929080833] | Category ID comes from category list |
| designModelCode | string  | N       | "D425"                    | Design model code                    |
| lastUpdatedTime | long    | N       | 1694319208000             | Design model last updated time       |

**Body**

| Name        | Type   | Description                    |
| ----------- | ------ | ------------------------------ |
| `id`        | long   | Primary key ID                 |
| modelId     | string | Design model id                |
| globalId    | string | Global ID                      |
| code        | string | Design model code              |
| normalPrice | number | Design model normal price(USD) |
| name        | string | Design model name              |
| type        | string | Design model type              |
| createdTime | string | Design model crated time       |
| updateTime  | string | Design model update time       |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
    "code": 10000,
    "data": {
        "list": [
            {
                "id": "1889",
                "model_id": "2073164990626574110001",
                "globalId": "2073164990626574110001",
                "code": "B577",
                "normalPrice": 8.05,
                "name": "Short sleeve T-shirt",
                "imageUrl": "https://oss-pubilc.kakaclo.com/images/common/custom/images/20240315/23448f22-7af0-4dd4-b768-5f7444e52495.png",
                "type": "3D",
                "createdTime": "2024-03-13 11:58:58",
                "updatedTime": null
            }
        ],
        "total": 1
    },
    "message": "success"
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
