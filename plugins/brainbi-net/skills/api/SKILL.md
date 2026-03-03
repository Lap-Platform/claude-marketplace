---
name: brainbi
description: "brainbi API skill. Use when working with brainbi for {{server}}. Covers 33 endpoints."
version: 1.0.0
generator: lapsh
---

# brainbi

## Auth
ApiKey Authorization in header

## Base URL
Not specified.

## Setup
1. Set your API key in the appropriate header
2. GET /{{server}}/api/rule -- verify access
3. POST /{{server}}/api/rule -- create first rule

## Endpoints

33 endpoints across 1 groups. See references/api-spec.lap for full details.

### {{server}}
| Method | Path | Description |
|--------|------|-------------|
| GET | /{{server}}/api/rule | Rules |
| GET | /{{server}}/api/rule/1 | Rule {id} |
| POST | /{{server}}/api/rule | Rule |
| GET | /{{server}}/api/rule/ruleData/1 | Rule Data |
| GET | /{{server}}/api/rule/ruleData/1/latest | Rule Data Latest |
| GET | /{{server}}/api/products | Products |
| GET | /{{server}}/api/products/1 | Products {id} |
| GET | /{{server}}/api/products/23767/rules | Products {id} Get Rules |
| POST | /{{server}}/api/products | Products |
| GET | /{{server}}/api/analyze/pricing | [BETA] Scrape Product |
| GET | /{{server}}/api/analyze/pricing | [BETA] Scrape Product Copy |
| PUT | /{{server}}/api/products | Products |
| DELETE | /{{server}}/api/products/1137 | Products |
| GET | /{{server}}/api/customers | Customers |
| GET | /{{server}}/api/customers/1 | Customers {id} |
| POST | /{{server}}/api/customers | Customers |
| PUT | /{{server}}/api/customers/1137 | Customers |
| DELETE | /{{server}}/api/customers/1137 | Customers |
| GET | /{{server}}/api/orders | Orders |
| GET | /{{server}}/api/orders/12 | Orders {id} |
| POST | /{{server}}/api/orders | Orders |
| PUT | /{{server}}/api/orders/1137 | Orders |
| DELETE | /{{server}}/api/orders/1137 | Orders |
| GET | /{{server}}/api/orderlines | OrderLines |
| GET | /{{server}}/api/orderlines/123 | OrderLines {id} |
| POST | /{{server}}/api/orderlines | OrderLine |
| PUT | /{{server}}/api/orderlines/1137 | OrderLines |
| DELETE | /{{server}}/api/orderlines/1137 | OrderLines |
| GET | /{{server}}/api/seo/ranking/latest | SEO Latest Rankings |
| POST | /{{server}}/api/login | Login and get bearer token |
| POST | /{{server}}/api/register | Register |
| POST | /{{server}}/api/register_woocommerce | Register and Create Store Connection for WooCommerce |
| POST | /{{server}}/api/logout | Logout |

## Enhanced Skill Content
## Question Mapping

- "What scraping rules are configured?" -> GET /api/rule
- "Show me the details for rule ID 1" -> GET /api/rule/1
- "Create a new scraping rule for a product" -> POST /api/rule
- "What data has rule 1 collected?" -> GET /api/rule/ruleData/1
- "What is the latest scraped data for rule 1?" -> GET /api/rule/ruleData/1/latest
- "List all products in the system" -> GET /api/products
- "Get details for product 1" -> GET /api/products/1
- "What rules are attached to product 23767?" -> GET /api/products/23767/rules
- "Add a new product to track" -> POST /api/products
- "Run a pricing analysis for a product URL" -> GET /api/analyze/pricing
- "Delete product 1137" -> DELETE /api/products/1137
- "Show all orders and their statuses" -> GET /api/orders
- "What order lines belong to order 123?" -> GET /api/orderlines/123
- "What are the latest SEO rankings?" -> GET /api/seo/ranking/latest
- "Register a new WooCommerce store" -> POST /api/register_woocommerce

## Response Tips

- **Rules** (`/api/rule`, `/api/rule/:id`): Rule objects include `scrape_url` and `scrape_selector` -- check `type` field to determine scraping strategy. `ruleData` sub-resources return collected scrape results; use `/latest` to avoid fetching full history.
- **Products** (`/api/products`): Require many fields on create/update including `store_remote_id` and `store_remote_variant_id` -- these tie back to the external store. The `/rules` sub-resource links products to scraping rules.
- **Pricing Analysis** (`/api/analyze/pricing`): Takes the same fields as product creation -- treat this as a read-only analysis pass before committing a product. Watch for duplicate endpoint definitions in the spec (both are GET with identical signatures).
- **Orders & Order Lines** (`/api/orders`, `/api/orderlines`): Financial fields (`sub_total`, `shipping`, `total`) are strings, not numbers -- parse carefully. Bearer token auth is required on several endpoints but not all; check auth per call.
- **Customers** (`/api/customers`): Share the same field schema as orders (`currency`, `country`, `total`). The `created_at` field is required on create and update -- use ISO 8601 format.
- **Auth** (`/api/login`, `/api/register`, `/api/logout`): Login returns a Bearer token for subsequent authenticated requests. Logout requires the email, not the token.

## Anomaly Flags

- **Mixed auth models**: Most endpoints use ApiKey in header, but several (`GET /products/1`, `GET /orders/12`, `POST /orders`, `GET /orderlines`, `PUT /orderlines`) require Bearer token instead. Surface a warning if a Bearer-required call is attempted with only an ApiKey.
- **Duplicate endpoint**: `GET /api/analyze/pricing` appears twice with identical signatures -- flag if the API returns different results or errors on repeated calls; this may indicate a spec issue.
- **String-typed numerics**: Price, cost_price, shipping, sub_total, and total are all `str` -- flag if values contain non-numeric characters or currency symbols that could break downstream calculations.
- **Destructive operations without confirmation**: DELETE endpoints for products, customers, orders, and order lines all use hardcoded IDs in examples (1137) -- always confirm the target ID before executing deletions.
- **Missing pagination signals**: List endpoints (`/products`, `/orders`, `/customers`, `/orderlines`, `/rule`) show no pagination parameters -- flag if response payloads are unexpectedly large or truncated.
- **Stale scrape data**: When `/api/rule/ruleData/:id/latest` returns old timestamps, surface this as a potential scraping failure.

## Playbook

### 1. Onboard a New Store (WooCommerce)

1. Register the store via `POST /api/register_woocommerce` with credentials, shop URL, and WooCommerce API keys (`consumer_key`, `consumer_secret`).
2. Log in with `POST /api/login` using the registered email and password.
3. Store the returned Bearer token for authenticated requests.
4. Verify connectivity by calling `GET /api/products` to confirm the store integration is active.

### 2. Set Up Product Price Monitoring

1. Add the product via `POST /api/products` with full product details (name, vendor, price, cost_price, URL, EAN/UPC).
2. Create a scraping rule via `POST /api/rule` linking the `product_id`, target `scrape_url`, and CSS `scrape_selector`.
3. Validate the rule by fetching `GET /api/rule/ruleData/:id/latest` to confirm data collection has started.
4. Run `GET /api/analyze/pricing` with the product fields to get a competitive pricing analysis.

### 3. Full Order Lifecycle

1. Create a customer record via `POST /api/customers` with store ID, country, and currency.
2. Create the order via `POST /api/orders` (requires Bearer token) with totals and status.
3. Add line items via `POST /api/orderlines` for each product in the order.
4. Update order status via `PUT /api/orders/:id` as it progresses (e.g., pending to shipped).
5. To cancel, update status first via PUT, then optionally `DELETE /api/orders/:id` and `DELETE /api/orderlines/:id`.

### 4. Audit Product Rules and Scraped Data

1. List all products with `GET /api/products`.
2. For each product of interest, fetch its rules via `GET /api/products/:id/rules`.
3. For each rule, pull the latest scraped data via `GET /api/rule/ruleData/:ruleId/latest`.
4. Compare scraped prices against the product's `price` and `cost_price` to identify margin changes.
5. Flag any rules where latest data is stale (old timestamps) or missing.

### 5. SEO Ranking Check and Reporting

1. Authenticate via `POST /api/login` to get a session token.
2. Fetch the latest rankings via `GET /api/seo/ranking/latest`.
3. Cross-reference ranked products with `GET /api/products/:id` to enrich ranking data with product details.
4. Log out cleanly via `POST /api/logout` with the account email.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
