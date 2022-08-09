# Quick Start

{% hint style="info" %}
**Good to know:** A quick start guide can be good to help folks get up and running with your API in a few steps. Some people prefer diving in with the basics rather than meticulously reading every page of documentation!
{% endhint %}

## Get your API keys

Your API requests are authenticated using API **Access-Token**. Any request that doesn't include an API key will return an error.

Apps must authenticate using OAuth 2.0 to use kakaclo open API resources.you can get API **Access-Token** from your business manager.

## API Endpoint

After you get your **Access-Token**, it's very easy to start making API call to kakaclo open API.All endpoints are only accessible via HTTPS and are located at `https://developer.kakaclo.com/openapi`

{% hint style="info" %}
Access-Token needs to be put in the http request header，**Authorization: Bearer YOU\_ACCES-TOKEN**
{% endhint %}

## Make your first request

To make your first request, send an authenticated request to the products endpoint. This will query a product, which is nice.

{% swagger baseUrl="https://developer.kakaclo.com/openapi" method="get" path="/v1/product/category" summary="Query category" %}
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
     --url 'https://developer.kakaclo.com/openapi/v1/product/category' \
     --header 'Accept: application/json' \
     --header 'Authorization: Bearer YOU_ACCES-TOKEN' 
```
{% endtab %}
{% endtabs %}
