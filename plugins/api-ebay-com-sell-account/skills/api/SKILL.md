---
name: account-v1-api
description: "Account v1 API skill. Use when working with Account v1 for custom_policy, fulfillment_policy, payment_policy. Covers 37 endpoints."
version: 1.0.0
generator: lapsh
---

# Account v1 API
API version: v1.9.3

## Auth
OAuth2

## Base URL
https://api.ebay.com{basePath}

## Setup
1. Configure auth: OAuth2
2. GET /custom_policy/ -- verify access
3. POST /custom_policy/ -- create first custom_policy

## Endpoints

37 endpoints across 13 groups. See references/api-spec.lap for full details.

### custom_policy
| Method | Path | Description |
|--------|------|-------------|
| GET | /custom_policy/ | This method retrieves the list of custom policies defined for a seller's account. To limit the returned custom policies, specify the <b>policy_types</b> query parameter. |
| POST | /custom_policy/ | This method creates a new custom policy that specifies the seller's terms for complying with local governmental regulations. Each Custom Policy targets a <b>policyType</b>. Multiple policies may be created as using the following custom policy types:<ul><li>PRODUCT_COMPLIANCE: Product Compliance policies disclose product information as required for regulatory compliance. <br/><br/><span class="tablenote"><strong>Note:</strong> A maximum of 60 Product Compliance policies per seller may be created.</span></li><li>TAKE_BACK: Takeback policies describe the seller's legal obligation to take back a previously purchased item when the buyer purchases a new one. <br/><br/><span class="tablenote"><strong>Note:</strong> A maximum of 18 Takeback policies per seller may be created.</span></li></ul>A successful create policy call returns an HTTP status code of <b>201 Created</b> with the system-generated policy ID included in the Location response header. |
| GET | /custom_policy/{custom_policy_id} | This method retrieves the custom policy specified by the <b>custom_policy_id</b> path parameter. |
| PUT | /custom_policy/{custom_policy_id} | This method updates an existing custom policy specified by the <b>custom_policy_id</b> path parameter. Since this method overwrites the policy's <b>name</b>, <b>label</b>, and <b>description</b> fields, always include the complete and current text of all three policy fields in the request payload, even if they are not being updated.<br/> <br/>For example, the value for the <b>label</b> field is to be updated, but the <b>name</b> and <b>description</b> values will remain unchanged. The existing <b>name</b> and <b>description</b> values, as they are defined in the current policy, must also be passed in. <br/><br/>A successful policy update call returns an HTTP status code of <b>204 No Content</b>. |

### fulfillment_policy
| Method | Path | Description |
|--------|------|-------------|
| POST | /fulfillment_policy/ | This method creates a new fulfillment policy for an eBay marketplace where the policy encapsulates seller's terms for fulfilling item purchases. Fulfillment policies include the shipment options that the seller offers to buyers.  <br><br>A successful request returns the <b>getFulfillmentPolicy</b> URI to the new policy in the <b>Location</b> response header and the ID for the new policy is returned in the response payload.  <p class="tablenote"><b>Tip:</b> For details on creating and using the business policies supported by the Account API, see <a href="/api-docs/sell/static/seller-accounts/business-policies.html">eBay business policies</a>.</p> |
| GET | /fulfillment_policy/{fulfillmentPolicyId} | This method retrieves the complete details of a fulfillment policy. Supply the ID of the policy you want to retrieve using the <b>fulfillmentPolicyId</b> path parameter. |
| PUT | /fulfillment_policy/{fulfillmentPolicyId} | This method updates an existing fulfillment policy. Specify the policy you want to update using the <b>fulfillment_policy_id</b> path parameter. Supply a complete policy payload with the updates you want to make; this call overwrites the existing policy with the new details specified in the payload. |
| DELETE | /fulfillment_policy/{fulfillmentPolicyId} | This method deletes a fulfillment policy. Supply the ID of the policy you want to delete in the <b>fulfillmentPolicyId</b> path parameter. |
| GET | /fulfillment_policy | This method retrieves all the fulfillment policies configured for the marketplace you specify using the <code>marketplace_id</code> query parameter. |
| GET | /fulfillment_policy/get_by_policy_name | This method retrieves the details for a specific fulfillment policy. In the request, supply both the policy <code>name</code> and its associated <code>marketplace_id</code> as query parameters. |

### payment_policy
| Method | Path | Description |
|--------|------|-------------|
| GET | /payment_policy | This method retrieves all the payment business policies configured for the marketplace you specify using the <code>marketplace_id</code> query parameter. |
| POST | /payment_policy | This method creates a new payment policy where the policy encapsulates seller's terms for order payments. <br><br>A successful request returns the <b>getPaymentPolicy</b> URI to the new policy in the <b>Location</b> response header and the ID for the new policy is returned in the response payload.  <p class="tablenote"><b>Tip:</b> For details on creating and using the business policies supported by the Account API, see <a href="/api-docs/sell/static/seller-accounts/business-policies.html">eBay business policies</a>.</p> |
| GET | /payment_policy/{payment_policy_id} | This method retrieves the complete details of a payment policy. Supply the ID of the policy you want to retrieve using the <b>paymentPolicyId</b> path parameter. |
| PUT | /payment_policy/{payment_policy_id} | This method updates an existing payment policy. Specify the policy you want to update using the <b>payment_policy_id</b> path parameter. Supply a complete policy payload with the updates you want to make; this call overwrites the existing policy with the new details specified in the payload. |
| DELETE | /payment_policy/{payment_policy_id} | This method deletes a payment policy. Supply the ID of the policy you want to delete in the <b>paymentPolicyId</b> path parameter. |
| GET | /payment_policy/get_by_policy_name | This method retrieves the details of a specific payment policy. Supply both the policy <code>name</code> and its associated <code>marketplace_id</code> in the request query parameters. |

### payments_program
| Method | Path | Description |
|--------|------|-------------|
| GET | /payments_program/{marketplace_id}/{payments_program_type} | <span class="tablenote"><b>Note:</b> This method is no longer applicable, as all seller accounts globally have been enabled for the new eBay payment and checkout flow.</span><br>This method returns whether or not the user is opted-in to the specified payments program. Sellers opt-in to payments programs by marketplace and you use the <b>marketplace_id</b> path parameter to specify the marketplace of the status flag you want returned. |
| GET | /payments_program/{marketplace_id}/{payments_program_type}/onboarding | <span class="tablenote"><b>Note:</b> This method is no longer applicable, as all seller accounts globally have been enabled for the new eBay payment and checkout flow.</span><br>This method retrieves a seller's onboarding status for a payments program for a specified marketplace. The overall onboarding status of the seller and the status of each onboarding step is returned. |

### privilege
| Method | Path | Description |
|--------|------|-------------|
| GET | /privilege | This method retrieves the seller's current set of privileges, including whether or not the seller's eBay registration has been completed, as well as the details of their site-wide <b>sellingLimit</b> (the amount and quantity they can sell on a given day). |

### program
| Method | Path | Description |
|--------|------|-------------|
| GET | /program/get_opted_in_programs | This method gets a list of the seller programs that the seller has opted-in to. |
| POST | /program/opt_in | This method opts the seller in to an eBay seller program. Refer to the <a href="/api-docs/sell/account/overview.html#opt-in" target="_blank">Account API overview</a> for information about available eBay seller programs.<br><br><span class="tablenote"><b>Note:</b> It can take up to 24-hours for eBay to process your request to opt-in to a Seller Program. Use the <a href="/api-docs/sell/account/resources/program/methods/getOptedInPrograms" target="_blank">getOptedInPrograms</a> call to check the status of your request after the processing period has passed.</span> |
| POST | /program/opt_out | This method opts the seller out of a seller program in which they are currently opted in to. A seller can retrieve a list of the seller programs they are opted-in to using the <b>getOptedInPrograms</b> method. |

### rate_table
| Method | Path | Description |
|--------|------|-------------|
| GET | /rate_table | This method retrieves a seller's <i>shipping rate tables</i> for the country specified in the <b>country_code</b> query parameter. If you call this method without specifying a country code, the call returns all of the seller's shipping rate tables.  <br><br>The method's response includes a <b>rateTableId</b> for each table defined by the seller. This <b>rateTableId</b> value is used in add/revise item call or in create/update fulfillment business policy call to specify the shipping rate table to use for that policy's domestic or international shipping options. <br><br>This call currently supports getting rate tables related to the following marketplaces: United States, Canada, United Kingdom, Germany, Australia, France, Italy, and Spain.  <span class="tablenote"><b>Note:</b> Rate tables created with the Trading API might not have been assigned a <b>rateTableId</b> at the time of their creation. This method can assign and return <b>rateTableId</b> values for rate tables with missing IDs if you make a request using the <b>country_code</b> where the seller has defined rate tables.</span>  <br><br>Sellers can define up to 40 shipping rate tables for their account, which lets them set up different rate tables for each of the marketplaces they sell into. Go to <a href="https://www.ebay.com/ship/rt ">Shipping rate tables</a> in  <b>My eBay</b> to create and update rate tables. |

### return_policy
| Method | Path | Description |
|--------|------|-------------|
| GET | /return_policy | This method retrieves all the return policies configured for the marketplace you specify using the <code>marketplace_id</code> query parameter. |
| POST | /return_policy | This method creates a new return policy where the policy encapsulates seller's terms for returning items.  <br><br>Each policy targets a specific marketplace, and you can create multiple policies for each marketplace. Return policies are not applicable to motor-vehicle listings.<br><br>A successful request returns the <b>getReturnPolicy</b> URI to the new policy in the <b>Location</b> response header and the ID for the new policy is returned in the response payload.  <p class="tablenote"><b>Tip:</b> For details on creating and using the business policies supported by the Account API, see <a href="/api-docs/sell/static/seller-accounts/business-policies.html">eBay business policies</a>.</p> |
| GET | /return_policy/{return_policy_id} | This method retrieves the complete details of the return policy specified by the <b>returnPolicyId</b> path parameter. |
| PUT | /return_policy/{return_policy_id} | This method updates an existing return policy. Specify the policy you want to update using the <b>return_policy_id</b> path parameter. Supply a complete policy payload with the updates you want to make; this call overwrites the existing policy with the new details specified in the payload. |
| DELETE | /return_policy/{return_policy_id} | This method deletes a return policy. Supply the ID of the policy you want to delete in the <b>returnPolicyId</b> path parameter. |
| GET | /return_policy/get_by_policy_name | This method retrieves the details of a specific return policy. Supply both the policy <code>name</code> and its associated <code>marketplace_id</code> in the request query parameters. |

### bulk_create_or_replace_sales_tax
| Method | Path | Description |
|--------|------|-------------|
| POST | /bulk_create_or_replace_sales_tax | This method creates or updates multiple sales-tax table entries.<br><br><i>Sales-tax tables</i> can be set up for countries that support different <i>tax jurisdictions</i>.<br><br><span class="tablenote"><b>Note:</b> Sales-tax tables are only available for the US (EBAY_US) and Canada (EBAY_CA) marketplaces.</span><br>Each sales-tax table entry comprises the following parameters:<ul><li><code>countryCode</code></li><li><code>jurisdictionId</code></li><li><code>salesTaxPercentage</code></li><li><code>shippingAndHandlingTaxed</code></li></ul><br>Valid jurisdiction IDs are retrieved using <b><a href="/api-docs/sell/metadata/resources/country/methods/getSalesTaxJurisdictions" target="_blank">getSalesTaxJurisdictions</a></b> in the Metadata API.<br><br>For details about using this call, refer to <a href="/api-docs/sell/static/seller-accounts/tax-tables.html">Establishing sales-tax tables</a>.<br><br><div class="msgbox_important"><p class="msgbox_importantInDiv" data-mc-autonum="&lt;b&gt;&lt;span style=&quot;color: #dd1e31;&quot; class=&quot;mcFormatColor&quot;&gt;Important! &lt;/span&gt;&lt;/b&gt;"><span class="autonumber"><span><b><span style="color: #dd1e31;" class="mcFormatColor">Important!</span></b></span></span> In the US, eBay now calculates, collects, and remits sales tax to the proper taxing authorities in all 50 states and Washington, DC. Sellers can no longer specify sales-tax rates for these jurisdictions using a tax table.<br><br>However, sellers may continue to use a sales-tax table to set rates for the following US territories:<ul><li>American Samoa (AS)</li><li>Guam (GU)</li><li>Northern Mariana Islands (MP)</li><li>Palau (PW)</li><li>US Virgin Islands (VI)</li></ul>For additional information, refer to <a href="https://www.ebay.com/help/selling/fees-credits-invoices/taxes-import-charges?id=4121 " target="_blank">Taxes and import charges</a>.</p></div> |

### sales_tax
| Method | Path | Description |
|--------|------|-------------|
| GET | /sales_tax/{countryCode}/{jurisdictionId} | This call retrieves the current sales-tax table entry for a specific tax jurisdiction. Specify the jurisdiction to retrieve using the <b>countryCode</b> and <b>jurisdictionId</b> path parameters. All four response fields will be returned if a sales-tax entry exists for the tax jurisdiction. Otherwise, the response will be returned as empty.<br><br><span class="tablenote"><b>Note:</b> Sales-tax tables are only available for the US (EBAY_US) and Canada (EBAY_CA) marketplaces.</span><br><div class="msgbox_important"><p class="msgbox_importantInDiv" data-mc-autonum="&lt;b&gt;&lt;span style=&quot;color: #dd1e31;&quot; class=&quot;mcFormatColor&quot;&gt;Important! &lt;/span&gt;&lt;/b&gt;"><span class="autonumber"><span><b><span style="color: #dd1e31;" class="mcFormatColor">Important!</span></b></span></span> In the US, eBay now calculates, collects, and remits sales tax to the proper taxing authorities in all 50 states and Washington, DC. Sellers can no longer specify sales-tax rates for these jurisdictions using a tax table.<br><br>However, sellers may continue to use a sales-tax table to set rates for the following US territories:<ul><li>American Samoa (AS)</li><li>Guam (GU)</li><li>Northern Mariana Islands (MP)</li><li>Palau (PW)</li><li>US Virgin Islands (VI)</li></ul>For additional information, refer to <a href="https://www.ebay.com/help/selling/fees-credits-invoices/taxes-import-charges?id=4121 " target="_blank">Taxes and import charges</a>.</p></div> |
| PUT | /sales_tax/{countryCode}/{jurisdictionId} | This method creates or updates a sales-tax table entry for a jurisdiction. Specify the tax table entry you want to configure using the two path parameters: <b>countryCode</b> and <b>jurisdictionId</b>.  <br><br>A tax table entry for a jurisdiction is comprised of two fields: one for the jurisdiction's sales-tax rate and another that's a boolean value indicating whether or not shipping and handling are taxed in the jurisdiction.<br><br>You can set up <i>sales-tax tables</i> for countries that support different <i>tax jurisdictions</i>.<br><br><span class="tablenote"><b>Note:</b> Sales-tax tables are only available for the US (EBAY_US) and Canada (EBAY_CA) marketplaces.</span><br>Retrieve valid jurisdiction IDs using <b><a href="/api-docs/sell/metadata/resources/country/methods/getSalesTaxJurisdictions" target="_blank">getSalesTaxJurisdictions</a></b> in the Metadata API.<br><br>For details about using this call, refer to <a href="/api-docs/sell/static/seller-accounts/tax-tables.html">Establishing sales-tax tables</a>.<br><br><div class="msgbox_important"><p class="msgbox_importantInDiv" data-mc-autonum="&lt;b&gt;&lt;span style=&quot;color: #dd1e31;&quot; class=&quot;mcFormatColor&quot;&gt;Important! &lt;/span&gt;&lt;/b&gt;"><span class="autonumber"><span><b><span style="color: #dd1e31;" class="mcFormatColor">Important!</span></b></span></span> In the US, eBay now calculates, collects, and remits sales tax to the proper taxing authorities in all 50 states and Washington, DC. Sellers can no longer specify sales-tax rates for these jurisdictions using a tax table.<br><br>However, sellers may continue to use a sales-tax table to set rates for the following US territories:<ul><li>American Samoa (AS)</li><li>Guam (GU)</li><li>Northern Mariana Islands (MP)</li><li>Palau (PW)</li><li>US Virgin Islands (VI)</li></ul>For additional information, refer to <a href="https://www.ebay.com/help/selling/fees-credits-invoices/taxes-import-charges?id=4121 " target="_blank">Taxes and import charges</a>.</p></div> |
| DELETE | /sales_tax/{countryCode}/{jurisdictionId} | This call deletes a sales-tax table entry for a jurisdiction. Specify the jurisdiction to delete using the <b>countryCode</b> and <b>jurisdictionId</b> path parameters.<br><br><span class="tablenote"><b>Note:</b> Sales-tax tables are only available for the US (EBAY_US) and Canada (EBAY_CA) marketplaces.</span> |
| GET | /sales_tax | Use this call to retrieve all sales tax table entries that the seller has defined for a specific country. All four response fields will be returned for each tax jurisdiction that matches the search criteria. If no sales tax rates are defined for the specified, a <code>204 No Content</code> status code is returned with no response payload.<br><br><span class="tablenote"><b>Note:</b> Sales-tax tables are only available for the US (EBAY_US) and Canada (EBAY_CA) marketplaces.</span><br><div class="msgbox_important"><p class="msgbox_importantInDiv" data-mc-autonum="&lt;b&gt;&lt;span style=&quot;color: #dd1e31;&quot; class=&quot;mcFormatColor&quot;&gt;Important! &lt;/span&gt;&lt;/b&gt;"><span class="autonumber"><span><b><span style="color: #dd1e31;" class="mcFormatColor">Important!</span></b></span></span> In the US, eBay now calculates, collects, and remits sales tax to the proper taxing authorities in all 50 states and Washington, DC. Sellers can no longer specify sales-tax rates for these jurisdictions using a tax table.<br><br>However, sellers may continue to use a sales-tax table to set rates for the following US territories:<ul><li>American Samoa (AS)</li><li>Guam (GU)</li><li>Northern Mariana Islands (MP)</li><li>Palau (PW)</li><li>US Virgin Islands (VI)</li></ul>For additional information, refer to <a href="https://www.ebay.com/help/selling/fees-credits-invoices/taxes-import-charges?id=4121 " target="_blank">Taxes and import charges</a>.</p></div> |

### subscription
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscription | This method retrieves a list of subscriptions associated with the seller account. |

### kyc
| Method | Path | Description |
|--------|------|-------------|
| GET | /kyc | <span class="tablenote"><b>Note:</b> This method was originally created to see which onboarding requirements were still pending for sellers being onboarded for eBay managed payments, but now that all seller accounts are onboarded globally, this method should now just return an empty payload with a <code>204 No Content</code> HTTP status code. </span> |

### advertising_eligibility
| Method | Path | Description |
|--------|------|-------------|
| GET | /advertising_eligibility | This method allows developers to check the seller eligibility status for eBay advertising programs. |

## Enhanced Skill Content
## Question Mapping

- "What are my current fulfillment policies?" -> GET /fulfillment_policy
- "How do I create a new return policy for my eBay store?" -> POST /return_policy
- "What payment methods are configured for marketplace EBAY_US?" -> GET /payment_policy
- "Can I look up a fulfillment policy by its name?" -> GET /fulfillment_policy/get_by_policy_name
- "What are my selling limits and privileges?" -> GET /privilege
- "Am I enrolled in eBay's managed payments program?" -> GET /payments_program/{marketplace_id}/{payments_program_type}
- "How do I opt into an eBay seller program?" -> POST /program/opt_in
- "What sales tax rates do I have set for the US?" -> GET /sales_tax
- "How do I bulk-update sales tax across multiple jurisdictions?" -> POST /bulk_create_or_replace_sales_tax
- "What shipping rate tables are available for my country?" -> GET /rate_table
- "How do I delete a payment policy I no longer need?" -> DELETE /payment_policy/{payment_policy_id}
- "What custom policies do I have?" -> GET /custom_policy/
- "Is my account eligible for eBay advertising?" -> GET /advertising_eligibility
- "What are the onboarding steps for managed payments?" -> GET /payments_program/{marketplace_id}/{payments_program_type}/onboarding
- "What subscriptions does my account have?" -> GET /subscription

## Response Tips

- **Policy lists** (fulfillment, payment, return, custom): Paginated with `href`, `next`, `prev`, `offset`, `limit`, `total`. Follow `next` for additional pages. The policy array is nested under a plural key (e.g., `fulfillmentPolicies`, `paymentPolicies`).
- **Single policy GETs**: Return the full policy object directly (no wrapper). Check for nested maps like `shippingOptions[].shippingServices[]` or `deposit.paymentMethods[]` which contain further nested objects.
- **Policy creates/updates**: 201 (create) and 200 (update) responses may include a `warnings` array -- always surface these to the user even on success.
- **Deletes**: Return 204 with no body. A 409 error means the policy is in use and cannot be deleted.
- **Bulk sales tax**: May return 200 (all succeeded) or 207 (partial success) -- inspect `updatedSalesTaxEntries` for per-item status on 207.
- **Privilege/KYC/Subscription**: Flat response structures. KYC may return 204 (no checks needed) which is a success, not an error.
- **Programs**: `get_opted_in_programs` returns a `programs` array; opt-in/opt-out return 200 with no body on success.

## Anomaly Flags

- **409 Conflict on delete**: Policy is actively referenced by listings. Surface this clearly -- user must reassign listings before deleting.
- **207 Multi-Status on bulk sales tax**: Partial failure. Parse each entry in the response and flag which jurisdictions failed.
- **Warnings array in create/update responses**: These indicate non-blocking issues (e.g., deprecated payment methods, region restrictions). Always display to user.
- **KYC 204 vs 200**: A 204 means no KYC action needed; a 200 with `kycChecks` means the seller has outstanding verification requirements -- flag urgently.
- **`wasPreviouslyOptedIn: true` in payments program**: Seller was previously enrolled but left. Re-enrollment may have different terms.
- **`sellingLimit` approaching zero**: If `quantity` or `amount.value` is low in the privilege response, warn the seller they are near their limit.
- **500 errors**: eBay internal errors. Suggest retry with backoff; do not retry mutating operations (POST/PUT/DELETE) without user confirmation.
- **Missing `marketplaceId` on policy calls**: Most list endpoints require `marketplace_id` as a query param. Omitting it returns 400 -- prompt the user for their target marketplace.

## Playbook

### 1. Set Up a New Marketplace (Full Policy Suite)

1. Call `GET /privilege` to confirm the account has selling privileges and note the selling limits.
2. Create a fulfillment policy: `POST /fulfillment_policy` with shipping options, handling time, and marketplace ID.
3. Create a payment policy: `POST /payment_policy` with payment methods and marketplace ID.
4. Create a return policy: `POST /return_policy` with return period, refund method, and return shipping payer.
5. Optionally create custom policies: `POST /custom_policy/` for product compliance or take-back policies.
6. Review each response's `warnings` array and address any flagged issues.

### 2. Configure Sales Tax for Multiple States

1. Build a list of jurisdiction entries with `countryCode`, `salesTaxJurisdictionId`, `salesTaxPercentage`, and `shippingAndHandlingTaxed`.
2. Call `POST /bulk_create_or_replace_sales_tax` with the full list.
3. If the response is 207, parse `updatedSalesTaxEntries` to identify failures and fix invalid jurisdiction IDs.
4. Verify with `GET /sales_tax?country_code=US` to confirm all entries are applied.

### 3. Enroll in eBay Programs

1. Call `GET /program/get_opted_in_programs` to see current enrollments.
2. Call `GET /payments_program/{marketplace_id}/EBAY_PAYMENTS/onboarding` to check onboarding status and required steps.
3. If steps are complete, call `POST /program/opt_in` with the desired `programType`.
4. On 409 conflict, the seller may already be enrolled or ineligible -- check the error message.
5. Confirm enrollment by calling `GET /program/get_opted_in_programs` again.

### 4. Audit and Clean Up Policies

1. List all policies per type: `GET /fulfillment_policy`, `GET /payment_policy`, `GET /return_policy` for the target marketplace.
2. Identify unused or duplicate policies by name and description.
3. Attempt `DELETE /fulfillment_policy/{id}` (or payment/return equivalent) for each unused policy.
4. If a 409 is returned, the policy is still attached to active listings -- skip it or reassign listings first.
5. Verify cleanup with a fresh list call and confirm `total` has decreased.

### 5. Check Account Health and Compliance

1. Call `GET /privilege` to verify selling limits and registration status.
2. Call `GET /kyc` -- if 200 with `kycChecks`, review each check's details and complete required verification.
3. Call `GET /advertising_eligibility` with the marketplace header to see which ad programs are available.
4. Call `GET /subscription` to review active subscription tiers and their limits.
5. Surface any KYC issues or low selling limits as action items for the seller.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
