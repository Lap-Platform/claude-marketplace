---
name: akeneo-pim-rest-api
description: "Akeneo PIM REST API skill. Use when working with Akeneo PIM REST for api. Covers 137 endpoints."
version: 1.0.0
generator: lapsh
---

# Akeneo PIM REST API
API version: 1.0.0

## Auth
ApiKey Authorization in header

## Base URL
http://demo.akeneo.com

## Setup
1. Set your API key in the appropriate header
2. GET /api/rest/v1/products-uuid -- verify access
3. POST /api/rest/v1/products-uuid -- create first products-uuid

## Endpoints

137 endpoints across 1 groups. See references/api-spec.lap for full details.

### api
| Method | Path | Description |
|--------|------|-------------|
| GET | /api/rest/v1/products-uuid | Get list of products |
| POST | /api/rest/v1/products-uuid | Create a new product |
| PATCH | /api/rest/v1/products-uuid | Update/create several products |
| POST | /api/rest/v1/products-uuid/search | Search list of products |
| GET | /api/rest/v1/products-uuid/{uuid} | Get a product |
| PATCH | /api/rest/v1/products-uuid/{uuid} | Update/create a product |
| DELETE | /api/rest/v1/products-uuid/{uuid} | Delete a product |
| POST | /api/rest/v1/products-uuid/{uuid}/proposal | Submit a draft for approval |
| GET | /api/rest/v1/products-uuid/{uuid}/draft | Get a draft |
| GET | /api/rest/v1/products | Get list of products |
| POST | /api/rest/v1/products | Create a new product |
| PATCH | /api/rest/v1/products | Update/create several products |
| GET | /api/rest/v1/products/{code} | Get a product |
| PATCH | /api/rest/v1/products/{code} | Update/create a product |
| DELETE | /api/rest/v1/products/{code} | Delete a product |
| POST | /api/rest/v1/products/{code}/proposal | Submit a draft for approval |
| GET | /api/rest/v1/products/{code}/draft | Get a draft |
| GET | /api/rest/v1/product-models | Get list of product models |
| POST | /api/rest/v1/product-models | Create a new product model |
| PATCH | /api/rest/v1/product-models | Update/create several product models |
| GET | /api/rest/v1/product-models/{code} | Get a product model |
| PATCH | /api/rest/v1/product-models/{code} | Update/create a product model |
| DELETE | /api/rest/v1/product-models/{code} | Delete a product model |
| POST | /api/rest/v1/product-models/{code}/proposal | Submit a draft for approval |
| GET | /api/rest/v1/product-models/{code}/draft | Get a draft |
| GET | /api/rest/v1/published-products | Get list of published products |
| GET | /api/rest/v1/published-products/{code} | Get a published product |
| GET | /api/rest/v1/media-files | Get a list of product media files |
| POST | /api/rest/v1/media-files | Create a new product media file |
| GET | /api/rest/v1/media-files/{code} | Get a product media file |
| GET | /api/rest/v1/media-files/{code}/download | Download a product media file |
| POST | /api/rest/v1/jobs/export/{code} | Launch export job by code |
| POST | /api/rest/v1/jobs/import/{code} | Launch import job by code |
| GET | /api/rest/v1/families | Get list of families |
| POST | /api/rest/v1/families | Create a new family |
| PATCH | /api/rest/v1/families | Update/create several families |
| GET | /api/rest/v1/families/{code} | Get a family |
| PATCH | /api/rest/v1/families/{code} | Update/create a family |
| DELETE | /api/rest/v1/families/{code} | Delete a family |
| GET | /api/rest/v1/families/{family_code}/variants | Get list of family variants |
| POST | /api/rest/v1/families/{family_code}/variants | Create a new family variant |
| PATCH | /api/rest/v1/families/{family_code}/variants | Update/create several family variants |
| GET | /api/rest/v1/families/{family_code}/variants/{code} | Get a family variant |
| PATCH | /api/rest/v1/families/{family_code}/variants/{code} | Update/create a family variant |
| GET | /api/rest/v1/attributes | Get list of attributes |
| POST | /api/rest/v1/attributes | Create a new attribute |
| PATCH | /api/rest/v1/attributes | Update/create several attributes |
| GET | /api/rest/v1/attributes/{code} | Get an attribute |
| PATCH | /api/rest/v1/attributes/{code} | Update/create an attribute |
| GET | /api/rest/v1/attributes/{attribute_code}/options | Get list of attribute options |
| POST | /api/rest/v1/attributes/{attribute_code}/options | Create a new attribute option |
| PATCH | /api/rest/v1/attributes/{attribute_code}/options | Update/create several attribute options |
| GET | /api/rest/v1/attributes/{attribute_code}/options/{code} | Get an attribute option |
| PATCH | /api/rest/v1/attributes/{attribute_code}/options/{code} | Update/create an attribute option |
| GET | /api/rest/v1/attribute-groups | Get list of attribute groups |
| POST | /api/rest/v1/attribute-groups | Create a new attribute group |
| PATCH | /api/rest/v1/attribute-groups | Update/create several attribute groups |
| GET | /api/rest/v1/attribute-groups/{code} | Get an attribute group |
| PATCH | /api/rest/v1/attribute-groups/{code} | Update/create an attribute group |
| GET | /api/rest/v1/association-types | Get a list of association types |
| POST | /api/rest/v1/association-types | Create a new association type |
| PATCH | /api/rest/v1/association-types | Update/create several association types |
| GET | /api/rest/v1/association-types/{code} | Get an association type |
| PATCH | /api/rest/v1/association-types/{code} | Update/create an association type |
| GET | /api/rest/v1/channels | Get a list of channels |
| POST | /api/rest/v1/channels | Create a new channel |
| PATCH | /api/rest/v1/channels | Update/create several channels |
| GET | /api/rest/v1/channels/{code} | Get a channel |
| PATCH | /api/rest/v1/channels/{code} | Update/create a channel |
| GET | /api/rest/v1/locales | Get a list of locales |
| GET | /api/rest/v1/locales/{code} | Get a locale |
| GET | /api/rest/v1/categories | Get list of categories |
| POST | /api/rest/v1/categories | Create a new category |
| PATCH | /api/rest/v1/categories | Update/create several categories |
| GET | /api/rest/v1/categories/{code} | Get a category |
| PATCH | /api/rest/v1/categories/{code} | Update/create a category |
| POST | /api/rest/v1/category-media-files | Create a category media file |
| GET | /api/rest/v1/category-media-files/{file_path}/download | Download a category media file |
| GET | /api/rest/v1/currencies | Get a list of currencies |
| GET | /api/rest/v1/currencies/{code} | Get a currency |
| GET | /api/rest/v1/measure-families | Get list of measure families (deprecated as of v5.0) |
| GET | /api/rest/v1/measure-families/{code} | Get a measure family (deprecated as of v5.0) |
| GET | /api/rest/v1/measurement-families | Get list of measurement families |
| PATCH | /api/rest/v1/measurement-families | Update/create several measurement families |
| GET | /api/rest/v1/reference-entities | Get list of reference entities |
| GET | /api/rest/v1/reference-entities/{code} | Get a reference entity |
| PATCH | /api/rest/v1/reference-entities/{code} | Update/create a reference entity |
| GET | /api/rest/v1/reference-entities/{reference_entity_code}/attributes | Get the list of attributes of a given reference entity |
| GET | /api/rest/v1/reference-entities/{reference_entity_code}/attributes/{code} | Get an attribute of a given reference entity |
| PATCH | /api/rest/v1/reference-entities/{reference_entity_code}/attributes/{code} | Update/create an attribute of a given reference entity |
| GET | /api/rest/v1/reference-entities/{reference_entity_code}/attributes/{attribute_code}/options | Get a list of attribute options of a given attribute for a given reference entity |
| GET | /api/rest/v1/reference-entities/{reference_entity_code}/attributes/{attribute_code}/options/{code} | Get an attribute option for a given attribute of a given reference entity |
| PATCH | /api/rest/v1/reference-entities/{reference_entity_code}/attributes/{attribute_code}/options/{code} | Update/create a reference entity attribute option |
| GET | /api/rest/v1/reference-entities/{reference_entity_code}/records | Get the list of the records of a reference entity |
| PATCH | /api/rest/v1/reference-entities/{reference_entity_code}/records | Update/create several reference entity records |
| GET | /api/rest/v1/reference-entities/{reference_entity_code}/records/{code} | Get a record of a given reference entity |
| PATCH | /api/rest/v1/reference-entities/{reference_entity_code}/records/{code} | Update/create a record of a given reference entity |
| POST | /api/rest/v1/reference-entities-media-files | Create a new media file for a reference entity or a record |
| GET | /api/rest/v1/reference-entities-media-files/{code} | Download the media file associated to a reference entity or a record |
| GET | /api/rest/v1/asset-families | Get list of asset families |
| GET | /api/rest/v1/asset-families/{code} | Get an asset family |
| PATCH | /api/rest/v1/asset-families/{code} | Update/create an asset family |
| GET | /api/rest/v1/asset-families/{asset_family_code}/attributes | Get the list of attributes of a given asset family |
| GET | /api/rest/v1/asset-families/{asset_family_code}/attributes/{code} | Get an attribute of a given asset family |
| PATCH | /api/rest/v1/asset-families/{asset_family_code}/attributes/{code} | Update/create an attribute of a given asset family |
| GET | /api/rest/v1/asset-families/{asset_family_code}/attributes/{attribute_code}/options | Get a list of attribute options of a given attribute for a given asset family |
| GET | /api/rest/v1/asset-families/{asset_family_code}/attributes/{attribute_code}/options/{code} | Get an attribute option for a given attribute of a given asset family |
| PATCH | /api/rest/v1/asset-families/{asset_family_code}/attributes/{attribute_code}/options/{code} | Update/create an asset attribute option for a given asset family |
| POST | /api/rest/v1/asset-media-files | Create a new media file for an asset |
| GET | /api/rest/v1/asset-media-files/{code} | Download the media file associated to an asset |
| GET | /api/rest/v1/asset-families/{asset_family_code}/assets | Get the list of the assets of a given asset family |
| PATCH | /api/rest/v1/asset-families/{asset_family_code}/assets | Update/create several assets |
| GET | /api/rest/v1/asset-families/{asset_family_code}/assets/{code} | Get an asset of a given asset family |
| PATCH | /api/rest/v1/asset-families/{asset_family_code}/assets/{code} | Update/create an asset |
| DELETE | /api/rest/v1/asset-families/{asset_family_code}/assets/{code} | Delete an asset |
| GET | /api/rest/v1/assets | Get list of PAM assets |
| POST | /api/rest/v1/assets | Create a new PAM asset |
| PATCH | /api/rest/v1/assets | Update/create several PAM assets |
| GET | /api/rest/v1/assets/{code} | Get a PAM asset |
| PATCH | /api/rest/v1/assets/{code} | Update/create a PAM asset |
| GET | /api/rest/v1/assets/{asset_code}/reference-files/{locale_code} | Get a reference file |
| POST | /api/rest/v1/assets/{asset_code}/reference-files/{locale_code} | Upload a new reference file |
| GET | /api/rest/v1/assets/{asset_code}/reference-files/{locale_code}/download | Download a reference file |
| GET | /api/rest/v1/assets/{asset_code}/variation-files/{channel_code}/{locale_code} | Get a variation file |
| POST | /api/rest/v1/assets/{asset_code}/variation-files/{channel_code}/{locale_code} | Upload a new variation file |
| GET | /api/rest/v1/assets/{asset_code}/variation-files/{channel_code}/{locale_code}/download | Download a variation file |
| GET | /api/rest/v1/asset-categories | Get list of PAM asset categories |
| POST | /api/rest/v1/asset-categories | Create a new PAM asset category |
| PATCH | /api/rest/v1/asset-categories | Update/create several PAM asset categories |
| GET | /api/rest/v1/asset-categories/{code} | Get a PAM asset category |
| PATCH | /api/rest/v1/asset-categories/{code} | Update/create a PAM asset category |
| GET | /api/rest/v1/asset-tags | Get list of PAM asset tags |
| GET | /api/rest/v1/asset-tags/{code} | Get a PAM asset tag |
| PATCH | /api/rest/v1/asset-tags/{code} | Update/create a PAM asset tag |
| GET | /api/rest/v1 | Get list of all endpoints |
| POST | /api/oauth/v1/token | Get authentication token |
| GET | /api/rest/v1/system-information | Get system information |

## Enhanced Skill Content
## Question Mapping

- "How do I list all products in the catalog?" -> GET /api/rest/v1/products
- "How do I find a product by its UUID?" -> GET /api/rest/v1/products-uuid/{uuid}
- "How do I create a new product?" -> POST /api/rest/v1/products
- "How do I update multiple products at once?" -> PATCH /api/rest/v1/products
- "How do I search products with filters?" -> POST /api/rest/v1/products-uuid/search
- "What families are defined in the PIM?" -> GET /api/rest/v1/families
- "How do I get the attribute options for a select attribute?" -> GET /api/rest/v1/attributes/{attribute_code}/options
- "How do I upload a media file for a product?" -> POST /api/rest/v1/media-files
- "How do I download an asset image?" -> GET /api/rest/v1/asset-media-files/{code}
- "How do I trigger a product export job?" -> POST /api/rest/v1/jobs/export/{code}
- "How do I import a CSV file into the PIM?" -> POST /api/rest/v1/jobs/import/{code}
- "How do I authenticate and get an access token?" -> POST /api/oauth/v1/token
- "How do I submit a product draft for approval?" -> POST /api/rest/v1/products/{code}/proposal
- "What reference entities exist and how do I browse their records?" -> GET /api/rest/v1/reference-entities then GET /api/rest/v1/reference-entities/{reference_entity_code}/records
- "How do I check which version of Akeneo PIM is running?" -> GET /api/rest/v1/system-information

## Response Tips

- **Products & Product Models**: Paginated lists; use `pagination_type=search_after` for large catalogs (avoids offset limits). Quality scores and completenesses are optional nested objects -- request them explicitly via query params.
- **Families & Attributes**: Standard page-based pagination (`page`, `limit`, `with_count`). Family variants are nested under `/families/{code}/variants`.
- **Reference Entities & Assets (new system)**: Use cursor-based pagination only (`search_after`). No `page` param. Records and assets are scoped under their parent entity/family.
- **Assets (legacy)**: Support both `page` and `search_after` pagination. Reference files and variation files are locale- and channel-specific sub-resources.
- **Media Files**: `POST` returns `Location` header with the new media code -- there is no code in the response body. Download endpoints return raw binary.
- **Batch PATCH (collections)**: Returns a streaming JSON response with per-line status for each item -- parse line by line, not as a single JSON object.
- **OAuth Token**: Returns `access_token` and `refresh_token`. Token format and expiry are in the response body. 422 typically means malformed grant type.
- **Error responses**: 401 = expired/missing token, 403 = insufficient permissions, 406 = missing `Accept: application/json` header, 422 = validation failure with field-level details, 415 = wrong `Content-Type`.

## Anomaly Flags

- **429 on attribute options**: The attribute options PATCH endpoints (both collection and single) can return 429. Surface rate-limit headers proactively and suggest backing off before retrying batch option updates.
- **201 vs 204 ambiguity**: Single-resource PATCH endpoints return 201 (created) or 204 (updated). Flag when a PATCH unexpectedly creates a new resource -- the caller may have misspelled a code.
- **413 on batch operations**: Collection-level PATCH endpoints return 413 when the payload is too large. Surface this early if the request body exceeds ~100 items and recommend splitting into smaller batches.
- **406 errors on every GET**: Almost all GET endpoints error on 406, meaning the `Accept` header is wrong or missing. If a user gets repeated 406s, proactively suggest adding `Accept: application/json`.
- **422 with field details**: Validation errors include per-field messages. Surface the specific failing fields rather than just the status code.
- **Legacy vs new asset system**: The API has both `/assets` (legacy PAM) and `/asset-families/{code}/assets` (new Asset Manager). Flag if a user is mixing calls between the two systems, as they are incompatible.
- **Missing auth on write operations**: All POST/PATCH/DELETE require auth. If a 401 appears on a write, remind the user to obtain a fresh token via `/api/oauth/v1/token`.

## Playbook

### 1. Initial Setup and Authentication

1. Call `POST /api/oauth/v1/token` with your client credentials (Base64-encoded `client_id:secret` in the `Authorization` header, grant type in the body).
2. Extract `access_token` from the response.
3. Use `Authorization: Bearer {access_token}` on all subsequent requests.
4. Verify connectivity by calling `GET /api/rest/v1` (API root) or `GET /api/rest/v1/system-information`.

### 2. Bulk Product Export and Sync

1. Call `GET /api/rest/v1/products` with `pagination_type=search_after` and `limit=100`.
2. For each page, extract the `search_after` cursor from `_links.next`.
3. Repeat until no `next` link is present.
4. Optionally include `with_quality_scores=true` and `with_completenesses=true` to get enrichment status per product.
5. For large catalogs (>50k products), prefer UUID-based endpoints (`/products-uuid`) for stable identifiers.

### 3. Creating a Product with Media

1. Upload the image via `POST /api/rest/v1/media-files` with `Content-Type: multipart/form-data`. Capture the media code from the `Location` response header.
2. Create the product via `POST /api/rest/v1/products` with the media code assigned to the relevant image attribute in the body.
3. Verify by calling `GET /api/rest/v1/products/{code}` and confirming the attribute value contains the media code.

### 4. Setting Up a Product Family with Variants

1. Create the family via `POST /api/rest/v1/families` with the attribute set and attribute requirements.
2. Add a family variant via `POST /api/rest/v1/families/{family_code}/variants` defining the variant axes (e.g., size, color).
3. Create a product model via `POST /api/rest/v1/product-models` referencing the family and variant level.
4. Create variant products via `POST /api/rest/v1/products` with a `parent` field pointing to the product model code.
5. Verify the hierarchy by fetching `GET /api/rest/v1/product-models/{code}` and checking its associations.

### 5. Managing Reference Entity Records

1. List available reference entities via `GET /api/rest/v1/reference-entities` (cursor-paginated).
2. Inspect the entity structure via `GET /api/rest/v1/reference-entities/{code}` to understand its attributes.
3. List attribute definitions via `GET /api/rest/v1/reference-entities/{code}/attributes`.
4. Upsert records in bulk via `PATCH /api/rest/v1/reference-entities/{code}/records` with an array of record objects. Parse the streaming response line by line for per-record status.
5. Verify individual records via `GET /api/rest/v1/reference-entities/{code}/records/{record_code}`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
