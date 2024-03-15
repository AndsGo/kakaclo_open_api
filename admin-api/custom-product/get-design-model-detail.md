---
description: Get design model details
---

# Get Design Model Detail

dEndpoint

<mark style="color:green;">`GET`</mark> /openapi/v1/product/custom/designModel/detail/{id}

**Headers**

For common header, refer to [How to call KakaClo Shop APIs - Common Headers](https://docs.kakaclo.com/kuai-su-kai-shi)

Copy

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



Request Parameter

| Name | Type     | Description    |
| ---- | -------- | -------------- |
| id   | int\[64] | Primary key ID |

**Response Body Parameter**

| Name           | Type      | Description                      |
| -------------- | --------- | -------------------------------- |
| `id`           | int\[64]  | Primary key ID                   |
| modelId        | string    | Design model id                  |
| globalId       | string    | Global ID                        |
| code           | string    | Design model code                |
| spu            | string    | spu code                         |
| status         | int\[32]  | Design model status(1-active)    |
| name           | string    | Design model name                |
| normalPrice    | number    | Design model normal price(USD)   |
| salesVolume    | int\[32]  | The sales volume of design model |
| imageUrl       | string    | Image url of design model        |
| imageUrls      | \[]string | Image url list of design model   |
| type           | string    | Design model type                |
| technique      | string    | Technique of design model        |
| productionTime | string    | Production time of design model  |
| description    | string    | Description of design model      |
| sizeContent    | string    | Size content of design model     |
| createDate     | string    | Design model crated time         |
| modifyDate     | string    | Design model update time         |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
    "code": 10000,
    "data": {
        "id": 1889,
        "modelId": "2073164990626574110001",
        "globalId": "2073164990626574110001",
        "code":"B577",
        "spu": "PODQRB577",
        "status": 1,
        "name": "Print on Demand Woman'S Spring And Summer New Sexy Tube Top Mesh Pearl Hip Dress",
        "normalPrice": 8.05,
        "salesVolume": 50,
        "imageUrl": "https://oss-pubilc.kakaclo.com/images/common/custom/images/20240315/23448f22-7af0-4dd4-b768-5f7444e52495.png",
        "imageUrls": [
            "https://oss-pubilc.kakaclo.com/images/common/custom/images/20240315/23448f22-7af0-4dd4-b768-5f7444e52495.png"
        ],
        "type": "3D",
        "technique": "Thermal transfer",
        "productionTime": "5-7 business days",
        "description": "Product description ~~",
        "sizeContent": "[{\"size\":[{\"name\":\"Sleeve Length\",\"size_value\":[{\"name\":\"M\",\"value\":19},{\"name\":\"L\",\"value\":19.5}]},{\"name\":\"1/2 cuff\",\"size_value\":[{\"name\":\"M\",\"value\":16.9},{\"name\":\"L\",\"value\":17.6}]},{\"name\":\"shoulder width\",\"size_value\":[{\"name\":\"M\",\"value\":41},{\"name\":\"L\",\"value\":43}]},{\"name\":\"1/2 bust\",\"size_value\":[{\"name\":\"M\",\"value\":48.5},{\"name\":\"L\",\"value\":51.5}]},{\"name\":\"clothes length\",\"size_value\":[{\"name\":\"M\",\"value\":64},{\"name\":\"L\",\"value\":66}]}],\"sheet_name\":\"Size Chart\"}]",
        "createDate":"2024-03-13 11:58:58",
        "modifyDate":"2024-03-13 14:58:59",
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
