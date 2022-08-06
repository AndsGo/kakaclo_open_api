# Quick Start

{% hint style="warning" %}
**Good to know:** A quick start guide can be good to help folks get up and running with your API in a few steps. Some people prefer diving in with the basics rather than meticulously reading every page of documentation!
{% endhint %}

## Get your API **Access-Token**

Your API requests are authenticated using API **Access-Token**. Any request that doesn't include an API **Access-Token** will return an error.

Apps must authenticate using OAuth 2.0 to use kakaclo open API resources.you can get API **Access-Token** from your business manager.

## **API endpoint**

After you get your **Access-Token**, it's very easy to start making API call to Shoplazzaa.All endpoints are only accessible via HTTPS and are located at&#x20;

`https://api.kakaclo.com/openapi​`

## Make your first request

To make your first request, send an authenticated request to the products endpoint. This will query a product, which is nice.

{% swagger baseUrl="https:/api.kakaclo.com/openapi/v1" method="get" path="/product/category" summary="Query category" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200" description="Pet successfully created" %}
```javascript
{
    "name"="Wilson",
    "owner": {
        "id": "sha7891bikojbkreuy",
        "name": "Samuel Passet",
    "species": "Dog",}
    "breed": "Golden Retriever",
}
```
{% endswagger-response %}

{% swagger-response status="401" description="Permission denied" %}

{% endswagger-response %}
{% endswagger %}

Take a look at how you might call this method using our official libraries, or via `curl`:

{% tabs %}
{% tab title="curl" %}
```
curl --request GET \
     --url 'https://api.kakaclo.com/openapi/v1/produc/category' \
     --header 'Accept: application/json' \
     --header 'Authorization: Beare YOU-ACCESS-TOKOEN'
```
{% endtab %}
{% endtabs %}
