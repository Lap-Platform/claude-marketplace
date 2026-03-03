---
name: chomp-food-database-api-documentation
description: "Chomp Food Database API Documentation API skill. Use when working with Chomp Food Database API Documentation for food. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# Chomp Food Database API Documentation
API version: 1.0.0-oas3

## Auth
ApiKey api_key in query

## Base URL
https://chompthis.com/api/v2

## Setup
1. Set your API key in the appropriate header
2. GET /food/branded/barcode.php -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### food
| Method | Path | Description |
|--------|------|-------------|
| GET | /food/branded/barcode.php | Get a branded food item using a barcode |
| GET | /food/branded/name.php | Get a branded food item by name |
| GET | /food/branded/search.php | Get data for branded food items using various search parameters |
| GET | /food/ingredient/search.php | Get raw/generic food ingredient item(s) |

## Enhanced Skill Content
## Question Mapping

- "What food product has this barcode?" -> GET /food/branded/barcode.php
- "Look up a product by its UPC code" -> GET /food/branded/barcode.php
- "Scan this barcode and tell me what it is" -> GET /food/branded/barcode.php
- "Find branded foods called 'oat milk'" -> GET /food/branded/name.php
- "Search for products by brand name" -> GET /food/branded/name.php
- "Show me the first 5 results for 'protein bar'" -> GET /food/branded/name.php (limit=5)
- "What vegan foods are available?" -> GET /food/branded/search.php (diet=Vegan)
- "Find gluten free snacks in the US" -> GET /food/branded/search.php (diet=Gluten Free, country=US)
- "Which products contain almonds?" -> GET /food/branded/search.php (ingredient=almonds)
- "Search for foods high in vitamin D" -> GET /food/branded/search.php (vitamin=vitamin D)
- "Find products without palm oil" -> GET /food/branded/search.php (palm_oil=...)
- "What foods have iron as a mineral?" -> GET /food/branded/search.php (mineral=iron)
- "Look up the ingredient 'xanthan gum'" -> GET /food/ingredient/search.php
- "What is maltodextrin?" -> GET /food/ingredient/search.php (find=maltodextrin)
- "Find allergen-free alternatives in a category" -> GET /food/branded/search.php (allergen + category)

## Response Tips

- **All endpoints** return `{items: [map]}` -- always iterate over `items` array; an empty array means no matches, not an error.
- **Barcode lookup** returns zero or one item in `items` -- treat array length 0 as "product not found" even though HTTP status may be 200.
- **Name and search endpoints** support `limit` (max 10) and `page` for pagination -- if `items` returns exactly `limit` results, more pages likely exist.
- **Ingredient search** has a tighter limit cap (max 3) -- expect concise results; prompt user to refine the query if nothing matches.
- **Error responses** (400/401/404/500) -- 401 means the `api_key` query param is missing or invalid; 400 typically indicates a missing required parameter.

## Anomaly Flags

- **401 on any request**: API key is missing, expired, or malformed -- surface immediately and suggest checking the `api_key` parameter.
- **Empty `items` array on barcode lookup**: The barcode may be valid but not in Chomp's database -- flag this and suggest trying the name search as a fallback.
- **Repeated 500 errors**: Chomp API may be experiencing downtime -- surface after two consecutive failures and suggest retrying later.
- **Page returns fewer results than `limit`**: You have reached the last page of results -- proactively note "no more results available."
- **Unexpected `limit` values**: Branded search accepts 1-10, ingredient search accepts 1-3 -- flag if user requests more and explain the cap.
- **Missing nutritional fields in response maps**: Some branded products have incomplete data -- flag when key nutrition fields (calories, protein, fat) are null or absent.

## Playbook

### 1. Identify a Product by Barcode

1. Call `GET /food/branded/barcode.php?code={barcode}&api_key={key}`
2. Check if `items` array is non-empty
3. If empty, fall back to `GET /food/branded/name.php` using the product name from the packaging
4. Extract nutrition info, brand, and category from the first item in `items`

### 2. Search for Diet-Compliant Foods

1. Call `GET /food/branded/search.php?diet={Vegan|Vegetarian|Gluten Free}&api_key={key}&limit=10`
2. Optionally narrow by `category`, `country`, or `brand`
3. Page through results using `page=2`, `page=3`, etc. until `items` returns fewer than `limit` results
4. Present matching products with brand, name, and key nutritional highlights

### 3. Investigate an Unfamiliar Ingredient

1. Call `GET /food/ingredient/search.php?find={ingredient_name}&api_key={key}&limit=3`
2. Review the returned items for description, common uses, and safety info
3. If more context is needed, call `GET /food/branded/search.php?ingredient={ingredient_name}&api_key={key}` to see which products contain it
4. Summarize findings: what it is, where it appears, and any dietary flags

### 4. Find Allergen-Safe Alternatives

1. Call `GET /food/branded/search.php?category={desired_category}&api_key={key}&limit=10`
2. Filter results by adding `allergen={allergen_to_avoid}` to exclude products containing the allergen
3. Cross-check with `trace={allergen}` to also exclude products with trace contamination warnings
4. Present the safe options with brand, name, and allergen/trace details

### 5. Compare Products by Name

1. Call `GET /food/branded/name.php?name={product_name}&api_key={key}&limit=10` for the first product
2. Repeat for the second product name
3. Extract nutritional maps from each result's `items[0]`
4. Build a side-by-side comparison of calories, macros, and key micronutrients
5. Highlight meaningful differences and flag any missing data fields


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
