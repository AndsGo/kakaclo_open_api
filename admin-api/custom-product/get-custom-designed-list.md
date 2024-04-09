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

<table><thead><tr><th>Properties</th><th width="92">Type</th><th width="83">Require</th><th width="165">Sample</th><th>Properties description</th></tr></thead><tbody><tr><td>modelCodes</td><td>[]string</td><td>N</td><td>["PODQRA028"]</td><td>Design model code array</td></tr><tr><td>spus</td><td>[]string</td><td>N</td><td>["QCUT00042"]</td><td>Spu array</td></tr><tr><td>searchContent</td><td>string</td><td>N</td><td>Short sleeve T-shirt</td><td>Product name or single spu, fuzzy query</td></tr><tr><td>lastUpdatedTime</td><td>int[64]</td><td>N</td><td>1694319208000</td><td>Design model last updated time</td></tr><tr><td>pageNumber</td><td>int</td><td>N</td><td>1</td><td>pageNumber starts from 1, default is 1</td></tr><tr><td>pageSize</td><td>int</td><td>N</td><td>20</td><td>"page Size" represents the return list pagination, the number of custom designed product per page. Each page can retrieve up to 100 custom order records.default is 20</td></tr></tbody></table>

**Body**

| Name             | Type     | Description                        |
| ---------------- | -------- | ---------------------------------- |
| `id`             | int\[64] | Primary key ID                     |
| customDesignedId | string   | POD customized designed product ID |
| categoryName     | string   | Skir                               |
| modelCode        | string   | Design model code                  |
| price            | double   | Designed product price(USD)        |
| enName           | string   | Design product english name        |
| imageUrl         | string   | Design product image url           |
| backImageUrl     | string   | Design product  back image url     |
| kkProductId      | int\[64] | Kaka product ID                    |
| modelId          | string   | Design model id                    |
| orderCount       | int      | Quantity of order                  |
| spu              | string   | Spu code                           |
| createDate       | int\[64] | Design product crated time         |
| modifyDate       | int\[64] | Design product update time         |

**Response**

```

  "code": 10000,
  "data": {
    "list": [
      {
        "backImageUrl": "https://oss-pubilc.kakaclo.com/images/common/custom/images/20240325/5baf5db0-4e6a-41e9-9c79-df2ec2bc758e.png",
        "customDesignedId": 234234645,
        "customModelId": 234355433,
        "enName": "en_name",
        "id": 1,
        "imageUrl": "https://oss-pubilc.kakaclo.com/images/common/custom/images/20240325/1f74a546-96ce-4940-86d2-b345f4897ad0.png",
        "kkCategoryId": 12331,
        "kkProductId": 2323423,
        "modelCode": "PODQRA028",
        "modelId": "123451234565",
        "orderCount": 0,
        "price": 8.35,
        "spu": "A302",
        "createDate":1712475208144,
        "modifyDate":1712475208144,
      }
    ],
    "total": 1
  },
  "message": "Success!"
}
```
