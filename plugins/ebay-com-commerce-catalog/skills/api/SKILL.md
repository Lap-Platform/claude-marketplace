---
name: catalog-api
description: "Catalog API skill. Use when working with Catalog for product, product_summary. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# Catalog API
API version: v1_beta.5.3

## Auth
OAuth2

## Base URL
https://api.ebay.com{basePath}

## Setup
1. Configure auth: OAuth2
2. GET /product_summary/search -- verify access

## Endpoints

2 endpoints across 2 groups. See references/api-spec.lap for full details.

### product
| Method | Path | Description |
|--------|------|-------------|
| GET | /product/{epid} | This method retrieves details of the catalog product identified by the eBay product identifier (ePID) specified in the request. These details include the product's title and description, aspects and their values, associated images, applicable category IDs, and any recognized identifiers that apply to the product. <br /><br /> For a new listing, you can use the <b>search</b> method to identify candidate products on which to base the listing, then use the <b>getProduct</b> method to present the full details of those candidate products to the seller to make a a final selection. |

### product_summary
| Method | Path | Description |
|--------|------|-------------|
| GET | /product_summary/search | This method searches for and retrieves summaries of one or more products in the eBay catalog that match the search criteria provided by a seller. The seller can use the summaries to select the product in the eBay catalog that corresponds to the item that the seller wants to offer for sale. When a corresponding product is found and adopted by the seller, eBay will use the product information to populate the item listing. The criteria supported by <b>search</b> include keywords, product categories, and category aspects. To see the full details of a selected product, use the <b>getProduct</b> call. <br /><br /> In addition to product summaries, this method can also be used to identify <i>refinements</i>, which help you to better pinpoint the product you're looking for. A refinement consists of one or more <i>aspect</i> values and a count of the number of times that each value has been used in previous eBay listings. An aspect is a property (e.g. color or size) of an eBay category, used by sellers to provide details about the items they're listing. The <b>refinement</b> container is returned when you include the <b>fieldGroups</b> query parameter in the request with a value of <code>ASPECT_REFINEMENTS</code> or <code>FULL</code>. <br /><br /> <span style="padding: 15px 20px; display: block; border: 1px solid #cccccc"><b>Example</b> <br />A seller wants to find a product that is "gray" in color, but doesn't know what term the manufacturer uses for that color. It might be <code>Silver</code>, <code>Brushed Nickel</code>, <code>Pewter</code>, or even <code>Grey</code>. The returned <b>refinement</b> container identifies all aspects that have been used in past listings for products that match your search criteria, along with all of the values those aspects have taken, and the number of times each value was used. You can use this data to present the seller with a histogram of the values of each aspect. The seller can see which color values have been used in the past, and how frequently they have been used, and selects the most likely value or values for their product. You issue the <b>search</b> method again with those values in the <b>aspect_filter</b> parameter to narrow down the collection of products returned by the call.</span> <br /><br /> Although all query parameters are optional, this method must include at least the <b>q</b> parameter, or the <b>category_ids</b>, <b>gtin</b>, or <b>mpn</b> parameter with a valid value. If you provide more than one of these parameters, they will be combined with a logical AND to further refine the returned collection of matching products. <br /><br /> <span class="tablenote"><strong>Note:</strong> This method requires that certain special characters in the query parameters be percent-encoded: <br /><br /> &nbsp;&nbsp;&nbsp;&nbsp;<code>(space)</code> = <code>%20</code> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<code>,</code> = <code>%2C</code> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<code>:</code> = <code>%3A</code> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<code>[</code> = <code>%5B</code> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<code>]</code> = <code>%5D</code> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<code>{</code> = <code>%7B</code> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<code>|</code> = <code>%7C</code> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<code>}</code> = <code>%7D</code> <br /><br /> This requirement applies to all query parameter values. However, for readability, method examples and samples in this documentation will not use the encoding.</span> <br /><br /> This method returns product summaries rather than the full details of the products. To retrieve the full details of a product, use the <b>getProduct</b> method with an ePID. |

## Enhanced Skill Content
## Question Mapping

- "What product details does eBay have for this ePID?" -> GET /product/{epid}
- "Show me images and description for a specific eBay product" -> GET /product/{epid}
- "What GTINs, UPCs, or EANs are associated with this product?" -> GET /product/{epid}
- "How many vehicle compatibilities does this product have?" -> GET /product/{epid}
- "Search for products matching a keyword on eBay" -> GET /product_summary/search
- "Find products by GTIN or MPN" -> GET /product_summary/search
- "What products exist in a specific eBay category?" -> GET /product_summary/search
- "Filter product search results by aspect (e.g., color, size)?" -> GET /product_summary/search
- "How many total products match my search query?" -> GET /product_summary/search
- "Get the next page of product search results" -> GET /product_summary/search
- "Search for products on a specific eBay marketplace (e.g., UK, DE)?" -> GET /product_summary/search (with X-EBAY-C-MARKETPLACE-ID header)
- "What are the dominant categories and aspect refinements for my search?" -> GET /product_summary/search
- "Look up a product by UPC or ISBN" -> GET /product_summary/search (using gtin param)
- "What brand and MPN does a product have?" -> GET /product/{epid}

## Response Tips

- **Product detail (GET /product/{epid})**: Response is a flat object with arrays for multi-value identifiers (ean, upc, isbn, mpn, gtin). `aspects` and `additionalImages` are arrays of maps -- iterate to extract facet names/values and image URLs. `image` is a single map with height/width/imageUrl.
- **Product search (GET /product_summary/search)**: Paginated via `offset`/`limit`/`total` with `next` and `prev` URLs for cursor navigation. A 204 means zero results (empty body, not an empty list). `refinement.aspectDistributions` contains facet counts for narrowing searches. `productSummaries` is the results array.
- **Errors (all endpoints)**: 400 = malformed request or invalid parameter values, 403 = insufficient OAuth scope or marketplace access denied, 404 = ePID not found (product detail only), 500 = retry with backoff.

## Anomaly Flags

- **204 on search**: Surface explicitly -- means no results at all, not an error. Suggest broadening query or checking category_ids.
- **Missing identifiers**: If a product response returns empty `ean`, `upc`, and `gtin` arrays, flag that the product lacks standard identifiers -- downstream listing or matching workflows may fail.
- **High compatibilityCount**: If `compatibilityCount` is large (>500), alert the user -- this is a parts/accessories product with extensive fitment data that may need separate compatibility API calls.
- **Pagination ceiling**: If `total` greatly exceeds what can be paged through (offset + limit approaching API limits), warn that not all results are retrievable.
- **403 on marketplace-specific requests**: If X-EBAY-C-MARKETPLACE-ID is set and a 403 is returned, flag that the OAuth token may lack scope for that marketplace.
- **Stale product version**: The `version` field in product detail can indicate catalog updates -- surface when it changes between calls.

## Playbook

### 1. Search and Inspect a Product

1. Call `GET /product_summary/search?q=<keyword>&limit=5` to find matching products
2. If 204 is returned, broaden the query or remove filters
3. From `productSummaries`, pick the best match and extract its `epid`
4. Call `GET /product/{epid}` to retrieve full product details
5. Use `title`, `brand`, `description`, and identifier arrays as needed

### 2. Browse Products by Category with Refinements

1. Call `GET /product_summary/search?category_ids=<id>&limit=10` to list products in a category
2. Inspect `refinement.aspectDistributions` for available facets (e.g., Brand, Color)
3. Narrow results with `aspect_filter` (e.g., `aspect_filter=categoryId:123,Brand:{Sony}`)
4. Page through results using `next` URL or by incrementing `offset`
5. Check `total` to understand full result set size

### 3. Look Up a Product by Barcode (UPC/EAN/GTIN)

1. Call `GET /product_summary/search?gtin=<barcode>` with the scanned or known barcode
2. If 204, the barcode is not in the eBay catalog -- try searching by keyword instead
3. If results are returned, extract `epid` from the top match
4. Call `GET /product/{epid}` for full details including all associated identifiers

### 4. Multi-Marketplace Product Comparison

1. Call `GET /product/{epid}` with header `X-EBAY-C-MARKETPLACE-ID: EBAY_US` to get US catalog data
2. Repeat with `EBAY_GB`, `EBAY_DE`, or other marketplace IDs
3. Compare `title`, `description`, and `aspects` across marketplaces for localization differences
4. Note any 403 errors -- these indicate the product or marketplace is not accessible with current credentials

### 5. Bulk Product Enrichment

1. Start with a list of GTINs or MPNs to enrich
2. For each identifier, call `GET /product_summary/search?gtin=<value>` (or `mpn=<value>`)
3. Collect `epid` from each successful match
4. Call `GET /product/{epid}` for each to retrieve full metadata (brand, images, aspects, identifiers)
5. Handle 204s and 404s gracefully -- log unmatched identifiers for manual review


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
