---
description: Create a custom order
---

# Create Custom Order

{% swagger method="post" path="/order" baseUrl="/openapi/v1/product/custom" summary="" %}
{% swagger-description %}

{% endswagger-description %}
{% endswagger %}

## Body  Properties <a href="#response-parameter" id="response-parameter"></a>



<table><thead><tr><th width="162">Properties</th><th width="117">Type</th><th width="94">Require</th><th width="143">Sample	</th><th>Properties description</th></tr></thead><tbody><tr><td>productName</td><td>string[200]</td><td>Y</td><td>Bule Skirt</td><td>Product name</td></tr><tr><td>mainImageUrl</td><td>string[200]</td><td>Y</td><td><a href="https://img.kakaclo.com/image%2FFSZW11087%2FFSZW11087_P_FREESIZE_NUB%2F0b39a40b85efb6ed554eaf7456b79ab2.jpg">https://img.kakaclo.com/image%2FFSZW11087%2FFSZW11087_P_FREESIZE_NUB%2F0b39a40b85efb6ed554eaf7456b79ab2.jpg</a></td><td>product image url</td></tr><tr><td>customOrderId</td><td>string[40]</td><td>N</td><td>KA10001</td><td>custom order id</td></tr><tr><td>channelType</td><td>string[20]</td><td>N</td><td>Standard</td><td>Logistics type, for example: standard,express, expedited</td></tr><tr><td><a href="create-custom-order.md#response-parameter-2">orderAddresses</a></td><td>object</td><td>Y</td><td></td><td>Order address information</td></tr><tr><td><a href="create-custom-order.md#response-parameter-3">orderItemsList</a></td><td>array object</td><td>Y</td><td></td><td>Order item array</td></tr></tbody></table>

## &#x20;<a href="#response-parameter" id="response-parameter"></a>

## orderAddresses  Properties <a href="#response-parameter" id="response-parameter"></a>

<table><thead><tr><th>Properties</th><th width="116">Type</th><th width="93">Require</th><th width="146">Sample	</th><th>Properties description</th></tr></thead><tbody><tr><td>country</td><td>string[50]</td><td>Y</td><td>US</td><td>Receiving country</td></tr><tr><td>city</td><td>string[100]</td><td>Y</td><td>Orlafasns</td><td>Receiving city</td></tr><tr><td>phone</td><td>int[32]</td><td>Y</td><td>07 82 24 67 93</td><td>Receiving phone number</td></tr><tr><td>recipient</td><td>string[100]</td><td>Y</td><td>Lffsollia Odfsdlena</td><td>recipient</td></tr><tr><td>street1</td><td>string[100]</td><td>Y</td><td>7 rue Rabelais</td><td>street1</td></tr><tr><td>street2</td><td>string[100]</td><td>N</td><td></td><td></td></tr><tr><td>province</td><td>string[50]</td><td>Y</td><td>de Lofasfasire</td><td>Receiving province</td></tr><tr><td>zip</td><td>string[50]</td><td>Y</td><td>vsvs00v30</td><td>post code</td></tr></tbody></table>



## Order Item  Properties <a href="#response-parameter" id="response-parameter"></a>

<table><thead><tr><th width="180">Properties</th><th width="112">Type</th><th width="89">Require</th><th width="156">Sample	</th><th>Properties description</th></tr></thead><tbody><tr><td>customSku</td><td>string[32]</td><td>N</td><td>FSZW11087_P_FREESIZE_NUB</td><td>Your product’s unique identifier: If the product SKU code of the platform system is not matched for the first time, you need to manually match it in the temporary order list in the platform backend; when it is passed in again, the system SKU code will be automatically identified.</td></tr><tr><td>quantity</td><td>int[16]</td><td>Y</td><td>100</td><td>Order stock</td></tr><tr><td>importImage</td><td>string[100] Array</td><td>Y</td><td>["<a href="https://img.kakaclo.com/image%2FFSZW11087%2FFSZW11087_P_FREESIZE_NUB%2Fda299fa3e37b65654bc5153c325b8b00.jpg">https://img.kakaclo.com/image%2FFSZW11087%2FFSZW11087_P_FREESIZE_NUB%2Fda299fa3e37b65654bc5153c325b8b00.jpg</a>"]</td><td>Pictures for reference use in customized designs</td></tr><tr><td>remark</td><td>string[100]</td><td>N</td><td>Wan the back removed and replace with a beautiful white Lace material/pattern</td><td>Order remark</td></tr><tr><td>color</td><td>string[50]</td><td>Y</td><td>Pink</td><td>Specific color</td></tr><tr><td>size</td><td>string[50]</td><td>Y</td><td>XL</td><td>Specific size</td></tr><tr><td>print</td><td>string[100]</td><td>N</td><td>Positioning printing</td><td>Printing content</td></tr><tr><td>material</td><td>string[100]</td><td>N</td><td>Acrylic</td><td>Specific material name</td></tr><tr><td>printUniQueCode</td><td>string[100]</td><td>N</td><td></td><td>Print content ('##' separated)</td></tr><tr><td>customerBarcode</td><td>string[100]</td><td>N</td><td>FSZW11087_P_FREESIZE_NUB</td><td>Unique code</td></tr><tr><td>uniqueCodeType</td><td>string[100]</td><td>N</td><td>3</td><td>Print unique code label display template 1-barcode 2-QR code 3-double code 4-plain text</td></tr></tbody></table>
