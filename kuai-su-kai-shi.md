# Quick Start

{% hint style="info" %}
**Good to know:** A quick start guide can be good to help folks get up and running with your API in a few steps. Some people prefer diving in with the basics rather than meticulously reading every page of documentation!
{% endhint %}

## Get your API keys

Your API requests are authenticated using API keys. Any request that doesn't include an API key will return an error.

Apps must authenticate using OAuth 2.0 to use  kakaclo open API resources.you can get API keys from your business manager

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

{% hint style="info" %}
**Good to know:** You can use the API Method block to fully document an API method. You can also sync your API blocks with an OpenAPI file or URL to auto-populate them.
{% endhint %}

Take a look at how you might call this method using our official libraries, or via `curl`:

{% tabs %}
{% tab title="curl" %}
```
curl --request GET \
     --url 'https://api.kakaclo.com/openapi/v1/category' \
     --header 'Accept: application/json' \
     --header 'Authorization: Bearer YOU_TOKEN' 
```
{% endtab %}
{% endtabs %}
