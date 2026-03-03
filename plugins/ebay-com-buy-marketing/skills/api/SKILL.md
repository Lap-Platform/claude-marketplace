---
name: buy-marketing-api
description: "Buy Marketing API skill. Use when working with Buy Marketing for merchandised_product. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Buy Marketing API
API version: v1_beta.2.0

## Auth
OAuth2

## Base URL
https://api.ebay.com/buy/marketing/v1_beta

## Setup
1. Configure auth: OAuth2
2. GET /merchandised_product -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### merchandised_product
| Method | Path | Description |
|--------|------|-------------|
| GET | /merchandised_product | This method returns an array of products based on the category and metric specified. This includes details of the product, such as the eBay product ID (EPID), title, and user reviews and ratings for the product. You can use the <code>epid</code> returned by this method in the Browse API <b>search</b> method to retrieve items for this product. <h3><b>Restrictions </b></h3> <ul><li>To test <b> getMerchandisedProducts</b> in Sandbox, you must use category ID 9355 and the response will be mock data.  </li>   <li>For a list of supported sites and other restrictions, see <a href="/api-docs/buy/marketing/overview.html#API">API Restrictions</a>.</li>  </ul> |

## Enhanced Skill Content
## Question Mapping

- "What are the best-selling products in a category?" -> GET /merchandised_product
- "Show me trending items for category 267?" -> GET /merchandised_product
- "Which products are most popular in Electronics?" -> GET /merchandised_product
- "Get merchandised products filtered by brand?" -> GET /merchandised_product (use aspect_filter)
- "How do I find top-rated products in a specific category?" -> GET /merchandised_product (metric_name=BEST_SELLING)
- "Can I limit the number of merchandised products returned?" -> GET /merchandised_product (use limit)
- "What metrics are available for merchandised products?" -> GET /merchandised_product (metric_name is required -- try BEST_SELLING)
- "Show me the top 5 products in Clothing?" -> GET /merchandised_product (limit=5, category_id for Clothing)
- "How do I filter merchandised products by color or size?" -> GET /merchandised_product (use aspect_filter with key:value pairs)
- "What happens if I request an invalid category?" -> GET /merchandised_product returns 400
- "Why am I getting a 409 conflict error?" -> GET /merchandised_product -- category_id may conflict with marketplace or metric constraints
- "Is there a way to browse merchandised products without a category?" -> No -- category_id is required
- "How do I paginate through merchandised product results?" -> GET /merchandised_product (use limit; API returns a fixed window, no offset-based paging)

## Response Tips

- **merchandised_product**: Response contains a list of product objects with image, title, price, and rating fields. The `limit` param caps results but there is no offset/cursor -- this is a curated snapshot, not a paginated collection. Error 400 means bad category_id or metric_name; 409 indicates a conflict between the requested metric and the category or marketplace; 500 is a server-side retry scenario.

## Anomaly Flags

- **400 with no obvious cause**: The category_id may be valid but not supported for the requested metric_name on the caller's marketplace -- surface the specific error message to the user.
- **409 Conflict**: Unusual for a GET endpoint. Flag this prominently -- it likely means the category/metric combination is disallowed or the data is temporarily inconsistent.
- **500 errors**: Transient eBay platform issues. Recommend retry with backoff; if persistent, flag as a service degradation.
- **Empty result set on 200**: The category exists but has no merchandised products for the given metric. Surface this explicitly so the user does not assume a failure.
- **OAuth2 token expiry**: Auth failures will manifest before reaching this endpoint. If requests suddenly fail after working, surface token refresh as the likely fix.
- **aspect_filter misuse**: Invalid aspect keys silently return unfiltered results rather than erroring. Flag when aspect_filter is provided but results appear unfiltered.

## Playbook

### 1. Find Best-Selling Products in a Category

1. Identify the eBay category ID for your target category (use eBay Taxonomy API if needed).
2. Call `GET /merchandised_product?category_id={id}&metric_name=BEST_SELLING`.
3. Optionally add `limit=10` to cap results.
4. Parse the response for product titles, prices, images, and ratings.

### 2. Filter Merchandised Products by Aspect

1. Call `GET /merchandised_product?category_id={id}&metric_name=BEST_SELLING` first to see available products.
2. Identify the aspect you want to filter on (e.g., Brand, Color).
3. Reissue the call with `aspect_filter=Brand:{value}` to narrow results.
4. Compare the filtered vs. unfiltered result count to confirm the filter took effect.

### 3. Handle Errors Gracefully

1. On **400**: Check that `category_id` is a valid leaf category and `metric_name` is a supported value. Log the error detail from the response body.
2. On **409**: Try a different `metric_name` or verify the category is eligible for merchandised products on your marketplace.
3. On **500**: Wait 2-5 seconds, then retry. After 3 failures, abort and notify the user of an eBay service issue.

### 4. Build a Trending Products Dashboard

1. Assemble a list of target category IDs for your dashboard sections.
2. For each category, call `GET /merchandised_product?category_id={id}&metric_name=BEST_SELLING&limit=5`.
3. Aggregate responses into a unified display, grouping by category.
4. Cache results for 1-4 hours -- merchandised product data is curated and does not change frequently.
5. Surface any categories that returned empty results or errors as "unavailable" sections.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
