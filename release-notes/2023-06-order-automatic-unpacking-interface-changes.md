---
description: Order Automatic Split interface changes
---

# 2023-06  Order Automatic Split interface changes

2023-06 Update: Update the order related interface. This mainly includes interfaces for creating an order (automatic split), trial shipping (automatic split), and refund (automatic split partial refund).

## What’s changes in Order V1

The following features were changes in order V1 of kakaclo open APIs:

#### Creating orders  has been adjusted as follows:

* The request parameter removes the [channelCode ](../admin-api/order-1/order.md)and [warehouseCode](../admin-api/order-1/order.md) fields.
* The request parameter has added the [channelType](../admin-api/order-1/order.md) parameter, which is used as the basis for automatic split and shipping calculation.

## What’s changes in Order V2

The following features were changes in order V2 of kakaclo open APIs:

#### Creating orders  has been adjusted as follows:

* The request parameter removes the [channelCode ](../admin-api/order/order.md)and [warehouseCode](../admin-api/order/order.md) fields.
* The request parameter has added the [channelType](../admin-api/order/order.md) parameter, which is used as the basis for automatic split and shipping calculation.

#### Query Order  has been adjusted as follows:

* In the return parameter orderItems, the country shortcode field '[countryCode ](../admin-api/order-1/order-list/)after automatic split is added. It is used as the basis parameter for partial refund of the automatic split order.

#### Automatic Split Logistics Channel  has been adjusted as follows:

* Added an interface for automatic split and trial freight calculation, which is used to query the freight estimates for automatic split and delivery of different logistics timeliness levels.
