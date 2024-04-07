---
description: Get the list of products designed in the designer
---

# Get Custom Designed List

Endpoint

<mark style="color:green;">`POST`</mark> /openapi/v1/product/custom/customDesigned/search

**Headers**

For common header, refer to [How to call KakaClo Shop APIs - Common Headers](https://docs.kakaclo.com/kuai-su-kai-shi)

```
curl --request POST
     --url 'https://developer.kakaclo.com/openapi/v1/product/custom/customDesigned/search'
     --header 'Content-Type: application/json'
     --header 'Authorization: Bearer YOU_ACCES-TOKEN'
```

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

#### Request Body Properties <a href="#response-parameter-1" id="response-parameter-1"></a>

<table><thead><tr><th>Properties</th><th width="92">Type</th><th width="83">Require</th><th width="165">Sample</th><th>Properties description</th></tr></thead><tbody><tr><td>categoryNames</td><td>[]string</td><td>N</td><td>["Skirt"]</td><td>Category name comes from category name list</td></tr><tr><td>modelCode</td><td>string</td><td>N</td><td>"PODQRA028"</td><td>Design model code</td></tr><tr><td>spus</td><td>[]string</td><td>N</td><td>["QCUT00042"]</td><td>Spu array</td></tr><tr><td>searchContent</td><td>string</td><td>N</td><td>Short sleeve T-shirt</td><td>Product name or single spu, fuzzy query</td></tr><tr><td>lastUpdatedTime</td><td>int[64]</td><td>N</td><td>1694319208000</td><td>Design model last updated time</td></tr></tbody></table>

**Body**

| Name         | Type     | Description                    |
| ------------ | -------- | ------------------------------ |
| `id`         | int\[64] | Primary key ID                 |
| modelId      | string   | Design model id                |
| categoryName | string   | Skirt                          |
| modelCode    | string   | Design model code              |
| normalPrice  | double   | Design model normal price(USD) |
| enName       | string   | Design model english name      |
| imageUrl     | string   | Design model image url         |
| backImageUrl | string   | Design model back image url    |
| createDate   | string   | Design model crated time       |
| modifyDate   | string   | Design model update time       |

**Response**

```
{
    "code": 10000,
    "data": {
        "list": [
            {
                "id": "1889",
                "model_id": "2073164990626574110001",
                "globalId": "2073164990626574110001",
                "code": "PODQRA028",
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
