---
description: Get the list of sample clothing model that can be designed by the system.
---

# Get Design Model List

intEndpoint

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

<table><thead><tr><th>Properties</th><th width="92">Type</th><th width="89">Require</th><th>Sample</th><th>Properties description</th></tr></thead><tbody><tr><td>categoryNames</td><td>[]string</td><td>N</td><td>["Skirt"]</td><td>Category name comes from category name list</td></tr><tr><td>modelCodes</td><td>[]string</td><td>N</td><td>["PODQRA028"]</td><td>Design model code array</td></tr><tr><td>lastUpdatedTime</td><td>int[64]</td><td>N</td><td>1694319208000</td><td>Design model last updated time</td></tr><tr><td>pageNumber</td><td>int</td><td>N</td><td>1</td><td>pageNumber starts from 1, default is 1</td></tr><tr><td>pageSize</td><td>int</td><td>N</td><td>20</td><td>"page Size" represents the return list pagination, the number of custom model per page. Each page can retrieve up to 100 custom order records.default is 20</td></tr><tr><td>enName</td><td>string</td><td>N</td><td>"Short sleeve T-shirt"</td><td>Design model  english name,Support fuzzy query</td></tr></tbody></table>

**Body**

| Name         | Type     | Description                    |
| ------------ | -------- | ------------------------------ |
| `id`         | int\[64] | Primary key ID                 |
| categoryName | string   | Design model category name     |
| modelCode    | string   | Design model code              |
| price        | double   | Design model normal price(USD) |
| enName       | string   | Design model english name      |
| imageUrl     | string   | Design model image url         |
| backImageUrl | string   | Design model back image url    |
| createDate   | int\[64] | Design model crated time       |
| modifyDate   | int\[64] | Design model update time       |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
    "code": 10000,
    "data": {
        "list": [
            {
                "id": 73,
                "modelCode": "PODQRA028",
                "categoryName": "T-shirt",
                "price": 8.05,
                "enName": "Short sleeve T-shirt",
                "imageUrl": "https://oss-pubilc.kakaclo.com/images/common/custom/images/20240323/5b14dda5-68e6-41bf-ae3a-b8caa2eaa267.png",
                "backImageUrl": "https://oss-pubilc.kakaclo.com/images/common/custom/images/20240329/5140a1a5-7f33-4ceb-99c7-6b86184d012e.png",
                "createDate": 1712629505078,
                "modifyDate": 1712629505078
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
