---
description: Order V2 Version Update Instructions
---

# 2022-12 Order V2 Version

2022-12 Updated Order-related interfaces, mainly including [Query Order](../admin-api/order-1/order-list/) and [Refund Order](../admin-api/order-1/refund-order.md) endpoints.

## What’s changes in Order V2

The following features were changes in Order V2 of kakaclo open APIs:

#### Query Order has been adjusted as follows:

* The [Order List Properties](../admin-api/order-1/order-list/#response-parameter) status field is split into 4 fields: status, financialStatus, fulfillmentStatus, and refundStatus.
* The field name of [Order List Properties](../admin-api/order-1/order-list/#response-parameter) has been adjusted \
  payAt -> payDate\
  completedAt -> completedDate|\
  skusAmount -> subTotalAmount
* [Order List Properties](../admin-api/order-1/order-list/#response-parameter) added couponAmount, promotionAmount, refundableAmount, refundedAmount fields.
* [Order Items Properties](../admin-api/order-1/order-list/#response-parameter-2) added itemId and refundStatus fields.
* [Fulfillments Properties ](../admin-api/order-1/order-list/#response-parameter-1)added packId and status fields.

