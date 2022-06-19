SortOrder: 2
# Order Object Conversion

To help with migration to the eCommerce Orders API, refer to the table below for field changes between the old [Stores order object](https://dev.wix.com/api/rest/wix-stores/orders/order-object) and the new [eCommerce order object](https://bo.wix.com/wix-docs/rest/ecommerce/orders/order-object).


Note that some fields are accessible via other eCommerce APIs. In these cases, the field in the 2nd column refers to its
location in the other API, which is specified in the 3rd column.

The address object used in the new eCommerce APIs is slightly different to the one used in the Stores APIs. For more details, refer to the [address object conversion table](https://bo.wix.com/wix-docs/rest/ecommerce/orders/address-object-conversion).

Fields marked with an asterisk (*) signify little to no change in semantics or access.

For details on webhooks, refer to the [Webhook Conversion Table](#Webhooks-Conversion-Table) below.

## Order Object Conversion Table
| Stores Order Object                                         | eCommerce Order Object                                                    | Notes                                             |
| ------------------------------------------------------------|---------------------------------------------------------------------------|---------------------------------------------------|
| `id`*                                                       | `id`                                                                      |
| `number`*                                                   | `number`                                                                  |
| `dateCreated`                                               | `createdDate`                                                             |
| `buyerInfo.id`                                              | `buyerInfo.contactId` & `buyerInfo.memberId`                              |
| `buyerInfo.id` && `buyerInfo.identityType: "MEMBER"`        | `buyerInfo.memberId`                                                      |
| `buyerInfo.id` && `buyerInfo.identityType: "CONTACT"`       | `buyerInfo.contactId`                                                     |
| `buyerInfo.firstName`                                       | `billingInfo.contactDetails.firstName`                                    |
| `buyerInfo.lastName`                                        | `billingInfo.contactDetails.lastName`                                     |
| `buyerInfo.phone`                                           | `billingInfo.contactDetails.phone`                                        |
| `buyerInfo.email`*                                          | `buyerInfo.email`                                                         |
| `currency`*                                                 | `currency`                                                                |
| `weightUnit`*                                               | `weightUnit`                                                              |
| `totals.subtotal`                                           | `priceSummary.subtotal.amount`                                            |
| `totals.shipping`                                           | `priceSummary.shipping.amount`                                            |
| `totals.tax`                                                | `priceSummary.tax.amount`                                                 |
| `totals.discount`                                           | `priceSummary.discount.amount`                                            |
| `totals.total`                                              | `priceSummary.totalPrice.amount`                                          |
| `totals.weight`                                             | An order's total weight equals `(lineItems[0].physicalProperties.weight` X `lineItems[0].quantity)` + `(lineItems[1].physicalProperties.weight` X `lineItems[1].quantity)` and so on. |
| `totals.quantity`                                           | An order's total line item quantity equals `lineItems[0].quantity` + `lineItems[1].quantity` + `lineItems[2].quantity` and so on.    |
| `totals.refund`  | Accessible via the Order Payments API, an order's total refunds equal `orderTransactions.refunds[0].transactions.amount` + `orderTransactions.refunds[1].transactions.amount` and so on.    | Pass `order.id` to the [List Transactions For Single Order](https://bo.wix.com/wix-docs/rest/ecommerce/order-payments/list-transactions-for-single-order) endpoint in the Order Payments API
| `totals.giftCard` | Accessible via the Order Payments API, an order's gift card amount is `orderTransactions.payments[i].amount` where `orderTransactions.payments[i].giftcardPaymentDetails` has value.       | Pass `order.id` to the [List Transactions For Single Order](https://bo.wix.com/wix-docs/rest/ecommerce/order-payments/list-transactions-for-single-order) endpoint in the Order Payments API. Currently there can be only 1 gift card in the payments array (only 1 item in the array that has `giftcardPaymentDetails` defined). This may change in the future.
| `billingInfo.paymentMethod`                                 | Accessible via the Order Payments API - `orderTransactions.payments[i].regularPaymentDetails.paymentMethod`       | Pass `order.id` to the [List Transactions For Single Order](https://bo.wix.com/wix-docs/rest/ecommerce/order-payments/list-transactions-for-single-order) endpoint in the Order Payments API. Note that in the past an order only had 1 transaction, and therefore a single payment method - now we support multiple transactions and therefore also multiple payment methods.
| `billingInfo.paymentProviderTransactionId`                  | Accessible via the Order Payments API - `orderTransactions.payments[i].regularPaymentDetails.providerTransactionId`| Pass `order.id` to the [List Transactions For Single Order](https://bo.wix.com/wix-docs/rest/ecommerce/order-payments/list-transactions-for-single-order) endpoint in the Order Payments API. Note that in the past an order only had 1 transaction, and therefore a single provider transaction ID - now we support multiple transactions and therefore also multiple provider transaction IDs.
| `billingInfo.paymentGatewayTransactionId`                   | Accessible via the Order Payments API - `orderTransactions.payments[i].regularPaymentDetails.gatewayTransactionId` | Pass `order.id` to the [List Transactions For Single Order](https://bo.wix.com/wix-docs/rest/ecommerce/order-payments/list-transactions-for-single-order) endpoint in the Order Payments API. Note that in the past an order only had 1 transaction, and therefore a single gateway transaction ID - now we support multiple transactions and therefore also multiple gateway transaction IDs.
| `billingInfo.paidDate`                                      | Accessible via the Order Payments API - `orderTransactions.payments[i].createdDate/updatedDate`                    | Pass `order.id` to the [List Transactions For Single Order](https://bo.wix.com/wix-docs/rest/ecommerce/order-payments/list-transactions-for-single-order) endpoint in the Order Payments API. Note that in the past an order only had 1 transaction, and therefore a single paid date - now we support multiple transactions and therefore also multiple payment dates.
| `billingInfo.refundableByPaymentProvider`                   | Accessible via the Order Payments API - `orderTransactions.payments[i].refundDisabled`                             | Pass `order.id` to the [List Transactions For Single Order](https://bo.wix.com/wix-docs/rest/ecommerce/order-payments/list-transactions-for-single-order) endpoint in the Order Payments API. Note that in the past an order only had 1 transaction, and therefore a single disabled refund - now we support multiple transactions and therefore you should check each payment to check if refund is disabled.
| `billingInfo.address`*                                      | `billingInfo.address`                                                     | [Address object conversion table](https://bo.wix.com/wix-docs/rest/ecommerce/orders/address-object-conversion)
| `shippingInfo.code`*                                        | `shippingInfo.code`                                                       |
| `shippingInfo.deliverByDate`                                | `shippingInfo.logistics.deliverByDate`                                    |
| `shippingInfo.deliveryOption`                               | `shippingInfo.title`                                                      |
| `shippingInfo.shippingRegion`                               | `shippingInfo.region.name`                                                |
| `shippingInfo.shippingDetails.address`                      | `shippingInfo.logistics.shippingDestination.address`                      | [Address object conversion table](https://bo.wix.com/wix-docs/rest/ecommerce/orders/address-object-conversion)
| `shippingInfo.shipmentDetails.discount`                     | `shippingInfo.cost.discount.amount`                                       |
| `shippingInfo.shipmentDetails.tax`                          | `shippingInfo.cost.taxDetails.totalTax.amount`                            |
| `shippingInfo.shipmentDetails.priceData.taxIncludedInPrice` | -                                                                         | If `shippingInfo.cost.price` jas the same value as `shippingInfo.cost.totalPriceAfterTax` then tax is included in price
| `shippingInfo.shipmentDetails.priceData.price`              | `shippingInfo.cost.totalPriceAfterTax.amount`                             |
| `shippingInfo.pickupDetails.pickupAddress`                  | `shippingInfo.logistics.pickupDetails.address`                            | [Address object conversion table](https://bo.wix.com/wix-docs/rest/ecommerce/orders/address-object-conversion)
| `shippingInfo.pickupDetails.pickupInstructions`             | `shippingInfo.logistics.instructions`                                     |
| `shippingInfo.estimatedDeliveryTime`                        | `shippingInfo.logistics.deliveryTime`                                     |
| `buyerNote`*                                                | `buyerNote`                                                               |
| `archived`*                                                 | `archived`                                                                |
| `paymentStatus`*                                            | `paymentStatus`                                                           |
| `paymentStatus` == `PENDING`                                | `status` == `INITIALIZED`                                                 |
| `fulfillmentStatus`*                                        | `fulfillmentStatus`                                                       | More info available by passing `order.id` to [List Fulfillments For Single Order](https://bo.wix.com/wix-docs/rest/ecommerce/order-fulfillments/list-fulfillments-for-single-order)
| `fulfillmentStatus` == `CANCELED`                           | `status` == `CANCELED`                                                    | More info available by passing `order.id` to [List Fulfillments For Single Order](https://bo.wix.com/wix-docs/rest/ecommerce/order-fulfillments/list-fulfillments-for-single-order)
| `lineItems[i].index`                                        | `lineItems[i].id`                                                            | While `lineItems[i].index` was int32 type, the eCommerce Order's `lineItems[i].id` field is of type GUID
| `lineItems[i].quantity`*                                    | `lineItems[i].quantity`                                                      |
| `lineItems[i].name`                                         | `lineItems[i].productName.original`                                          |
| `lineItems[i].translatedName`                               | `lineItems[i].productName.translated`                                        |
| `lineItems[i].productId`                                    | `lineItems[i].catalogReference.catalogItemId`                                | [Stores Catalog eCommerce Reference](https://bo.wix.com/wix-docs/rest/stores/stores-catalog/ecommerce-integration)
| `lineItems[i].lineItemType: "PHYSICAL"`                     | `lineItems[i].itemType.preset: "PHYSICAL"`                                   |
| `lineItems[i].lineItemType: "DIGITAL"`                      | `lineItems[i].itemType.preset: "DIGITAL"`                                    |
| `lineItems[i].lineItemType: "CUSTOM_AMOUNT_ITEM"`           | `lineItems[i].catalogReference` is empty   |
| `lineItems[i].options`                                      | `lineItems[i].catalogReference.options`                                      | [Stores Catalog eCommerce Reference](https://bo.wix.com/wix-docs/rest/stores/stores-catalog/ecommerce-integration)
| `lineItems[i].customTextFields`                             | `lineItems[i].descriptionLines`                                              |
| `lineItems[i].weight`                                       | `lineItems[i].physicalProperties.weight`                                     |
| `lineItems[i].mediaItem.url`                                | `lineItems[i].image.url`                                                     |
| `lineItems[i].mediaItem.height`                             | `lineItems[i].image.height`                                                  |
| `lineItems[i].mediaItem.width`                              | `lineItems[i].image.width`                                                   |
| `lineItems[i].mediaItem.id`                                 | `lineItems[i].image.id`                                                      |
| `lineItems[i].mediaItem.altText`                            | `lineItems[i].image.altText`                                                 |
| `lineItems[i].sku`                                          | `lineItems[i].physicalProperties.sku`                                        |
| `lineItems[i].notes`                                        | `lineItems[i].descriptionLines[i].plainTextValue.original`                      |
| `lineItems[i].variantId`                                    | `lineItems[i].catalogReference.options`                                      | [Stores Catalog eCommerce Reference](https://bo.wix.com/wix-docs/rest/stores/stores-catalog/ecommerce-integration)
| `lineItems[i].fulfillerId`*                                 | `lineItems[i].fulfillerId`                                                   |
| `lineItems[i].discount`                                     | `lineItems[i].totalDiscount.amount`                                          |
| `lineItems[i].tax`                                          | `lineItems[i].taxDetails.totalTax.amount`                                    |
| `lineItems[i].priceData.taxIncludedInPrice`                 | -                                                                         | If `lineItems[i].price` equals `lineItems[i].totalPriceAfterTax` then tax is included
| `lineItems[i].priceData.price`                              | `lineItems[i].price.amount`                                                  |
| `lineItems[i].priceData.totalPrice`                         | `lineItems[i].totalPriceAfterTax.amount`                                     |
| `activities[i].type`*                                          | `activities[i].type`                                                         |
| `activities[i].TRACKING_LINK_WAS_SET`                          | `activities[i].TRACKING_LINK_SET`                                            |
| `activities[i].INVOICE_WAS_SET`                                | `activities[i].INVOICE_ADDED`                                                |
| `activities[i].INVOICE_WAS_SENT`                               | `activities[i].INVOICE_SENT`                                                 |
| `activities[i].author`                                         | `activities[i].authorEmail`                                                  |
| `activities[i].message`                                        | `activities[i].merchantComment.message`                                      | If `activities.type = "MERCHANT_COMMENT"`
| `activities[i].timestamp`                                      | `activities[i].createdDate`                                                  |
| `invoiceInfo`                                               | `invoices`                                                                | Pass `order.id` to the [List Invoices For Single Order](https://bo.wix.com/wix-docs/rest/ecommerce/order-payments/list-invoices-for-single-order) endpoint in the Order Payments API
| `fulfillments`                                              | `orderWithFulfillments.fulfillments`                                      | Pass `order.id` to the [List Fulfillments For Single Order](https://bo.wix.com/wix-docs/rest/ecommerce/order-fulfillments/list-fulfillments-for-single-order) endpoint in the Order Fulfillments API
| `discount.appliedCoupon.couponId`                           | `appliedDiscounts[i].coupon.id`   | Search the `appliedDiscounts` array for the only populated `coupon` field; `couponId` is `coupon.id`
| `discount.appliedCoupon.name`                               | `appliedDiscounts[i].coupon.name` | Search the `appliedDiscounts` array for the only populated `coupon` field; `name` is `coupon.name`
| `discount.appliedCoupon.code`                               | `appliedDiscounts[i].coupon.code` | Search the `appliedDiscounts` array for the only populated `coupon` field; `code` is `coupon.code`
| `customField.value`                                         | `customFields[i].value.stringValue`                                       | Note: `customFields` is an array
| `customField.title`                                         | `customFields[i].title`                                                   |
| `customField.translatedTitle`                               | `customFields[i].translatedTitle`                                         |
| `cartId`                                                    | -                                                                         | Replaced by `checkoutId`
| `buyerLanguage`*                                            | `buyerLanguage`                                                           |
| `channelInfo.type`*                                         | `channelInfo.type`                                                        |
| `channelInfo.externalOrderId`*                              | `channelInfo.externalOrderId`                                             |
| `channelInfo.externalOrderUrl`*                             | `channelInfo.externalOrderUrl`                                            |
| `enteredBy.id` $$ `enteredBy.identityType: "MEMBER"`        | `createdBy.memberId`                                                      |
| `enteredBy.id` $$ `enteredBy.identityType: "USER"`          | `createdBy.userId`                                                        |
| `enteredBy.id` $$ `enteredBy.identityType: "APP"`           | `createdBy.appId`                                                         |
| `enteredBy.id` $$ `enteredBy.identityType: "CONTACT"`       | `createdBy.visitorId` | Previously, for a buyer that is not logged in, `CONTACT` type and ID were returned. in the eCommerce API, `visitorId` is returned. Note: the ID itself will also be different.
| `lastUpdated`                                               | `updatedDate`                                                             |
| `numericId`                                                 | -                                                                         | Removed due to added cursor paging functionality
| `refunds`                                                   | `orderTransactions.refunds`                                               | Pass `order.id` to the [List Transactions For Single Order](https://bo.wix.com/wix-docs/rest/ecommerce/order-payments/list-transactions-for-single-order) endpoint in the Order Payments API

*Fields marked with an asterisk signify little to no change in semantics or access.


## Webhooks Conversion Table

The following list shows old Stores Orders webhooks and the new eCommerce webhooks (across Orders, Order Payments, and Order Fulfillments) that are triggered at the same time:

| Stores Orders API                                                                         | eCommerce Orders API                                                         |
|----------------------------------------------------------------------------------------|---------------------------------------------------------------------------------|
| [Order Paid Webhook](https://dev.wix.com/api/rest/wix-stores/orders/order-paid-webhook) | Orders - [Payment Status Updated Webhook](https://bo.wix.com/wix-docs/rest/ecommerce/orders/payment-status-updated-domain-event) sent with `order.paymentStatus = PAID` |
| [Order Created Webhook](https://dev.wix.com/api/rest/wix-stores/orders/order-created-webhook) | Orders - [Order Approved Webhook](https://bo.wix.com/wix-docs/rest/ecommerce/orders/order-approved-domain-event)  |
| [Order Canceled Webhook](https://dev.wix.com/api/rest/wix-stores/orders/order-canceled-webhook) | Orders - [Order Canceled Webhook](https://bo.wix.com/wix-docs/rest/ecommerce/orders/order-canceled-domain-event) |
| [Order Refunded Webhook](https://dev.wix.com/api/rest/wix-stores/orders/order-refunded-webhook) | Order Payments -  [Refund Created Webhook](https://bo.wix.com/wix-docs/rest/ecommerce/order-payments/refund-created-domain-event) |
| Fulfillment [Created](https://dev.wix.com/api/rest/wix-stores/orders/fulfillment-created-webhook) / [Updated](https://dev.wix.com/api/rest/wix-stores/orders/fulfillment-updated-webhook) / [Deleted](https://dev.wix.com/api/rest/wix-stores/orders/fulfillment-deleted-webhook) Webhooks | [Order With Fulfillments Updated Webhook](https://bo.wix.com/wix-docs/rest/ecommerce/order-fulfillments/order-with-fulfillments-updated-domain-event) |