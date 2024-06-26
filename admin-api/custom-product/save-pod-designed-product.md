---
description: >-
  Requesting this interface is equivalent to accessing the interface for saving
  designed products on the Kakaclo designer. A new product data item will be
  added to the list of designed products.
---

# Save POD Designed Product

## Create a new POD designed product

<mark style="color:green;">`POST`</mark> `/`openapi/v1/product/custom/customDesigned/addProduct

**Headers**

For common header, refer to [How to call KakaClo Shop APIs - Common Headers](https://docs.kakaclo.com/kuai-su-kai-shi)

```
curl --request POST
     --url 'https://developer.kakaclo.com/openapi/v1/product/custom/customDesigned/addProduct'
     --header 'Content-Type: application/json'
     --header 'Authorization: Bearer YOU_ACCES-TOKEN'
```

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |



**Request Body Properties**

| Name           | Type   | Description                                                                                           |
| -------------- | ------ | ----------------------------------------------------------------------------------------------------- |
| modelId        | string | modelId value source: id field returned by Get Design Model List or Get Design Model Detail interface |
| enName         | string | Name of the designed product                                                                          |
| imageUrl       | string | Designed clothing front picture                                                                       |
| backImageUrl   | string | Designed clothing back picture                                                                        |
| materialImages | array  | All the material pictures used in the clothing design pictures                                        |
| colorValue     | string | Select the specific color value of the color                                                          |



**Request body**

{% tabs %}
{% tab title="body example" %}
```json
{
  "modelId": "1",
  "enName": "Dinosaur Round Neck Short Sleeve T-Shirt-Children's Clothing",
  "imageUrl": "https://oss-pubilc.kakaclo.com/images/common/custom/images/20240325/1f74a546-96ce-4940-86d2-b345f4897ad0.png",
  "backImageUrl": "https://oss-pubilc.kakaclo.com/images/common/custom/images/20240325/5baf5db0-4e6a-41e9-9c79-df2ec2bc758e.png",
  "materialImages": [
    {
      "imageName": "aaa",
      "imageUrl": "https://oss-pubilc.kakaclo.com/images/common/custom/images/20240325/5baf5db0-4e6a-41e9-9c79-df2ec2bc758e.png"
    }
  ],
  "colorValue": "#A72525"
}
```
{% endtab %}
{% endtabs %}

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
  "data": "",
  "code": 10000,
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
