---
name: compliance-api
description: "Compliance API skill. Use when working with Compliance for listing_violation_summary, listing_violation. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# Compliance API
API version: 1.4.3

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
- "Are any of my listings violating eBay policies?" -> GET /listing_violation_summary
- "What product adoption violations exist in my account?" -> GET /listing_violation with compliance_type=PRODUCT_ADOPTION
- "Do I have any listing violations on the UK marketplace?" -> GET /listing_violation with X-EBAY-C-MARKETPLACE-ID=EBAY_GB
- "How many total violations do I have by type?" -> GET /listing_violation_summary
- "Show me all HTTPS violations for my listings" -> GET /listing_violation with compliance_type=HTTPS
- "Which of my listings have policy violations on ebay.de?" -> GET /listing_violation with X-EBAY-C-MARKETPLACE-ID=EBAY_DE
- "Give me a breakdown of violation counts before I dig into details" -> GET /listing_violation_summary then GET /listing_violation
- "Are there any compliance issues I should fix right now?" -> GET /listing_violation_summary followed by GET /listing_violation for non-zero types
- "Check if my store has outside-payment-policy violations" -> GET /listing_violation with compliance_type=OUTSIDE_PAYMENT_POLICY
- "What does my compliance health look like across all violation types?" -> GET /listing_violation_summary without compliance_type filter

## Response Tips

- **Violation summaries**: 200 returns violation counts grouped by compliance_type; 204 means no violations found (empty body, not an error -- this is good news).
- **Violation details**: Response likely contains nested listing objects with violation metadata; expect arrays of violations per listing with specifics on what rule was broken.
- **Errors**: 400 indicates bad input (invalid marketplace ID or compliance_type); 500 is a server-side eBay issue -- retry after a short delay.
- **Headers**: Always include `X-EBAY-C-MARKETPLACE-ID` -- omitting it produces a 400, not a default fallback.

## Anomaly Flags

- **204 on summary**: Proactively confirm to the user that no violations were found -- don't treat empty response as an error.
- **High violation counts**: If summary shows a spike in any compliance_type, flag it as needing urgent attention before eBay takes enforcement action.
- **500 errors**: Surface eBay service instability and suggest retrying; do not retry silently more than twice.
- **Unknown compliance_type values**: If the API returns violation types not in the known set (PRODUCT_ADOPTION, HTTPS, OUTSIDE_PAYMENT_POLICY), flag them as potentially new policy categories the seller should review.
- **Marketplace mismatch**: If the user asks about one marketplace but results seem sparse, suggest checking if they meant a different marketplace ID.

## Playbook

### 1. Full Compliance Health Check

1. Call GET /listing_violation_summary with the target marketplace header to get counts by type.
2. If 204, report all clear -- no violations found.
3. For each compliance_type with violations, call GET /listing_violation with that type to get details.
4. Summarize total violations, list affected listings, and prioritize by severity.

### 2. Investigate a Specific Violation Type

1. Identify the compliance_type of interest (e.g., PRODUCT_ADOPTION, HTTPS).
2. Call GET /listing_violation with `compliance_type` set and the correct marketplace header.
3. Review each violated listing and note the specific rule or field causing the issue.
4. Provide actionable fix recommendations for each violation.

### 3. Multi-Marketplace Compliance Audit

1. Determine which marketplaces the seller operates on (e.g., EBAY_US, EBAY_GB, EBAY_DE).
2. For each marketplace, call GET /listing_violation_summary.
3. Compare violation counts across marketplaces to identify region-specific issues.
4. Drill into GET /listing_violation for any marketplace showing elevated counts.
5. Produce a consolidated report with per-marketplace breakdown.

### 4. Monitor Compliance Over Time

1. Call GET /listing_violation_summary and record current violation counts.
2. After the seller makes fixes, re-call the summary endpoint.
3. Compare before/after counts to confirm violations were resolved.
4. If counts increased, call GET /listing_violation to identify new violations introduced.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
