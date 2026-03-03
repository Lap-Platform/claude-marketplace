---
name: order-api
description: "Order API skill. Use when working with Order for guest_checkout_session, guest_purchase_order. Covers 8 endpoints."
version: 1.0.0
generator: lapsh
---

# Order API
API version: v2.1.2

## Auth
OAuth2

## Base URL
https://apix.ebay.com{basePath}

## Setup
1. Configure auth: OAuth2
2. GET /guest_checkout_session/{checkoutSessionId} -- verify access
3. POST /guest_checkout_session/{checkoutSessionId}/apply_coupon -- create first apply_coupon

## Endpoints

8 endpoints across 2 groups. See references/api-spec.lap for full details.

### guest_checkout_session
| Method | Path | Description |
|--------|------|-------------|
| POST | /guest_checkout_session/{checkoutSessionId}/apply_coupon | <span class="tablenote"><b>Note:</b> The Order API (v2) currently only supports the guest payment/checkout flow. If you need to support member payment/checkout flow, use the <a href="/api-docs/buy/order_v1/resources/methods">v1_beta version</a> of the Order API.</span><br><div class="msgbox_important"><p class="msgbox_importantInDiv" data-mc-autonum="&lt;b&gt;&lt;span style=&quot;color: #dd1e31;&quot; class=&quot;mcFormatColor&quot;&gt;Important! &lt;/span&gt;&lt;/b&gt;"><span class="autonumber"><span><b><span style="color: #dd1e31;" class="mcFormatColor">Important!</span></b></span></span> <a href="https://developer.ebay.com/api-docs/static/versioning.html#limited" target="_blank"><img src="/cms/img/docs/partners-api.svg" class="legend-icon partners-icon"  alt="Limited Release" title="Limited Release" />(Limited Release)</a> This method is only available to select developers approved by business units.</p></div><br>This method adds a coupon to an eBay guest checkout session and applies it to all the eligible items in the order.<br><br>The <b>checkoutSessionId</b> is passed in as a URI parameter and is required. The redemption code of the coupon is in the payload and is also required.<br><br>For a list of supported sites and other restrictions, see <a href="/api-docs/buy/order/overview.html#API">API Restrictions</a> in the Order API overview. |
| GET | /guest_checkout_session/{checkoutSessionId} | <span class="tablenote"><b>Note:</b> The Order API (v2) currently only supports the guest payment/checkout flow. If you need to support member payment/checkout flow, use the <a href="/api-docs/buy/order_v1/resources/methods">v1_beta version</a> of the Order API.</span><br><div class="msgbox_important"><p class="msgbox_importantInDiv" data-mc-autonum="&lt;b&gt;&lt;span style=&quot;color: #dd1e31;&quot; class=&quot;mcFormatColor&quot;&gt;Important! &lt;/span&gt;&lt;/b&gt;"><span class="autonumber"><span><b><span style="color: #dd1e31;" class="mcFormatColor">Important!</span></b></span></span> <a href="https://developer.ebay.com/api-docs/static/versioning.html#limited" target="_blank"><img src="/cms/img/docs/partners-api.svg" class="legend-icon partners-icon"  alt="Limited Release" title="Limited Release" />(Limited Release)</a> This method is only available to select developers approved by business units.</p></div><br>This method returns the details of the specified guest checkout session. The <b>checkoutSessionId</b> is passed in as a URI parameter and is required. This method has no request payload.<br><br>For a list of supported sites and other restrictions, see <a href="/api-docs/buy/order/overview.html#API">API Restrictions</a> in the Order API overview. |
| POST | /guest_checkout_session/initiate | <span class="tablenote"><b>Note:</b> The Order API (v2) currently only supports the guest payment/checkout flow. If you need to support member payment/checkout flow, use the <a href="/api-docs/buy/order_v1/resources/methods">v1_beta version</a> of the Order API.</span><br><div class="msgbox_important"><p class="msgbox_importantInDiv" data-mc-autonum="&lt;b&gt;&lt;span style=&quot;color: #dd1e31;&quot; class=&quot;mcFormatColor&quot;&gt;Important! &lt;/span&gt;&lt;/b&gt;"><span class="autonumber"><span><b><span style="color: #dd1e31;" class="mcFormatColor">Important!</span></b></span></span> <a href="https://developer.ebay.com/api-docs/static/versioning.html#limited" target="_blank"><img src="/cms/img/docs/partners-api.svg" class="legend-icon partners-icon"  alt="Limited Release" title="Limited Release" />(Limited Release)</a> This method is only available to select developers approved by business units.</p></div><br>This method creates an eBay guest checkout session, which is the first step in performing a checkout. The method returns a <b>checkoutSessionId</b> that you use as a URI parameter in subsequent guest checkout methods.  <br><br><span class="tablenote"><b>Note:</b> This method also returns the <b>X-EBAY-SECURITY-SIGNATURE</b> response header, which is a token that is used to launch the Checkout with eBay widget. The Checkout with eBay widget allows eBay guests to pay for items without leaving your site. For details about the Checkout with eBay widget, see <a href="/api-docs/buy/static/api-order.html#Integrat">Integrating the Checkout with eBay button</a>. </span><br>Also see <a href="/api-docs/buy/static/ref-buy-negative-testing.html">Negative Testing Using Stubs</a> for information on how to emulate error conditions for this  method using stubs.<br><br><span class="tablenote"><font color="006600"><b>TIP:</b></font> To test the entire checkout flow, you might need a "test" credit card. You can generate a credit card number from <a href="http://www.getcreditcardnumbers.com" target="_blank">http://www.getcreditcardnumbers.com</a>.</span><br>For a list of supported sites and other restrictions, see <a href="/api-docs/buy/order/overview.html#API">API Restrictions</a> in the Order API overview. |
| POST | /guest_checkout_session/{checkoutSessionId}/remove_coupon | <span class="tablenote"><b>Note:</b> The Order API (v2) currently only supports the guest payment/checkout flow. If you need to support member payment/checkout flow, use the <a href="/api-docs/buy/order_v1/resources/methods">v1_beta version</a> of the Order API.</span><br><div class="msgbox_important"><p class="msgbox_importantInDiv" data-mc-autonum="&lt;b&gt;&lt;span style=&quot;color: #dd1e31;&quot; class=&quot;mcFormatColor&quot;&gt;Important! &lt;/span&gt;&lt;/b&gt;"><span class="autonumber"><span><b><span style="color: #dd1e31;" class="mcFormatColor">Important!</span></b></span></span> <a href="https://developer.ebay.com/api-docs/static/versioning.html#limited" target="_blank"><img src="/cms/img/docs/partners-api.svg" class="legend-icon partners-icon"  alt="Limited Release" title="Limited Release" />(Limited Release)</a> This method is only available to select developers approved by business units.</p></div><br>This method removes a coupon from an eBay guest checkout session. The <b>checkoutSessionId</b> is passed in as a URI parameter and is required. The redemption code of the coupon is specified in the payload and is also required.<br><br>For a list of supported sites and other restrictions, see <a href="/api-docs/buy/order/overview.html#API">API Restrictions</a> in the Order API overview. |
| POST | /guest_checkout_session/{checkoutSessionId}/update_quantity | <span class="tablenote"><b>Note:</b> The Order API (v2) currently only supports the guest payment/checkout flow. If you need to support member payment/checkout flow, use the <a href="/api-docs/buy/order_v1/resources/methods">v1_beta version</a> of the Order API.</span><br><div class="msgbox_important"><p class="msgbox_importantInDiv" data-mc-autonum="&lt;b&gt;&lt;span style=&quot;color: #dd1e31;&quot; class=&quot;mcFormatColor&quot;&gt;Important! &lt;/span&gt;&lt;/b&gt;"><span class="autonumber"><span><b><span style="color: #dd1e31;" class="mcFormatColor">Important!</span></b></span></span> <a href="https://developer.ebay.com/api-docs/static/versioning.html#limited" target="_blank"><img src="/cms/img/docs/partners-api.svg" class="legend-icon partners-icon"  alt="Limited Release" title="Limited Release" />(Limited Release)</a> This method is only available to select developers approved by business units.</p></div><br>This method changes the quantity of the specified line item in an eBay guest checkout session.<br><br>For a list of supported sites and other restrictions, see <a href="/api-docs/buy/order/overview.html#API">API Restrictions</a> in the Order API overview. |
| POST | /guest_checkout_session/{checkoutSessionId}/update_shipping_address | <span class="tablenote"><b>Note:</b> The Order API (v2) currently only supports the guest payment/checkout flow. If you need to support member payment/checkout flow, use the <a href="/api-docs/buy/order_v1/resources/methods">v1_beta version</a> of the Order API.</span><br><div class="msgbox_important"><p class="msgbox_importantInDiv" data-mc-autonum="&lt;b&gt;&lt;span style=&quot;color: #dd1e31;&quot; class=&quot;mcFormatColor&quot;&gt;Important! &lt;/span&gt;&lt;/b&gt;"><span class="autonumber"><span><b><span style="color: #dd1e31;" class="mcFormatColor">Important!</span></b></span></span> <a href="https://developer.ebay.com/api-docs/static/versioning.html#limited" target="_blank"><img src="/cms/img/docs/partners-api.svg" class="legend-icon partners-icon"  alt="Limited Release" title="Limited Release" />(Limited Release)</a> This method is only available to select developers approved by business units.</p></div><br>This method changes the shipping address for the order in an eBay guest checkout session. All the line items in an order must be shipped to the same address, but the shipping method can be specific to the line item.<br><br><span class="tablenote"><b>Note:</b> If the address submitted cannot be validated, a warning message will be returned. This does not prevent the method from executing, but you may want to verify the address.</span><br>For a list of supported sites and other restrictions, see <a href="/api-docs/buy/order/overview.html#API">API Restrictions</a> in the Order API overview. |
| POST | /guest_checkout_session/{checkoutSessionId}/update_shipping_option | <span class="tablenote"><b>Note:</b> The Order API (v2) currently only supports the guest payment/checkout flow. If you need to support member payment/checkout flow, use the <a href="/api-docs/buy/order_v1/resources/methods">v1_beta version</a> of the Order API.</span><br><div class="msgbox_important"><p class="msgbox_importantInDiv" data-mc-autonum="&lt;b&gt;&lt;span style=&quot;color: #dd1e31;&quot; class=&quot;mcFormatColor&quot;&gt;Important! &lt;/span&gt;&lt;/b&gt;"><span class="autonumber"><span><b><span style="color: #dd1e31;" class="mcFormatColor">Important!</span></b></span></span> <a href="https://developer.ebay.com/api-docs/static/versioning.html#limited" target="_blank"><img src="/cms/img/docs/partners-api.svg" class="legend-icon partners-icon"  alt="Limited Release" title="Limited Release" />(Limited Release)</a> This method is only available to select developers approved by business units.</p></div><br>This method changes the shipping method for the specified line item in an eBay guest checkout session. The shipping option can be set for each line item. This gives the shopper the ability choose the cost of shipping for each line item.<br><br>For a list of supported sites and other restrictions, see <a href="/api-docs/buy/order/overview.html#API">API Restrictions</a> in the Order API overview. |

### guest_purchase_order
| Method | Path | Description |
|--------|------|-------------|
| GET | /guest_purchase_order/{purchaseOrderId} | <span class="tablenote"><b>Note:</b> The Order API (v2) currently only supports the guest payment/checkout flow. If you need to support member payment/checkout flow, use the <a href="/api-docs/buy/order_v1/resources/methods">v1_beta version</a> of the Order API.</span><br><div class="msgbox_important"><p class="msgbox_importantInDiv" data-mc-autonum="&lt;b&gt;&lt;span style=&quot;color: #dd1e31;&quot; class=&quot;mcFormatColor&quot;&gt;Important! &lt;/span&gt;&lt;/b&gt;"><span class="autonumber"><span><b><span style="color: #dd1e31;" class="mcFormatColor">Important!</span></b></span></span> <a href="https://developer.ebay.com/api-docs/static/versioning.html#limited" target="_blank"><img src="/cms/img/docs/partners-api.svg" class="legend-icon partners-icon"  alt="Limited Release" title="Limited Release" />(Limited Release)</a> This method is only available to select developers approved by business units.</p></div><br>This method retrieves the details about a specific guest purchase order. It returns the line items, including purchase  order status, dates created and modified, item quantity and listing data, payment and shipping information, and prices, taxes, discounts and credits.<br><br>The <b>purchaseOrderId</b> is passed in as a URI parameter and is required.<br><br><span class="tablenote"><b>Note:</b> The <b>purchaseOrderId</b> value is returned in the call-back URL that is sent through the new eBay pay widget. For more information about eBay managed payments and the new Order API payment flow, see <a href="/api-docs/buy/static/api-order.html">Order API</a> in the Buying Integration Guide.</span><br>You can use this method to not only get the details of a purchase order, but to check the value of the <a href="#response.purchaseOrderPaymentStatus">purchaseOrderPaymentStatus</a> field to determine if the order has been paid for. If the order has been paid for, this field will return <code>PAID</code>.<br><br>For a list of supported sites and other restrictions, see <a href="/api-docs/buy/order/overview.html#API">API Restrictions</a> in the Order API overview. |

## Enhanced Skill Content
## Question Mapping

- "How do I start a guest checkout for an eBay item?" -> POST /guest_checkout_session/initiate
- "How do I check the current state of my checkout session?" -> GET /guest_checkout_session/{checkoutSessionId}
- "How do I apply a coupon or promo code to my cart?" -> POST /guest_checkout_session/{checkoutSessionId}/apply_coupon
- "How do I remove a coupon I already applied?" -> POST /guest_checkout_session/{checkoutSessionId}/remove_coupon
- "How do I change the quantity of an item in my checkout?" -> POST /guest_checkout_session/{checkoutSessionId}/update_quantity
- "How do I update the shipping address for my order?" -> POST /guest_checkout_session/{checkoutSessionId}/update_shipping_address
- "How do I pick a different shipping option for a line item?" -> POST /guest_checkout_session/{checkoutSessionId}/update_shipping_option
- "How do I look up a completed guest purchase order?" -> GET /guest_purchase_order/{purchaseOrderId}
- "What is the total price including taxes and fees for my checkout?" -> GET /guest_checkout_session/{checkoutSessionId} (read `pricingSummary.total`)
- "How do I check if import charges apply to my order?" -> GET /guest_checkout_session/{checkoutSessionId} (read `pricingSummary.importCharges`)
- "What coupons are currently applied to my session?" -> GET /guest_checkout_session/{checkoutSessionId} (read `appliedCoupons`)
- "What is the payment status of my guest purchase?" -> GET /guest_purchase_order/{purchaseOrderId} (read `purchaseOrderPaymentStatus`)
- "Has my guest order been refunded?" -> GET /guest_purchase_order/{purchaseOrderId} (read `refundedAmount`)
- "How do I swap a coupon (replace one with another)?" -> POST remove_coupon then POST apply_coupon (two-step)

## Response Tips

- **Checkout session endpoints**: All 7 endpoints return the same full session object. After any mutation (apply coupon, update address, etc.), the entire updated session is returned -- no need to GET again to see changes.
- **Pricing summary**: `pricingSummary` is deeply nested. Monetary values are always `{currency, value}` pairs where `value` is a string (not a number). Parse accordingly.
- **Warnings array**: Every checkout and order response includes a `warnings` array. Always surface these to the user -- they contain item-level issues like stock limits or shipping restrictions.
- **Purchase order**: The order response adds `purchaseOrderStatus`, `purchaseOrderPaymentStatus`, `purchaseOrderCreationDate`, and `refundedAmount` fields not present in checkout sessions. `deliveryDiscount` also appears only here.
- **Errors**: 409 (Conflict) is common on checkout mutations -- it typically means a concurrent modification or invalid session state. 403 usually indicates the session has expired or the marketplace header is wrong.

## Anomaly Flags

- **Warnings present**: Surface any entries in the `warnings` array immediately -- these indicate actionable problems (e.g., item out of stock, address undeliverable, quantity adjusted).
- **409 Conflict on mutations**: Flag when a session update returns 409. The session may have been modified concurrently or already completed. Re-fetch with GET before retrying.
- **Import charges or import tax populated**: Alert the user when `pricingSummary.importCharges` or `pricingSummary.importTax` contains a non-zero value -- this means cross-border fees apply.
- **Refunded amount on purchase order**: If `refundedAmount.value` is non-zero, proactively inform the user that a partial or full refund has been issued.
- **Missing marketplace header**: If a 400 or 403 error occurs, check whether `X-EBAY-C-MARKETPLACE-ID` was included. This common field is easy to forget and required for correct pricing/availability.
- **Price changes between calls**: Compare `pricingSummary.total` across sequential responses. If the total changes unexpectedly after an address or shipping update, surface the delta to the user.
- **Empty lineItems**: If the session returns an empty `lineItems` array, flag it -- the item may have been removed or is no longer available.

## Playbook

### 1. Complete a Guest Checkout (End to End)

1. Call `POST /guest_checkout_session/initiate` with `lineItemInputs` (itemId + quantity), `contactEmail`, and `shippingAddress`.
2. Save the returned `checkoutSessionId` for all subsequent calls.
3. Optionally apply a coupon via `POST /guest_checkout_session/{id}/apply_coupon` with the `redemptionCode`.
4. Review `pricingSummary` in the response to confirm totals, taxes, and delivery cost.
5. If shipping options are available in `lineItems`, select one via `POST /guest_checkout_session/{id}/update_shipping_option`.
6. Complete payment through eBay's payment flow (outside this API).
7. Retrieve the final order with `GET /guest_purchase_order/{purchaseOrderId}`.

### 2. Apply, Verify, and Swap a Coupon

1. Call `POST /guest_checkout_session/{id}/apply_coupon` with the `redemptionCode`.
2. Check `appliedCoupons` in the response to confirm it was accepted.
3. Compare `pricingSummary.priceDiscount` and `pricingSummary.total` to see the savings.
4. To swap for a different coupon, first call `POST /guest_checkout_session/{id}/remove_coupon` with the old code.
5. Then call `POST /guest_checkout_session/{id}/apply_coupon` with the new code.
6. Verify `appliedCoupons` again to confirm the swap.

### 3. Update Shipping Details After Session Creation

1. Call `GET /guest_checkout_session/{id}` to review current shipping address and options.
2. Call `POST /guest_checkout_session/{id}/update_shipping_address` with the corrected address fields.
3. Check the response for `warnings` -- address changes can trigger delivery restriction warnings.
4. Review updated `pricingSummary.deliveryCost` and `pricingSummary.total` since shipping cost may change.
5. If new shipping options become available, select one via `POST /guest_checkout_session/{id}/update_shipping_option`.

### 4. Modify Item Quantity in Cart

1. Call `GET /guest_checkout_session/{id}` and locate the target item's `lineItemId` in the `lineItems` array.
2. Call `POST /guest_checkout_session/{id}/update_quantity` with the `lineItemId` and new `quantity`.
3. Check `warnings` for stock-related issues (e.g., quantity exceeds available inventory).
4. Review `pricingSummary.priceSubtotal` and `pricingSummary.total` to confirm the updated pricing.

### 5. Track a Guest Purchase Order

1. After checkout completion, save the `purchaseOrderId`.
2. Call `GET /guest_purchase_order/{purchaseOrderId}` to retrieve order details.
3. Check `purchaseOrderStatus` for fulfillment state and `purchaseOrderPaymentStatus` for payment state.
4. If `refundedAmount.value` is non-zero, a refund has been processed -- check `warnings` for details.
5. Review `lineItems` for per-item shipping tracking and delivery estimates.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
