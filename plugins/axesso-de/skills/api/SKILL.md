---
name: axesso-api
description: "Axesso API skill. Use when working with Axesso for amz. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# Axesso Api
API version: 1.0.0

## Auth
No authentication required.

## Base URL
http://api.axesso.de

## Setup
1. No auth setup needed
2. GET /amz/amazon-lookup-product -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### amz
| Method | Path | Description |
|--------|------|-------------|
| GET | /amz/amazon-lookup-product | lookup product information |
| GET | /amz/amazon-lookup-buy-recommendations | request buy recommendations to a given product |
| GET | /amz/amazon-search-by-keyword | fetch results auf a keyword search on Amazon |
| GET | /amz/sort-options | request available sort options to use in keyword search |

## Enhanced Skill Content
## Question Mapping

- "What are the details for this Amazon product?" -> GET /amz/amazon-lookup-product
- "Look up an Amazon product by its URL" -> GET /amz/amazon-lookup-product
- "Get product info for a specific size variant" -> GET /amz/amazon-lookup-product (with `size` param)
- "What do people also buy with this product?" -> GET /amz/amazon-lookup-buy-recommendations
- "Show me recommended products related to this listing" -> GET /amz/amazon-lookup-buy-recommendations
- "Search Amazon for wireless headphones" -> GET /amz/amazon-search-by-keyword
- "Find products on Amazon.de matching a keyword" -> GET /amz/amazon-search-by-keyword (domainCode=de)
- "Search Amazon and sort by price" -> GET /amz/amazon-search-by-keyword (with `sortBy`)
- "Get the top 10 results for a keyword on Amazon" -> GET /amz/amazon-search-by-keyword (with `numberOfProducts`)
- "What sort options are available for Amazon searches?" -> GET /amz/sort-options
- "Which domain codes can I search on?" -> GET /amz/sort-options (check response for supported domains)
- "Compare recommendations across two products" -> GET /amz/amazon-lookup-buy-recommendations (call twice, diff results)
- "Find a product by keyword, then get its full details" -> GET /amz/amazon-search-by-keyword then GET /amz/amazon-lookup-product
- "What alternatives exist for a product I found?" -> GET /amz/amazon-lookup-product then GET /amz/amazon-lookup-buy-recommendations

## Response Tips

- **Product lookup** (`/amazon-lookup-product`): Response contains nested product attributes; check for variant/size-specific fields when `size` is provided. A 406 means the URL format is not acceptable -- verify it is a valid Amazon product URL.
- **Buy recommendations** (`/amazon-lookup-buy-recommendations`): Returns a list of recommended products; may be empty if Amazon has no suggestions for that listing. A 406 typically means the product URL is malformed or unsupported.
- **Keyword search** (`/amazon-search-by-keyword`): Results are bounded by `numberOfProducts`; there is no cursor-based pagination, so adjust `numberOfProducts` to control result volume. The `domainCode` determines which Amazon storefront is searched (e.g., `com`, `de`, `co.uk`).
- **Sort options** (`/sort-options`): Returns a static reference list; cache this locally rather than calling repeatedly.

## Anomaly Flags

- **406 Not Acceptable**: Surface immediately -- indicates the provided URL is malformed or points to an unsupported Amazon page. Prompt the user to verify the URL format.
- **404 on product lookup**: The product may have been delisted or the URL may reference a region not supported by the API. Flag and suggest trying a different domain or checking product availability.
- **Empty recommendation lists**: If buy recommendations return zero results, flag that Amazon may not have suggestion data for that product -- suggest trying the keyword search as an alternative discovery method.
- **Unusual response latency**: Amazon scraping APIs can be throttled upstream. If responses take significantly longer than normal, surface a warning about potential rate limiting on the provider side.
- **Missing fields in product response**: If key fields (price, availability, title) come back null or absent, flag that the listing may be restricted, out of stock, or region-locked.

## Playbook

### 1. Full Product Research

1. Call `GET /amz/sort-options` to understand available sort strategies
2. Call `GET /amz/amazon-search-by-keyword` with the target keyword and desired `domainCode`
3. Pick a result URL from the search response
4. Call `GET /amz/amazon-lookup-product` with that URL to get full details
5. Call `GET /amz/amazon-lookup-buy-recommendations` with the same URL to see related products

### 2. Cross-Market Price Comparison

1. Call `GET /amz/amazon-search-by-keyword` with `domainCode=com` for the US storefront
2. Call `GET /amz/amazon-search-by-keyword` with `domainCode=de` (or another region) using the same keyword
3. Call `GET /amz/amazon-lookup-product` on matching results from each region
4. Compare pricing, availability, and variant options across the two responses

### 3. Product Alternative Discovery

1. Start with a known Amazon product URL
2. Call `GET /amz/amazon-lookup-buy-recommendations` to get related products
3. For each recommendation of interest, call `GET /amz/amazon-lookup-product` to get full details
4. Present a comparison table of the original product vs. alternatives

### 4. Sorted Keyword Search

1. Call `GET /amz/sort-options` to retrieve valid sort values
2. Choose the appropriate sort option (e.g., price low-to-high, rating)
3. Call `GET /amz/amazon-search-by-keyword` with `keyword`, `domainCode`, `sortBy`, and `numberOfProducts` set
4. Review results and optionally drill into individual products with `/amazon-lookup-product`


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
