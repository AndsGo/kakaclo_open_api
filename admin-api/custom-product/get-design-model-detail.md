---
description: Get design model details
---

# Get Design Model Detail

statusEndpoint

<mark style="color:green;">`GET`</mark> /openapi/v1/product/custom/designModel/detail/{id}

**Headers**

For common header, refer to [How to call KakaClo Shop APIs - Common Headers](https://docs.kakaclo.com/kuai-su-kai-shi)

```
curl --request POST
     --url 'https://developer.kakaclo.com/openapi/v1/product/custom/designModel/detail/{id}'
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

| Name          | Type     | Description                                         |
| ------------- | -------- | --------------------------------------------------- |
| `id`          | int\[64] | Primary key ID                                      |
| categoryName  | string   | Design model category English name                  |
| enName        | string   | Design model English name                           |
| enDescription | string   | Design model English description                    |
| enSizeContent | string   | Design model size content                           |
| imageUrl      | string   | Design model front image                            |
| backImageUrl  | string   | Design model back image                             |
| modelCode     | string   | Design model code                                   |
| orderCount    | int\[32] | The sales volume of design model                    |
| price         | int\[32] | Design model regular price                          |
|               | int\[32] | Design model status: 1-on the shelf, 4-out of stock |
| weight        | int\[32] | Design model first variant weight                   |
| createDate    | string   | Design model crated time                            |
| modifyDate    | string   | Design model update time                            |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
    "code": 10000,
    "data": {
        "id": 73,
        "categoryName": "T-shirt",
        "enName": "Round neck raglan long sleeve T-shirt",
        "enDescription": "<p> description ~~</p>",
        "enSizeContent": "[{\"size\":[{\"name\":\"Sleeve Length\",\"size_value\":[{\"name\":\"2XS\",\"value\":71.0},{\"name\":\"XS\",\"value\":72.27},{\"name\":\"S\",\"value\":73.54},{\"name\":\"M\",\"value\":74.81},{\"name\":\"L\",\"value\":76.08},{\"name\":\"XL\",\"value\":77.35},{\"name\":\"2XL\",\"value\":78.62},{\"name\":\"3XL\",\"value\":79.89},{\"name\":\"4XL\",\"value\":81.16},{\"name\":\"5XL\",\"value\":82.43},{\"name\":\"6XL\",\"value\":83.7},{\"name\":\"7XL\",\"value\":84.97},{\"name\":\"8XL\",\"value\":86.24}]},{\"name\":\"1/2 cuff\",\"size_value\":[{\"name\":\"2XS\",\"value\":10.2},{\"name\":\"XS\",\"value\":10.6},{\"name\":\"S\",\"value\":11.0},{\"name\":\"M\",\"value\":11.4},{\"name\":\"L\",\"value\":11.8},{\"name\":\"XL\",\"value\":12.2},{\"name\":\"2XL\",\"value\":12.6},{\"name\":\"3XL\",\"value\":13.0},{\"name\":\"4XL\",\"value\":13.4},{\"name\":\"5XL\",\"value\":13.8},{\"name\":\"6XL\",\"value\":14.2},{\"name\":\"7XL\",\"value\":14.6},{\"name\":\"8XL\",\"value\":15.0}]},{\"name\":\"1/2 bust\",\"size_value\":[{\"name\":\"2XS\",\"value\":49.0},{\"name\":\"XS\",\"value\":51.0},{\"name\":\"S\",\"value\":53.0},{\"name\":\"M\",\"value\":55.0},{\"name\":\"L\",\"value\":57.0},{\"name\":\"XL\",\"value\":59.0},{\"name\":\"2XL\",\"value\":61.0},{\"name\":\"3XL\",\"value\":63.0},{\"name\":\"4XL\",\"value\":65.0},{\"name\":\"5XL\",\"value\":67.0},{\"name\":\"6XL\",\"value\":69.0},{\"name\":\"7XL\",\"value\":71.0},{\"name\":\"8XL\",\"value\":73.0}]},{\"name\":\"1/2 swing\",\"size_value\":[{\"name\":\"2XS\",\"value\":48.0},{\"name\":\"XS\",\"value\":50.0},{\"name\":\"S\",\"value\":52.0},{\"name\":\"M\",\"value\":54.0},{\"name\":\"L\",\"value\":56.0},{\"name\":\"XL\",\"value\":58.0},{\"name\":\"2XL\",\"value\":60.0},{\"name\":\"3XL\",\"value\":62.0},{\"name\":\"4XL\",\"value\":64.0},{\"name\":\"5XL\",\"value\":66.0},{\"name\":\"6XL\",\"value\":68.0},{\"name\":\"7XL\",\"value\":70.0},{\"name\":\"8XL\",\"value\":72.0}]},{\"name\":\"clothes length\",\"size_value\":[{\"name\":\"2XS\",\"value\":65.0},{\"name\":\"XS\",\"value\":66.0},{\"name\":\"S\",\"value\":67.0},{\"name\":\"M\",\"value\":68.0},{\"name\":\"L\",\"value\":69.0},{\"name\":\"XL\",\"value\":70.0},{\"name\":\"2XL\",\"value\":71.0},{\"name\":\"3XL\",\"value\":72.0},{\"name\":\"4XL\",\"value\":73.0},{\"name\":\"5XL\",\"value\":74.0},{\"name\":\"6XL\",\"value\":75.0},{\"name\":\"7XL\",\"value\":76.0},{\"name\":\"8XL\",\"value\":77.0}]}],\"sheet_name\":\"Size Chart\"}]",
        "imageUrl": "https://oss-pubilc.kakaclo.com/images/common/custom/images/20240323/5b14dda5-68e6-41bf-ae3a-b8caa2eaa267.png",
        "backImageUrl": "https://oss-pubilc.kakaclo.com/images/common/custom/images/20240329/5140a1a5-7f33-4ceb-99c7-6b86184d012e.png",
        "modelCode": "PODQRB518",
        "orderCount": 0,
        "price": 6.41,
        "status": 1,
        "variants": [
            {
                "size": "2XS",
                "weight": 200.01
            },
            {
                "size": "XS",
                "weight": 200.01
            },
            {
                "size": "S",
                "weight": 200.01
            },
            {
                "size": "M",
                "weight": 200.01
            },
            {
                "size": "L",
                "weight": 200.01
            },
            {
                "size": "XL",
                "weight": 200.01
            },
            {
                "size": "2XL",
                "weight": 200.01
            },
            {
                "size": "3XL",
                "weight": 200.01
            },
            {
                "size": "4XL",
                "weight": 200.01
            },
            {
                "size": "5XL",
                "weight": 200.01
            },
            {
                "size": "6XL",
                "weight": 200.01
            },
            {
                "size": "7XL",
                "weight": 200.01
            },
            {
                "size": "8XL",
                "weight": 200.01
            }
        ],
        "weight": 200.01,
        "createDate":1712651022603,
        "modifyDate":1712651022603:
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
