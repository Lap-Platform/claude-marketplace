---
name: recommendation-api
description: "Recommendation API skill. Use when working with Recommendation for find. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Recommendation API
API version: v1.1.0

## Auth
OAuth2

## Base URL
https://api.ebay.com{basePath}

## Setup
1. Configure auth: OAuth2
3. POST /find -- create first find

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### find
| Method | Path | Description |
|--------|------|-------------|
| POST | /find | The <b>find</b> method currently returns information for a single recommendation type (<code>AD</code>) which contains information that sellers can use to configure <a href="/api-docs/sell/static/marketing/promoted-listings.html" title="Selling Integration Guide">Promoted Listings</a> ad campaigns. <p>The response from this method includes an array of the seller's listing IDs, where each element in the array contains recommendations related to the associated listing ID. For details on how to use this method, see <a href="/api-docs/sell/static/marketing/pl-reco-api.html" title="Selling Integration Guide">Using the Recommendation API to help configure campaigns</a>.</p>  <h3>The AD recommendation type</h3>  </p>  <p>The <code>AD</code> type contains two sets of information:</p>  <ul><li><b>The promoteWithAd indicator</b> <br>The <b>promoteWithAd</b> response field indicates whether or not eBay recommends you place the associated listing in a Promoted Listings ad campaign. <p>The returned value is set to either <code>RECOMMENDED</code> or <code>UNDETERMINED</code>, where <code>RECOMMENDED</code> identifies the listings that will benefit the most from having them included in an ad campaign.</p></li>  <li><b>The bid percentage</b> <br>Also known as the "ad rate," the <b>bidPercentage</b> field provides the current trending bid percentage of similarly promoted items in the marketplace. <p>The ad rate is a user-specified value that indicates the level of promotion that eBay applies to the campaign across the marketplace. The value is also used to calculate the Promotion Listings fee, which is assessed to the seller if a Promoted Listings action results in the sale of an item.</p></li></ul>  <h3>Configuring the request</h3> <p>You can configure a request to review all of a seller's currently active listings, or just a subset of them.</p>  <ul><li><b>All active listings</b> &ndash; If you leave the request body empty, the request targets <i>all</i> the items currently listed by the seller. <p>Here, the response is filtered to contain only the items where <b>promoteWithAd</b> equals <code>RECOMMENDED</code>. In this case, eBay recommends that all the returned listings should be included in a Promoted Listings ad campaign.</p></li> <li><b>Selected listing IDs</b> &ndash; If you populate the request body with a set of <b>listingIds</b>, the response contains data for all the specified listing IDs. <p>In this scenario, the response provides you with information on listings where the <b>promoteWithAd</b> can be either <code>RECOMMENDED</code> or <code>UNDETERMINED</code>.</li></ul>  <h3>The paginated response</h3>  <p>Because the response can contain many listing IDs, the <b>findListingRecommendations</b> method paginates the response set.</p> <p>You can control size of the returned pages, as well as an offset that dictates where to start the pagination, using query parameters in the request. |

## Enhanced Skill Content
## Question Mapping

- "What recommendations are available for my listing?" -> POST /find
- "How do I get suggestions to improve a specific eBay listing?" -> POST /find
- "Can I check recommendations for multiple listings at once?" -> POST /find with listingIds
- "How do I filter recommendations by type?" -> POST /find with filter
- "What marketplace do I target for recommendations?" -> POST /find with X-EBAY-C-MARKETPLACE-ID header
- "How do I paginate through a large set of recommendations?" -> POST /find with limit and offset
- "Why am I getting no recommendations for my listing?" -> POST /find (check for 204 No Content)
- "How do I get recommendations for the US marketplace?" -> POST /find with X-EBAY-C-MARKETPLACE-ID: EBAY_US
- "Can I limit the number of recommendations returned?" -> POST /find with limit
- "How do I skip the first N recommendations?" -> POST /find with offset
- "What happens if I send an invalid listing ID?" -> POST /find (watch for 400 error)
- "How do I get recommendations for a German eBay listing?" -> POST /find with X-EBAY-C-MARKETPLACE-ID: EBAY_DE

## Response Tips

- **POST /find**: A 200 means recommendations exist; a 204 means the listing is already optimized or no suggestions apply -- do not treat 204 as an error. Paginate with `limit`/`offset` when working with bulk listing IDs. A 400 typically signals a malformed filter or invalid listing ID; inspect the `errors` array for field-level detail. 500 is transient -- retry with backoff.

## Anomaly Flags

- **204 No Content on every request**: May indicate incorrect marketplace ID or that listings are not live -- surface to user for review
- **Repeated 400 errors**: Likely a malformed filter string or invalid listingIds format -- flag the request body for inspection
- **500 errors**: Transient server issue; if persistent across retries, alert the user that eBay's Recommendation service may be degraded
- **Missing X-EBAY-C-MARKETPLACE-ID**: Required header omitted -- will fail; proactively warn before sending
- **OAuth token expiry**: If 401/403 responses appear (outside documented errors), surface that the OAuth2 token likely needs refresh
- **Large listingIds arrays**: If sending many IDs without pagination params, warn that response may be truncated or slow

## Playbook

### 1. Get Recommendations for a Single Listing

1. Obtain a valid OAuth2 token for the eBay Recommendation API scope
2. Send `POST /find` with header `X-EBAY-C-MARKETPLACE-ID` set to the target marketplace (e.g., `EBAY_US`)
3. Include the listing ID in the `listingIds` array
4. If 200, parse the recommendations from the response body
5. If 204, report that no recommendations are available for this listing

### 2. Bulk-Check Recommendations Across Listings

1. Collect all listing IDs to check
2. Send `POST /find` with `listingIds` containing the batch, `limit` set to a reasonable page size (e.g., 50), and `offset` at 0
3. Process the returned recommendations
4. Increment `offset` by `limit` and repeat until a 204 or fewer results than `limit` are returned
5. Aggregate all recommendations for reporting

### 3. Filter Recommendations by Type

1. Determine the desired recommendation category (e.g., pricing, listing quality)
2. Send `POST /find` with the `filter` parameter set to the target type
3. Set the appropriate `X-EBAY-C-MARKETPLACE-ID` header
4. Parse the 200 response for filtered recommendations
5. If 204, no recommendations of that type exist for the given listings

### 4. Handle Errors and Retry

1. Send `POST /find` with the desired parameters
2. On 400, inspect the error response body for field-level validation messages; fix the request and resend
3. On 500, wait 2 seconds, then retry up to 3 times with exponential backoff
4. On repeated 500s, surface a degradation warning and stop retrying
5. Log all error responses for debugging


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
