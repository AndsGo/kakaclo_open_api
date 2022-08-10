---
description: View order related information
---

# Order List

##

{% swagger method="get" path="/openapi/v1/order/order" baseUrl="" summary="" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="query" name="status" %}
order status, please use comma as separator, for example  waiting_payment,cancel
{% endswagger-parameter %}

{% swagger-parameter in="query" name="createdAtMin" %}
filter orders created at or before date, for example: 

`2016-01-18T23:41:00Z`
{% endswagger-parameter %}

{% swagger-parameter in="query" name="createdAtMax" %}
filter orders created at or before date, for example: 

`2016-01-18T23:41:00Z`
{% endswagger-parameter %}

{% swagger-parameter in="query" name="updatedAtMin" %}
filter orders last updated at or after date, for example: 

`"2016-01-18T23:41:00Z"`
{% endswagger-parameter %}

{% swagger-parameter in="query" name="updatedAtMax" %}
filter orders last updated at or before date, for example: 

`2016-01-18T23:41:00Z`
{% endswagger-parameter %}

{% swagger-parameter in="query" name="ids" %}
Order's IDs, please use comma as separator, for example 1000000065617,1000000065618
{% endswagger-parameter %}
{% endswagger %}
