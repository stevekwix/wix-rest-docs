SortOrder: 1
# Old Cart to New Checkout Conversion Table

To help with migration from the old [Stores Cart API](https://dev.wix.com/api/rest/wix-stores/carts/cart-object) to the new eCommerce [Checkout](https://bo.wix.com/wix-docs/rest/ecommerce/checkout/introduction) API, refer to the table below for changes in name and/or location.

The address object used in the new eCommerce APIs is slightly different to the one used in the Stores APIs. For more details, refer to the [address object conversion table](https://bo.wix.com/wix-docs/rest/ecommerce/orders/address-object-conversion).

| Stores Cart Object                              | eCommerce Checkout Object                                 |
| ------------------------------------------------|-----------------------------------------------------------|
| `id`                                            | -                                                         |
| `status`                                        | -                                                         |
| `weightUnit`                                    | `weightUnit`                                              |
| `buyerNote`                                     | `buyerNote`                                               |
| `currency.code`                                 | `currency`                                                |
| `currency.symbol`                               | -                                                         |
| `convertedCurrency.code`                        | `conversionCurrency`                                      |
| `convertedCurrency.symbol`                      | -                                                         |
| `billingAddress.address`| `billingInfo.address` - See [address object conversion table](https://bo.wix.com/wix-docs/rest/ecommerce/orders/address-object-conversion) for more details.
| `billingAddress.contactDetails.firstName`       | `billingInfo.contactDetails.firstName`              |
| `billingAddress.contactDetails.lastName`        | `billingInfo.contactDetails.lastName`               |
| `billingAddress.contactDetails.phone`           | `billingInfo.contactDetails.phone`              |
| `billingAddress.contactDetails.company`         | `billingInfo.contactDetails.company`              |
| `billingAddress.contactDetails.vatId`           | `billingInfo.contactDetails.vatId`              |
| `billingAddress.contactDetails.email`           | `billingInfo.buyerInfo.email`              |
| `appliedCoupon.couponId`                        | `appliedDiscounts[i].coupon.id`                                               |
| `appliedCoupon.name`                            | `appliedDiscounts[i].coupon.name`                                               |
| `appliedCoupon.code`                            | `appliedDiscounts[i].coupon.code`                                               |
| `appliedCoupon.discountValue`                   | `appliedDiscounts[i].coupon.amount.amount`                                 |
| `appliedCoupon.convertedDiscountValue`          | `appliedDiscounts[i].coupon.convertedAmount`                               |
| `appliedCoupon.couponType`                      | -                                              |
| `totals.subtotal`                               | `priceSummary.subtotal.amount`                                               |
| `totals.shipping`                               | `priceSummary.shipping.amount`                                               |
| `totals.tax`                                    | `priceSummary.tax.amount`                                               |
| `totals.discount`                               | `priceSummary.discount.amount`                                               |
| `totals.total`                                  | `priceSummary.total.amount`                                               |
| `totals.weight`                                 | `lineItems[i].physicalProperties.weight` X `lineItems[i].quantity` and so on.                                            |
| `totals.quantity`                               | `lineItems[0].quantity` + `lineItems[1].quantity` + `lineItems[2].quantity` and so on.                          |
| `convertedTotals.subtotal`                      | `priceSummary.subtotal.convertedAmount`                                               |
| `convertedTotals.shipping`                      | `priceSummary.shipping.convertedAmount`                                               |
| `convertedTotals.tax`                           | `priceSummary.tax.convertedAmount`                                               |
| `convertedTotals.discount`                      | `priceSummary.discount.convertedAmount`                                               |
| `convertedTotals.total`                         | `priceSummary.total.convertedAmount`                                               |
| `convertedTotals.weight`                        | No weight conversion in checkout. Same value as `cart.totals.weight`.|
| `convertedTotals.quantity`                      | Same value as `cart.totals.quantity`.                        |
| `shippingInfo.shippingRuleDetails.ruleId`                | `ֿֿֿֿֿֿֿֿshippingInfo.region.id`                                               |
| `shippingInfo.shippingRuleDetails.optionId`              | `ֿֿֿֿֿֿֿֿshippingInfo.selectedCarrierServiceOption.title`                                              |
| `shippingInfo.shippingRuleDetails.deliveryOption`        | `ֿֿֿֿֿֿֿֿshippingInfo.selectedCarrierServiceOption.title`                                                |
| `shippingInfo.shippingRuleDetails.estimatedDeliveryTime` | `ֿֿֿֿֿֿֿֿshippingInfo.logistics.deliveryTime`                                              |
| `shippingInfo.pickupDetails.pickupAddress`               | `shippingInfo.selectedCarrierServiceOption.logistics.pickupDetails.address` - See [address object conversion table](https://bo.wix.com/wix-docs/rest/ecommerce/orders/address-object-conversion) for more details.  |
| `shippingInfo.pickupDetails.buyerDetails.firstName`      | `shippingInfo.shippingDestination.contactDetails.firstName`                                     |
| `shippingInfo.pickupDetails.buyerDetails.lastName`       | `shippingInfo.shippingDestination.contactDetails.lastName`                                     |
| `shippingInfo.pickupDetails.buyerDetails.email`          | `buyerInfo.email`                                     |
| `shippingInfo.pickupDetails.buyerDetails.phone`          | `shippingInfo.shippingDestination.contactDetails.phone`                                     |
| `shippingInfo.pickupDetails.pickupInstructions`    | `shippingInfo.logistics.instructions`                                     |
| `shippingInfo.shippingAddress.address`             | `shippingInfo.shippingDestination.address` - See [address object conversion table](https://bo.wix.com/wix-docs/rest/ecommerce/orders/address-object-conversion) for more details.  |
| `shippingInfo.shippingAddress.contactDetails`      | `shippingInfo.shippingDestination.contactDetails` |          |
| `buyerInfo.id` && `buyerInfo.identityType: CONTACT`| `buyerInfo.contactId`                                               |
| `buyerInfo.id` && `buyerInfo.identityType: VISITOR`| `buyerInfo.visitorId`                                               |
| `buyerInfo.id` && `buyerInfo.identityType: MEMBER` | `buyerInfo.memberId`                                               |
| `buyerInfo.email`                                  | `buyerInfo.email`                                               |
| `buyerInfo.phone`                                  | `billingInfo.contactDetails.phone`                                        |
| `buyerInfo.firstName`                              | `billingInfo.contactDetails.firstName`                                    |
| `buyerInfo.lastName`                               | `billingInfo.contactDetails.lastName`                                     |
| `lineItems[i].id`                                  | `lineItems[i].id` - Note: this `id` is of type GUID. In the old Stores Cart API, this `id` was of type Int32.                                               |
| `lineItems[i].productId`                           | `lineItems[i].catalogReference.catalogItemId` - Learn more about the [Catalog SPI](https://bo.wix.com/wix-docs/rest/ecommerce/catalog-spi/introduction).
| `lineItems[i].name`                                | `lineItems[i].productName.original`                          |
| `lineItems[i].quantity`                            | `lineItems[i].quantity`                          |
| `lineItems[i].weight`                              | `lineItems[i].physicalProperties.weight`                  |
| `lineItems[i].sku`                                 | `lineItems[i].physicalProperties.sku`                                               |
| `lineItems[i].lineItemType: "PHYSICAL"`            | `lineItems[i].itemType.preset: "PHYSICAL"`                                |
| `lineItems[i].lineItemType: "DIGITAL"`             | `lineItems[i].itemType.preset: "DIGITAL"`                               |
| `lineItems[i].lineItemType: "CUSTOM_AMOUNT_IT`     | `lineItems[i].itemType.custom` && `lineItems[i].catalogReference` is empty.            |
| `lineItems[i].notes`                               | -                                               |
| `lineItems[i].customTextFields`                    | `lineItems[i].descriptionLines`                                             |
| `lineItems[i].mediaItem.mediaType`                 | All line item media in the eCommerce Cart, Checkout, and Order APIs are images.
| `lineItems[i].mediaItem.url`                       | `lineItems[i].media.url`                                               |
| `lineItems[i].mediaItem.width`                     | `lineItems[i].media.width`                                               |
| `lineItems[i].mediaItem.height`                    | `lineItems[i].media.height`                                               |
| `lineItems[i].options`                             | `lineItems[i].catalogReference.options` - Learn more about the [Catalog SPI](https://bo.wix.com/wix-docs/rest/ecommerce/catalog-spi/introduction).
| `lineItems[i].priceData.price`                     | `lineItems[i].price.amount`                                               |
| `lineItems[i].priceData.totalPrice`                | `lineItems[i].price.amount` X `lineItems[i].quantity`                                 |
| `lineItems[i].convertedPriceData.price`            | `lineItems[i].price.convertedAmount`                                               |
| `lineItems[i].convertedPriceData.totalPrice`       | `lineItems[i].price.convertedAmount` X `lineItems[i].quantity`                       |