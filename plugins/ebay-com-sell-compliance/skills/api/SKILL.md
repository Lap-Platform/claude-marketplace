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

- "What listing violations do I have?" -> GET /listing_violation_summary
- "How many policy violations are in my account?" -> GET /listing_violation_summary
- "Show me a summary of compliance issues for my eBay store" -> GET /listing_violation_summary
- "What types of violations exist on marketplace EBAY_US?" -> GET /listing_violation_summary
- "Do I have any product adoption violations?" -> GET /listing_violation_summary with compliance_type=PRODUCT_ADOPTION
- "Get all listing violations of a specific type" -> GET /listing_violation
- "Which listings are violating eBay's policies?" -> GET /listing_violation
- "Show me detailed HTTPS compliance violations" -> GET /listing_violation with compliance_type=HTTPS
- "Are any of my listings flagged for outside transaction violations?" -> GET /listing_violation with compliance_type=OUTSIDE_TRANSACTION
- "What product-adoption violations exist on EBAY_DE?" -> GET /listing_violation with X-EBAY-C-MARKETPLACE-ID for DE
- "Give me a high-level overview before diving into violation details" -> GET /listing_violation_summary then GET /listing_violation
- "Check if my store is fully compliant" -> GET /listing_violation_summary (look for empty/204 response)
- "How do I fix my listing violations?" -> GET /listing_violation (inspect violation details for remediation info)

## Response Tips

- **Violation summaries**: A 204 means no violations exist for the given marketplace and compliance type -- treat this as a clean bill of health, not an error.
- **Violation listings**: Results are likely paginated; check for `offset`, `limit`, and `total` fields and loop until all pages are consumed.
- **Errors**: 400 indicates invalid parameters (wrong compliance_type or missing marketplace header); 500 is a transient server error worth retrying.
- **Marketplace header**: The `X-EBAY-C-MARKETPLACE-ID` header scopes all results to one marketplace -- responses from different marketplaces are independent.

## Anomaly Flags

- **204 No Content on summary**: Proactively confirm to the user that zero violations were found rather than treating it as an empty error.
- **500 errors**: Surface these immediately and suggest a retry after a short delay; persistent 500s indicate an eBay platform issue.
- **Missing compliance_type on violation detail**: The summary endpoint makes it optional but the detail endpoint requires it -- flag if a user tries to call detail without specifying one.
- **Marketplace mismatch**: If the user switches marketplace IDs between calls in a workflow, warn that results are scoped per marketplace and may not be comparable.
- **High violation counts**: If the summary shows a large number of violations, proactively suggest filtering by compliance_type to make results manageable.
- **OAuth2 token expiry**: Surface auth failures early and prompt for token refresh before retrying the full workflow.

## Playbook

### 1. Full Compliance Audit

1. Call GET /listing_violation_summary with `X-EBAY-C-MARKETPLACE-ID` set to the target marketplace.
2. If 204, report the store is fully compliant -- done.
3. For each compliance_type returned in the summary, call GET /listing_violation with that type.
4. Paginate through all results for each type.
5. Compile a combined report grouped by compliance type with listing IDs and violation details.

### 2. Check a Specific Violation Category

1. Choose the compliance_type (e.g., `PRODUCT_ADOPTION`, `HTTPS`, `OUTSIDE_TRANSACTION`).
2. Call GET /listing_violation_summary with that `compliance_type` to get the count.
3. If violations exist, call GET /listing_violation with the same `compliance_type`.
4. Paginate through results and present listing-level details.

### 3. Multi-Marketplace Compliance Scan

1. Define the list of marketplace IDs to audit (e.g., `EBAY_US`, `EBAY_GB`, `EBAY_DE`).
2. For each marketplace, call GET /listing_violation_summary with the corresponding `X-EBAY-C-MARKETPLACE-ID`.
3. Collect and compare violation counts across marketplaces.
4. For any marketplace with violations, drill into GET /listing_violation per compliance type.
5. Present a cross-marketplace summary highlighting which regions need attention.

### 4. Monitor for New Violations

1. Call GET /listing_violation_summary and record current violation counts per type.
2. On the next check, call the summary again and compare counts to the previous snapshot.
3. If any count increased, call GET /listing_violation for the affected type to identify new entries.
4. Surface newly flagged listings to the user with actionable detail.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
