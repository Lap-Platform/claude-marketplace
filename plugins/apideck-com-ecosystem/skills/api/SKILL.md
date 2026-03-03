---
name: ecosystem-api
description: "Ecosystem API skill. Use when working with Ecosystem for ecosystems. Covers 12 endpoints."
version: 1.0.0
generator: lapsh
---

# Ecosystem API
API version: 0.0.6

## Auth
No authentication required.

## Base URL
https://api.apideck.com

## Setup
1. No auth setup needed
2. GET /ecosystems/{ecosystem_id}/listings -- verify access

## Endpoints

12 endpoints across 1 groups. See references/api-spec.lap for full details.

### ecosystems
| Method | Path | Description |
|--------|------|-------------|
| GET | /ecosystems/{ecosystem_id} | Get ecosystem |
| GET | /ecosystems/{ecosystem_id}/listings | List listings |
| GET | /ecosystems/{ecosystem_id}/listings/{id} | Get listing |
| GET | /ecosystems/{ecosystem_id}/categories | List categories |
| GET | /ecosystems/{ecosystem_id}/categories/{id} | Get category |
| GET | /ecosystems/{ecosystem_id}/categories/{id}/listings | List category listings |
| GET | /ecosystems/{ecosystem_id}/collections | List collections |
| GET | /ecosystems/{ecosystem_id}/collections/{id} | Get collection |
| GET | /ecosystems/{ecosystem_id}/collections/{id}/listings | List collection listings |
| GET | /ecosystems/{ecosystem_id}/products | List products |
| GET | /ecosystems/{ecosystem_id}/products/{id} | Get product |
| GET | /ecosystems/{ecosystem_id}/products/{id}/listings | List product listings |

## Enhanced Skill Content
## Question Mapping

- "What does my ecosystem look like?" -> GET /ecosystems/{ecosystem_id}
- "Show me all listings in the ecosystem" -> GET /ecosystems/{ecosystem_id}/listings
- "Get details for a specific listing" -> GET /ecosystems/{ecosystem_id}/listings/{id}
- "What categories exist in the ecosystem?" -> GET /ecosystems/{ecosystem_id}/categories
- "Tell me about the CRM category" -> GET /ecosystems/{ecosystem_id}/categories/{id}
- "Which listings are in a specific category?" -> GET /ecosystems/{ecosystem_id}/categories/{id}/listings
- "List all collections" -> GET /ecosystems/{ecosystem_id}/collections
- "Show me the details of a collection" -> GET /ecosystems/{ecosystem_id}/collections/{id}
- "What listings belong to a collection?" -> GET /ecosystems/{ecosystem_id}/collections/{id}/listings
- "What products are available?" -> GET /ecosystems/{ecosystem_id}/products
- "Get details for a specific product" -> GET /ecosystems/{ecosystem_id}/products/{id}
- "Which listings are associated with a product?" -> GET /ecosystems/{ecosystem_id}/products/{id}/listings
- "How many published listings does my ecosystem have?" -> GET /ecosystems/{ecosystem_id} (check `total_published_listings`)
- "Find a listing by its external ID" -> GET /ecosystems/{ecosystem_id}/listings (use `external_id` param)
- "Is my ecosystem published and what domain is it on?" -> GET /ecosystems/{ecosystem_id} (check `is_published`, `custom_domain`)

## Response Tips

- **Ecosystem detail**: Deeply nested -- `card_settings`, `cta_settings`, `custom_settings`, `integration_settings`, `lead_form_settings`, `listing_settings`, `masthead_settings`, `meta_tag_settings` are all sub-objects within `data`. Access them as `data.card_settings.columns`, etc.
- **List endpoints** (listings, categories, collections, products): All paginated via cursor. Next page: pass `meta.cursors.next` as `cursor` param. Stop when `meta.cursors.next` is `null`. Default limit is 50.
- **Single-resource endpoints**: Response wraps the object in `data` with `status_code` and `status` at the top level. Always check `status === "OK"` before processing `data`.
- **Collections list**: Unlike other list endpoints, `/collections` does NOT return `meta` or `links` -- only `data`. Assume no pagination support.

## Anomaly Flags

- **Unpublished ecosystem**: If `GET /ecosystems/{id}` returns `is_published: false`, warn the user -- all public-facing features may be inaccessible.
- **Missing cursors**: If `meta.cursors.next` is `null` but `items_on_page` equals the `limit`, there may be exactly one page of results -- flag that the total count might be higher than visible.
- **Disabled detail pages**: If a listing has `detail_page_disabled: true`, linking to its detail page will fail -- surface this when listing details are retrieved.
- **Deprecated integration fields**: Fields like `piesync_id`, `combidesk_id`, `blendr_id`, `integromat_id` refer to services that have been sunset or rebranded. Flag when these are populated but newer equivalents (e.g., `unify_connector_id`) are empty.
- **Missing logo/media**: If `logo.url` is empty or `screenshots` is an empty array on a published listing, flag it as incomplete content.
- **Stale timestamps**: If `updated_at` is significantly older than expected (e.g., > 1 year), flag the resource as potentially stale.

## Playbook

### 1. Browse and inventory an entire ecosystem

1. Call `GET /ecosystems/{ecosystem_id}` to get the ecosystem name, total published listings, and configuration.
2. Call `GET /ecosystems/{ecosystem_id}/categories` to enumerate all categories.
3. Call `GET /ecosystems/{ecosystem_id}/collections` to enumerate all collections.
4. Call `GET /ecosystems/{ecosystem_id}/products` to enumerate all products.
5. Summarize: name, publication status, category count, collection count, product count, and total published listings.

### 2. Paginate through all listings

1. Call `GET /ecosystems/{ecosystem_id}/listings?limit=50` (no cursor for first page).
2. Read `meta.cursors.next` from the response.
3. If `next` is not null, call `GET /ecosystems/{ecosystem_id}/listings?limit=50&cursor={next}`.
4. Repeat step 2-3 until `meta.cursors.next` is null.
5. Aggregate all `data` arrays into a complete listing set.

### 3. Deep-dive a specific listing

1. Call `GET /ecosystems/{ecosystem_id}/listings` and scan `data` for the target by name or `external_id`.
2. Note the listing `id` from the match.
3. Call `GET /ecosystems/{ecosystem_id}/listings/{id}` for full details including partner info, screenshots, pricing, and media.
4. Check `published`, `upcoming`, and `detail_page_disabled` to understand the listing's visibility state.
5. Review `categories` and `collections` arrays to see where the listing appears.

### 4. Audit ecosystem branding and configuration

1. Call `GET /ecosystems/{ecosystem_id}`.
2. Inspect `card_settings` for visual layout (columns, icon size, border radius, shadow).
3. Check `cta_settings.enabled` -- if true, review button label, link, and copy.
4. Review `meta_tag_settings` for SEO completeness (title, description, keywords).
5. Verify `custom_settings.domain` matches `custom_domain` for DNS consistency.
6. Check `integration_settings` for active third-party tools (analytics, chat, automation).

### 5. Find all listings for a specific category

1. Call `GET /ecosystems/{ecosystem_id}/categories` and locate the target category by name.
2. Note the category `id` and its `count` field for expected listing volume.
3. Call `GET /ecosystems/{ecosystem_id}/categories/{id}/listings?limit=50`.
4. Paginate using `meta.cursors.next` until all listings are retrieved.
5. Compare retrieved count against the category's `count` field to verify completeness.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
