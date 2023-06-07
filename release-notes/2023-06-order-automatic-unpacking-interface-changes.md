---
description: Order Automatic Unpacking interface changes
---

# 2023-06  Order Automatic Unpacking interface changes

2023-06 Update: Update the order related interface. This mainly includes interfaces for creating an order (automatic unpacking), trial shipping (automatic unpacking), and refund (automatic unpacking partial refund).

## What’s changes in Order V1

The following features were changes in order V1 of kakaclo open APIs:

#### Creating orders  has been adjusted as follows:

* The request parameter removes the [channelCode ](../admin-api/order-1/order.md)and [warehouseCode](../admin-api/order-1/order.md) fields.
* The request parameter has added the [channelType](../admin-api/order-1/order.md) parameter, which is used as the basis for automatic unpacking and shipping calculation.

## What’s changes in Order V2

The following features were changes in order V2 of kakaclo open APIs:

#### Creating orders  has been adjusted as follows:

* The request parameter removes the [channelCode ](../admin-api/order/order.md)and [warehouseCode](../admin-api/order/order.md) fields.
* The request parameter has added the [channelType](../admin-api/order/order.md) parameter, which is used as the basis for automatic unpacking and shipping calculation.

#### Query Order  has been adjusted as follows:

* In the return parameter orderItems, the country shortcode field '[countryCode ](../admin-api/order-1/order-list/)after automatic unpacking is added. It is used as the basis parameter for partial refund of the automatic unpacking order.

#### Automatic Unpack Logistics Channel  has been adjusted as follows:

* Added an interface for automatic unpacking and trial freight calculation, which is used to query the estimated freight for automatic unpacking and delivery.
