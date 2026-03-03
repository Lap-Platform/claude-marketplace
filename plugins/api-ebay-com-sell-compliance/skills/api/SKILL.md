---
name: compliance-api
description: "Compliance API skill. Use when working with Compliance for listing_violation_summary, listing_violation. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# Compliance API
API version: 1.4.4

## Auth
OAuth2

## Base URL
https://api.ebay.com{basePath}

## Setup
1. Configure auth: OAuth2
2. GET /listing_violation_summary -- verify access

## Endpoints

2 endpoints across 2 groups. See references/api-spec.lap for full details.

### listing_violation_summary
| Method | Path | Description |
|--------|------|-------------|
| GET | /listing_violation_summary | This call returns listing violation counts for a seller. A user can pass in one or more compliance types through the <strong>compliance_type</strong> query parameter. See <a href="/api-docs/sell/compliance/types/com:ComplianceTypeEnum">ComplianceTypeEnum</a> for more information on the supported listing compliance types. Listing violations are returned for multiple marketplaces if the seller sells on multiple eBay marketplaces.<br /><br /> <span class="tablenote"><strong>Note:</strong> Only a canned response, with counts for all listing compliance types, is returned in the Sandbox environment. Due to this limitation, the <strong>compliance_type</strong> query parameter (if used) will not have an effect on the response. </span> |

### listing_violation
| Method | Path | Description |
|--------|------|-------------|
| GET | /listing_violation | This call returns specific listing violations for the supported listing compliance types. Only one compliance type can be passed in per call, and the response will include all the listing violations for this compliance type, and listing violations are grouped together by eBay listing ID. See <a href="/api-docs/sell/compliance/types/com:ComplianceTypeEnum">ComplianceTypeEnum</a> for more information on the supported listing compliance types. This method also has pagination control. <br /><br /> <span class="tablenote"><strong>Note:</strong> A maximum of 2000 listing violations will be returned in a result set. If the seller has more than 2000 listing violations, some/all of those listing violations must be corrected before additional listing violations will be retrieved. The user should pay attention to the <strong>total</strong> value in the response. If this value is '2000', it is possible that the seller has more than 2000 listing violations, but this field maxes out at 2000. </span> <br /><span class="tablenote"><strong>Note:</strong> In a future release of this API, the seller will be able to pass in a specific eBay listing ID as a query parameter to see if this specific listing has any violations. </span><br /> <span class="tablenote"><strong>Note:</strong> Only mocked non-compliant listing data will be returned for this call in the Sandbox environment, and not specific to the seller. However, the user can still use this mock data to experiment with the compliance type filters and pagination control.</span> |

## Enhanced Skill Content
## Question Mapping

- "What listing violations do I have?" -> GET /listing_violation
- "Show me a summary of my compliance issues" -> GET /listing_violation_summary
- "Are any of my listings non-compliant?" -> GET /listing_violation_summary
- "What product safety violations exist in my store?" -> GET /listing_violation with compliance_type=PRODUCT_SAFETY
- "Do I have any listing policy violations on EBAY_US?" -> GET /listing_violation with X-EBAY-C-MARKETPLACE-ID for US
- "How many violations do I have by type?" -> GET /listing_violation_summary
- "Show me all violations for a specific compliance type" -> GET /listing_violation
- "Is my account in good compliance standing?" -> GET /listing_violation_summary (check for 204 No Content)
- "What do I need to fix on my listings?" -> GET /listing_violation then review each violation
- "Are there violations on my UK marketplace listings?" -> GET /listing_violation with X-EBAY-C-MARKETPLACE-ID set to EBAY_GB
- "Give me a breakdown of violation counts" -> GET /listing_violation_summary with no compliance_type filter
- "Which listings are flagged for a specific policy?" -> GET /listing_violation with the relevant compliance_type
- "Do I have any violations at all?" -> GET /listing_violation_summary (204 means none, 200 means some)

## Response Tips

- **Violation summaries**: A 204 response means zero violations -- no body is returned. A 200 contains counts grouped by compliance type.
- **Violation details**: Results may be paginated; check for `offset`, `limit`, and `total` fields and follow-up with pagination params to retrieve all records.
- **Errors**: A 400 typically means an invalid compliance_type value or missing required header. A 500 is a server-side issue -- retry with backoff.
- **Headers**: The `X-EBAY-C-MARKETPLACE-ID` header scopes all results to a single marketplace; omitting it or using an invalid value returns a 400.

## Anomaly Flags

- **204 No Content on summary**: Surface this clearly -- it means no violations exist, not an error.
- **500 errors**: Flag server-side failures and suggest retrying after a short delay.
- **High violation counts**: If the summary shows a large number of violations for any compliance type, proactively warn the seller.
- **Missing marketplace header**: If a 400 is returned, check whether `X-EBAY-C-MARKETPLACE-ID` was included -- this is the most common mistake.
- **OAuth2 token expiry**: If requests start failing with 401/403, surface that the OAuth2 token likely needs refreshing before retrying.
- **Unexpected compliance types**: If the API returns violation types not previously seen, flag them as potentially new policy categories.

## Playbook

### 1. Check Overall Compliance Health

1. Call `GET /listing_violation_summary` with `X-EBAY-C-MARKETPLACE-ID` set to your target marketplace.
2. If the response is **204**, you have no violations -- you are in good standing.
3. If the response is **200**, review the counts per compliance type.
4. For any type with a non-zero count, proceed to Playbook 2.

### 2. Investigate Violations by Type

1. Pick a `compliance_type` from the summary results.
2. Call `GET /listing_violation` with both `X-EBAY-C-MARKETPLACE-ID` and the chosen `compliance_type`.
3. Review each violation entry for the affected listing ID and reason.
4. If results are paginated, increment the offset and repeat until all violations are retrieved.
5. Compile the list of affected listings for remediation.

### 3. Multi-Marketplace Compliance Audit

1. Identify all marketplaces you sell on (e.g., EBAY_US, EBAY_GB, EBAY_DE).
2. For each marketplace, call `GET /listing_violation_summary` with the corresponding `X-EBAY-C-MARKETPLACE-ID`.
3. Collect and compare violation counts across marketplaces.
4. Prioritize the marketplace with the highest violation count.
5. Drill into specific violations using `GET /listing_violation` for each marketplace and compliance type.

### 4. Resolve and Verify Fixes

1. Use `GET /listing_violation` to get the full list of violations for a compliance type.
2. For each violation, note the listing ID and the specific issue described.
3. Fix the listing through the eBay selling flow or Inventory API.
4. After fixes are applied, re-call `GET /listing_violation` with the same parameters.
5. Confirm the violation count has decreased. Repeat until the summary returns **204**.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
