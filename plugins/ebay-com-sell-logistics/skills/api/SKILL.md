---
name: logistics-api
description: "Logistics API skill. Use when working with Logistics for shipment, shipping_quote. Covers 6 endpoints."
version: 1.0.0
generator: lapsh
---

# Logistics API
API version: v1_beta.0.0

## Auth
OAuth2

## Base URL
https://api.ebay.com{basePath}

## Setup
1. Configure auth: OAuth2
2. GET /shipment/{shipmentId}/download_label_file -- verify access
3. POST /shipment/{shipmentId}/cancel -- create first cancel

## Endpoints

6 endpoints across 2 groups. See references/api-spec.lap for full details.

### shipment
| Method | Path | Description |
|--------|------|-------------|
| POST | /shipment/{shipmentId}/cancel | This method cancels the shipment associated with the specified shipment ID and the associated shipping label is deleted. When you cancel a shipment, the <b>totalShippingCost</b> of the canceled shipment is refunded to the account established by the user's billing agreement.  <br><br>Note that you cannot cancel a shipment if you have used the associated shipping label. |
| POST | /shipment/create_from_shipping_quote | This method creates a shipment based on the <b>shippingQuoteId</b> and <b>rateId</b> values supplied in the request. The rate identified by the <b>rateId</b> value specifies the carrier and service for the package shipment, and the rate ID must be contained in the shipping quote identified by the <b>shippingQuoteId</b> value. Call <b>createShippingQuote</b> to retrieve a set of live shipping rates.<br><br><span class="tablenote"><b>Note:</b> The Logistics API only supports USPS shipping rates and labels.</span><br/>When you create a shipment, eBay generates a shipping label that you can download and use to ship your package.<br/><br/>In a <b>createFromShippingQuote</b> request, sellers can include a list of shipping options they want to add to the base service quoted in the selected rate. The list of available shipping options is specific to each quoted rate and if available, the options are listed in the rate container of the shipping quote.<br/><br/>In addition to a configurable return-to location and other details about the shipment, the response to this method includes:<ul><li>The shipping carrier and service to be used for the package shipment</li><li>A list of selected shipping options, if any</li><li>The shipment tracking number</li><li>The total shipping cost (the sum cost of the base shipping service and any added options)</li></ul>When you create a shipment, your billing agreement account is charged the sum of the <b>baseShippingCost</b> and the total cost of any additional shipping options you might have selected. Use the URL returned in <b>labelDownloadURL</b> field, or call <b>downloadLabelFile</b> with the <b>shipmentId</b> value from the response, to download a shipping label for your package.<br/><br/><div class="msgbox_important"><p class="msgbox_importantInDiv" data-mc-autonum="&lt;b&gt;&lt;span style=&quot;color: #dd1e31;&quot; class=&quot;mcFormatColor&quot;&gt;Important! &lt;/span&gt;&lt;/b&gt;"><span class="autonumber"><span><b><span style="color: #dd1e31;" class="mcFormatColor">Important!</span></b></span></span> Sellers must set up their payment method before they can use this method to create a shipment and the associated shipping label.</p></div><h3 id="ba">Set up a billing agreement</h3>Prior to using this method to create a shipment, sellers must first set up their billing agreement. Failure to do so will return <code>Error 90030 Payment could not be completed.</code><br/><br/>The preferred method for sellers to set up their billing agreement is to go to <a href="https://gslblui.ebay.com/gslblui/payments " target="_blank">Set up billing agreement</a> and follow the on-screen directions.<br/><br/>Alternatively, sellers can do the following:<ul><li>Go to https://www.ebay.com/ship/single/{order_id}, where {order_id} is that of the order for which the label is being printed.</li><li>When prompted, select <b>PayPal</b>.</li><li>Verify that <b>Save PayPal for future purchases</b> is selected.</li><li>Click <b>Set up Payments</b> which will open PayPal in a pop-up window.</li><li>Log in using <i>PayPal credentials</i>, and then follow the on-screen prompts to set up the billing agreement.</li><li>Once the agreement has been set up, sellers can leave this page as there is no need to actually print a label.</li></ul> |
| GET | /shipment/{shipmentId}/download_label_file | This method returns the shipping label file that was generated for the <b>shipmentId</b> value specified in the request. Call <b>createFromShippingQuote</b> to generate a shipment ID.<br><br><span class="tablenote"><b>Note:</b> The Logistics API only supports USPS shipping rates and labels.</span><br>Use the <code>Accept</code> HTTP header to specify the format of the returned file. The default file format is a PDF file. <!-- Are other options available? --> |
| GET | /shipment/{shipmentId} | This method retrieves the shipment details for the specified shipment ID. Call <b>createFromShippingQuote</b> to generate a shipment ID. |

### shipping_quote
| Method | Path | Description |
|--------|------|-------------|
| POST | /shipping_quote | The <b>createShippingQuote</b> method returns a <i>shipping quote </i> that contains a list of live "rates."  <br><br>Each rate represents an offer made by a shipping carrier for a specific service and each offer has a live quote for the base service cost. Rates have a time window in which they are "live," and rates expire when their purchase window ends. If offered by the carrier, rates can include shipping options (and their associated prices), and users can add any offered shipping option to the base service should they desire.  Also, depending on the services required, rates can also include pickup and delivery windows.<br><br><span class="tablenote"><b>Note:</b> The Logistics API only supports USPS shipping rates and labels.</span><br>Each rate is for a single package and is based on the following information: <ul><li>The shipping origin</li> <li>The shipping destination</li> <li>The package size (weight and dimensions)</li></ul>  Rates are identified by a unique eBay-assigned <b>rateId</b> and rates are based on price points, pickup and delivery time frames, and other user requirements. Because each rate offered must be compliant with the eBay shipping program, all rates reflect eBay-negotiated prices.  <br><br>The various rates returned in a shipping quote offer the user a choice from which they can choose a shipping service that best fits their needs. Select the rate for your shipment and using the associated <b>rateId</b>, call <b>createFromShippingQuote</b> to create a shipment and generate a shipping label that you can use to ship the package. |
| GET | /shipping_quote/{shippingQuoteId} | This method retrieves the complete details of the shipping quote associated with the specified <b>shippingQuoteId</b> value.  <br><br>A "shipping quote" pertains to a single specific package and contains a set of shipping "rates" that quote the cost to ship the package by different shipping carriers and services. The quotes are based on the package's origin, destination, and size.  <br><br>Call <b>createShippingQuote</b> to create a <b>shippingQuoteId</b>. |

## Enhanced Skill Content
## Question Mapping

- "How do I get a shipping quote for a package?" -> POST /shipping_quote
- "What shipping rates are available between two addresses?" -> POST /shipping_quote
- "How do I create a shipment from a quote?" -> POST /shipment/create_from_shipping_quote
- "How do I cancel a shipment?" -> POST /shipment/{shipmentId}/cancel
- "Where is my shipment? What's the tracking number?" -> GET /shipment/{shipmentId}
- "How do I download a shipping label?" -> GET /shipment/{shipmentId}/download_label_file
- "What carrier was selected for my shipment?" -> GET /shipment/{shipmentId}
- "When does my shipping quote expire?" -> GET /shipping_quote/{shippingQuoteId}
- "What's the estimated delivery date for my shipment?" -> GET /shipment/{shipmentId}
- "How much did shipping cost?" -> GET /shipment/{shipmentId}
- "What additional shipping options are available?" -> POST /shipping_quote
- "Was my cancellation request accepted?" -> GET /shipment/{shipmentId}
- "How do I ship an eBay order I just sold?" -> POST /shipping_quote + POST /shipment/create_from_shipping_quote
- "Can I customize the label message?" -> POST /shipment/create_from_shipping_quote

## Response Tips

- **Shipment responses**: Deeply nested -- costs live under `rate.baseShippingCost` and `rate.totalShippingCost`; addresses are under `shipFrom.contactAddress`, `shipTo.contactAddress`, and `returnTo.contactAddress`. Check `cancellation.cancellationStatus` for cancel state.
- **Shipping quote responses**: The `rates` field is an array of available options -- iterate to compare carriers, costs, and delivery windows. Check `expirationDate` before using a `rateId`. The `warnings` array may contain important caveats.
- **Label download**: Returns raw file content (not JSON). Set the `Accept` header appropriately (e.g., `application/pdf`). A 200 with empty body may indicate the label is not yet generated.
- **Errors**: 400 = validation failure (bad addresses, missing fields), 404 = invalid shipmentId/quoteId, 409 = conflict (duplicate create or cancel on already-cancelled shipment), 500 = retry-eligible server error.

## Anomaly Flags

- **Quote expiration**: Surface `expirationDate` prominently when retrieving quotes -- an expired quote cannot be used to create a shipment and will return 409.
- **Cancellation status**: After calling cancel, check `cancellation.cancellationStatus` -- a request does not guarantee immediate cancellation. Flag if status is anything other than confirmed.
- **409 Conflict on create**: Indicates the quote was already used or the shipment already exists. Surface this clearly rather than retrying.
- **Missing tracking number**: If `shipmentTrackingNumber` is empty on a created shipment, the label may still be processing. Flag for follow-up.
- **Warnings array**: Shipping quotes may return `warnings` -- always surface these to the user as they may indicate address corrections, restricted items, or service limitations.
- **Cost discrepancy**: Compare `baseShippingCost` vs `totalShippingCost` on the rate object. If they differ significantly, surface `additionalOptions` that contributed to the difference.
- **Marketplace header**: Missing `X-EBAY-C-MARKETPLACE-ID` on create/quote calls will fail with 400. Flag if omitted from request context.

## Playbook

### Ship an eBay Order End-to-End

1. Call `POST /shipping_quote` with the order details, package dimensions/weight, and ship-from/ship-to addresses. Include `X-EBAY-C-MARKETPLACE-ID` header.
2. Review the `rates` array in the response. Compare `totalShippingCost`, `shippingCarrierName`, and `minEstimatedDeliveryDate`/`maxEstimatedDeliveryDate`.
3. Select a rate and note its `rateId` and the `shippingQuoteId`.
4. Call `POST /shipment/create_from_shipping_quote` with the `shippingQuoteId`, `rateId`, optional `labelCustomMessage`, and `labelSize`.
5. From the response, save `shipmentId`, `shipmentTrackingNumber`, and `labelDownloadUrl`.
6. Call `GET /shipment/{shipmentId}/download_label_file` with appropriate `Accept` header to retrieve the printable label.

### Cancel a Shipment

1. Call `POST /shipment/{shipmentId}/cancel` with the shipment ID.
2. Check the response's `cancellation.cancellationStatus` field.
3. If status is not confirmed, call `GET /shipment/{shipmentId}` periodically to poll for updated cancellation state.
4. Handle 409 gracefully -- the shipment may already be cancelled or in a non-cancellable state.

### Compare Shipping Options

1. Call `POST /shipping_quote` with your package and address details.
2. Check `expirationDate` to know how long rates are valid.
3. Iterate through the `rates` array, extracting `shippingCarrierName`, `shippingServiceName`, `totalShippingCost.value`, and delivery date range.
4. Review `additionalOptions` within each rate for available add-ons (insurance, signature, etc.).
5. Surface any entries in the `warnings` array to the user before they decide.

### Retrieve Shipment Details and Label

1. Call `GET /shipment/{shipmentId}` to get full shipment metadata.
2. Extract `shipmentTrackingNumber` for tracking, `rate.shippingCarrierName` for carrier info, and delivery estimates from `rate.minEstimatedDeliveryDate`/`rate.maxEstimatedDeliveryDate`.
3. If a label reprint is needed, call `GET /shipment/{shipmentId}/download_label_file` with `Accept: application/pdf`.

### Verify a Quote Before Creating a Shipment

1. Call `GET /shipping_quote/{shippingQuoteId}` with the saved quote ID.
2. Check `expirationDate` -- if expired, you must create a new quote via `POST /shipping_quote`.
3. Confirm `shipFrom`/`shipTo` addresses are still correct.
4. Review `warnings` for any flagged issues before proceeding to shipment creation.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
