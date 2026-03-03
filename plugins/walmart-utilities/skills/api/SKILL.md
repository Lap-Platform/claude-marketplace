---
name: utilities-management
description: "Utilities Management API skill. Use when working with Utilities Management for utilities. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# Utilities Management

## Auth
ApiKey WM_SEC.ACCESS_TOKEN in header

## Base URL
https://marketplace.walmartapis.com

## Setup
1. Set your API key in the appropriate header
2. GET /v3/utilities/taxonomy -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### utilities
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/utilities/taxonomy | Taxonomy by spec |
| GET | /v3/utilities/taxonomy/departments | All Departments |
| GET | /v3/utilities/taxonomy/departments/{departmentId} | All Categories |
| GET | /v3/utilities/apiStatus | API Platform Status |

## Enhanced Skill Content
## Question Mapping

- "What categories exist in the Walmart marketplace?" -> GET /v3/utilities/taxonomy
- "Show me the full taxonomy for WFS items" -> GET /v3/utilities/taxonomy (feedType=MP_WFS_ITEM)
- "What taxonomy version 4.2 looks like?" -> GET /v3/utilities/taxonomy (version=4.2)
- "List all Walmart departments" -> GET /v3/utilities/taxonomy/departments
- "What categories are under department 5438?" -> GET /v3/utilities/taxonomy/departments/{departmentId}
- "Is the Walmart Marketplace API up right now?" -> GET /v3/utilities/apiStatus
- "Which APIs are currently experiencing issues?" -> GET /v3/utilities/apiStatus
- "What feed types does the taxonomy support?" -> GET /v3/utilities/taxonomy (iterate feedType: item, MP_ITEM, MP_WFS_ITEM, MP_MAINTENANCE)
- "How do I find the right category for my product?" -> GET /v3/utilities/taxonomy/departments then GET /v3/utilities/taxonomy/departments/{departmentId}
- "What's the difference between taxonomy v3.2 and v4.2?" -> GET /v3/utilities/taxonomy (version=3.2) then GET /v3/utilities/taxonomy (version=4.2)
- "Show me the department structure for listing an item" -> GET /v3/utilities/taxonomy (feedType=MP_ITEM)
- "Can I check if the items API is healthy before bulk upload?" -> GET /v3/utilities/apiStatus
- "What subcategories does the Electronics department have?" -> GET /v3/utilities/taxonomy/departments/{departmentId}

## Response Tips

- **Taxonomy endpoints** (`/taxonomy`, `/departments`): Response `payload` is an array of maps - iterate to extract department/category trees. `status` field confirms request success before processing payload.
- **Department detail** (`/departments/{id}`): Response nests categories under `response.category[]` - each category map may contain further nested attributes and attribute groups.
- **API status** (`/apiStatus`): Returns `apiStatuses[]` array (not wrapped in `payload`) - each entry represents a distinct API surface; check individual status fields, not just HTTP 200.

## Anomaly Flags

- **API degradation detected**: Surface immediately when `/apiStatus` returns any entry with a non-healthy status - warn before the user attempts dependent operations.
- **Empty taxonomy payload**: Flag when `/taxonomy` returns `payload: []` for a given feedType/version combination - likely an invalid parameter pairing rather than genuinely empty data.
- **Unknown departmentId**: Surface when `/departments/{id}` returns an error or empty category list - the department may have been restructured or deprecated.
- **Version drift**: Alert when the user is querying an older taxonomy version (3.2) while newer versions (4.2) are available - category structures may have changed.
- **Missing correlation ID pattern**: Warn if the agent detects repeated calls without varying `WM_QOS.CORRELATION_ID` - Walmart may throttle or reject duplicate correlation IDs.
- **Feed type mismatch**: Flag when the user queries taxonomy with feedType=MP_WFS_ITEM but intends to list non-WFS items - wrong taxonomy tree will yield incorrect category assignments.

## Playbook

### 1. Find the Correct Category for a New Product Listing

1. Call `GET /v3/utilities/apiStatus` to confirm APIs are operational.
2. Call `GET /v3/utilities/taxonomy/departments` to retrieve all departments.
3. Identify the relevant department by name from the response `payload[]`.
4. Call `GET /v3/utilities/taxonomy/departments/{departmentId}` with the chosen ID.
5. Browse `response.category[]` to find the most specific matching category for the product.

### 2. Compare Taxonomy Versions Before Migration

1. Call `GET /v3/utilities/taxonomy` with `version=3.2` and note the payload structure.
2. Call `GET /v3/utilities/taxonomy` with `version=4.2` and note the payload structure.
3. Diff the two payloads to identify added, removed, or restructured categories.
4. Update item listings that reference deprecated category paths.

### 3. Pre-flight Health Check Before Bulk Operations

1. Call `GET /v3/utilities/apiStatus` and inspect each entry in `apiStatuses[]`.
2. If all statuses are healthy, proceed with bulk item upload or inventory sync.
3. If any API surface shows degradation, delay the operation and set up a retry loop checking `/apiStatus` at intervals.

### 4. Build a Department-Category Lookup Table

1. Call `GET /v3/utilities/taxonomy/departments` to get the full department list.
2. For each department in `payload[]`, extract the `departmentId`.
3. Call `GET /v3/utilities/taxonomy/departments/{departmentId}` for each ID.
4. Flatten `response.category[]` into a lookup table mapping department name to category names and IDs.
5. Cache the result locally - taxonomy changes infrequently.

### 5. Validate Feed Type Taxonomy for WFS Items

1. Call `GET /v3/utilities/taxonomy` with `feedType=MP_WFS_ITEM` and your target `version`.
2. Confirm the returned `payload[]` contains the expected category tree for fulfillment-eligible items.
3. Cross-reference with `feedType=MP_ITEM` taxonomy to identify categories exclusive to WFS.
4. Use the WFS-specific categories when building item feeds for Walmart Fulfillment Services.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
