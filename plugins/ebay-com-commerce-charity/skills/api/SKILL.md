---
name: charity-api
description: "Charity API skill. Use when working with Charity for charity_org. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# Charity API
API version: v1.2.1

## Auth
OAuth2

## Base URL
https://api.ebay.com{basePath}

## Setup
1. Configure auth: OAuth2
2. GET /charity_org -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### charity_org
| Method | Path | Description |
|--------|------|-------------|
| GET | /charity_org/{charity_org_id} | This call is used to retrieve detailed information about supported charitable organizations. It allows users to retrieve the details for a specific charitable organization using its charity organization ID. |
| GET | /charity_org | This call is used to search for supported charitable organizations. It allows users to search for a specific charitable organization, or for multiple charitable organizations, from a particular charitable domain and/or geographical region, or by using search criteria.<br /><br />The call returns paginated search results containing the charitable organizations that match the specified criteria. |

## Enhanced Skill Content
## Question Mapping

- "Find a charity by its ID?" -> GET /charity_org/{charity_org_id}
- "Look up charity organization details?" -> GET /charity_org/{charity_org_id}
- "Where is a specific charity located?" -> GET /charity_org/{charity_org_id}
- "What is a charity's mission statement?" -> GET /charity_org/{charity_org_id}
- "Get a charity's logo image URL?" -> GET /charity_org/{charity_org_id}
- "Search for charities by name?" -> GET /charity_org (use `q` parameter)
- "List all charities in a marketplace?" -> GET /charity_org
- "Find a charity by its registration ID?" -> GET /charity_org (use `registration_ids` parameter)
- "How many charities are available?" -> GET /charity_org (check `total` in response)
- "Get the next page of charity results?" -> GET /charity_org (use `offset` and `limit` parameters)
- "What charities match multiple registration IDs?" -> GET /charity_org (pass comma-separated `registration_ids`)
- "Does a specific charity have a website?" -> GET /charity_org/{charity_org_id} (check `website` field)
- "What country is a charity registered in?" -> GET /charity_org/{charity_org_id} (check `location.address.country`)
- "Browse charities with pagination?" -> GET /charity_org (iterate using `next` link or increment `offset`)

## Response Tips

- **Single charity** (`GET /charity_org/{charity_org_id}`): Returns a flat object with nested `location` (containing `address` and `geoCoordinates` maps) and `logoImage` map; missing optional fields may be absent rather than null.
- **Charity search/list** (`GET /charity_org`): Paginated via `offset`/`limit` with `total` count; use `next` and `prev` href strings to navigate pages; `charityOrgs` is the array of results.
- **Errors**: 400 indicates bad input (malformed ID, invalid query params, missing marketplace header); 404 only on single-charity lookup when ID does not exist; 500 is a server-side issue worth retrying.

## Anomaly Flags

- **Missing `X-EBAY-C-MARKETPLACE-ID` header**: Both endpoints require it; omitting it triggers a 400 that may not clearly indicate the missing header -- always include it.
- **Empty `charityOrgs` array with `total: 0`**: Surface when a search returns no results so the user can refine their query or check the marketplace ID.
- **404 on charity lookup**: The charity org ID may be invalid or the charity may have been delisted -- flag this clearly rather than silently failing.
- **Pagination exhaustion**: When `next` is absent or `offset + limit >= total`, surface that all results have been retrieved.
- **Unexpected 500 errors**: Flag for retry with exponential backoff; if persistent, suggest checking eBay API status page.
- **OAuth2 token expiry**: Auth failures (401/403) may surface outside the documented error codes -- flag and prompt for token refresh.

## Playbook

### 1. Search for a Charity by Name

1. Call `GET /charity_org` with `q` set to the search term and `X-EBAY-C-MARKETPLACE-ID` set to the target marketplace (e.g., `EBAY_US`).
2. Set `limit` to control page size (e.g., `10`).
3. Parse the `charityOrgs` array from the response.
4. If `total` exceeds `limit`, use the `next` URL or increment `offset` by `limit` to fetch additional pages.
5. Present matching charity names, IDs, and locations to the user.

### 2. Get Full Details for a Known Charity

1. Call `GET /charity_org/{charity_org_id}` with the charity's ID and the required `X-EBAY-C-MARKETPLACE-ID` header.
2. Extract key fields: `name`, `description`, `missionStatement`, `website`.
3. Parse `location.address` for city/state/country and `location.geoCoordinates` for lat/long if mapping is needed.
4. Use `logoImage.imageUrl` if displaying the charity's branding.

### 3. Look Up Charities by Registration IDs

1. Collect one or more registration IDs (e.g., EIN numbers).
2. Call `GET /charity_org` with `registration_ids` set to a comma-separated list and the required marketplace header.
3. Match returned `charityOrgs` entries against the input IDs using the `registrationId` field.
4. Flag any IDs that did not return a match.

### 4. Paginate Through All Charities in a Marketplace

1. Call `GET /charity_org` with `X-EBAY-C-MARKETPLACE-ID`, `offset=0`, and a chosen `limit` (e.g., `50`).
2. Record `total` from the first response.
3. Loop: increment `offset` by `limit` and repeat the call until `offset >= total` or `next` is absent.
4. Accumulate all `charityOrgs` entries across pages.
5. Surface the final count to confirm all records were retrieved.

### 5. Verify a Charity Exists Before Using It

1. Call `GET /charity_org/{charity_org_id}` with the candidate ID and marketplace header.
2. If 200: the charity is valid -- extract `name` and `registrationId` for confirmation.
3. If 404: the charity does not exist or is delisted -- inform the user and suggest searching by name via `GET /charity_org?q=...`.
4. If 400: the ID format is likely invalid -- check formatting and retry.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
