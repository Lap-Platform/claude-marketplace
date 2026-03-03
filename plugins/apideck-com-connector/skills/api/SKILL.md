---
name: connector-api
description: "Connector API skill. Use when working with Connector for connector. Covers 10 endpoints."
version: 1.0.0
generator: lapsh
---

# Connector API
API version: 10.24.0

## Auth
ApiKey Authorization in header

## Base URL
https://unify.apideck.com

## Setup
1. Set your API key in the appropriate header
2. GET /connector/connectors -- verify access

## Endpoints

10 endpoints across 1 groups. See references/api-spec.lap for full details.

### connector
| Method | Path | Description |
|--------|------|-------------|
| GET | /connector/connectors | List Connectors |
| GET | /connector/connectors/{id} | Get Connector |
| GET | /connector/connectors/{id}/docs/{doc_id} | Get Connector Doc content |
| GET | /connector/connectors/{id}/resources/{resource_id} | Get Connector Resource |
| GET | /connector/connectors/{id}/resources/{resource_id}/unified_api/{api_id}/schema | Get Connector Resource Schema |
| GET | /connector/connectors/{id}/resources/{resource_id}/unified_api/{api_id}/example | Get Connector Resource Example |
| GET | /connector/apis | List APIs |
| GET | /connector/apis/{id} | Get API |
| GET | /connector/apis/{id}/resources/{resource_id} | Get API Resource |
| GET | /connector/apis/{id}/resources/{resource_id}/coverage | Get API Resource Coverage |

## Enhanced Skill Content
## Question Mapping

- "What connectors are available?" -> GET /connector/connectors
- "Show me details for the Salesforce connector" -> GET /connector/connectors/{id}
- "What authentication type does a connector use?" -> GET /connector/connectors/{id}
- "What resources does a connector support?" -> GET /connector/connectors/{id}
- "How do I paginate through the connector list?" -> GET /connector/connectors with cursor and limit params
- "Where can I find documentation for a specific connector?" -> GET /connector/connectors/{id}/docs/{doc_id}
- "What operations are supported for a connector's resource?" -> GET /connector/connectors/{id}/resources/{resource_id}
- "What does the schema look like for a connector resource in a unified API?" -> GET /connector/connectors/{id}/resources/{resource_id}/unified_api/{api_id}/schema
- "Can I see an example response for a connector resource?" -> GET /connector/connectors/{id}/resources/{resource_id}/unified_api/{api_id}/example
- "What unified APIs are available?" -> GET /connector/apis
- "What categories does a unified API belong to?" -> GET /connector/apis/{id}
- "What resources exist under a specific unified API?" -> GET /connector/apis/{id}/resources/{resource_id}
- "Which connectors cover a particular API resource?" -> GET /connector/apis/{id}/resources/{resource_id}/coverage
- "Does a connector support webhooks?" -> GET /connector/connectors/{id} (check webhook_support field)
- "Is a free trial available for a connector?" -> GET /connector/connectors/{id} (check free_trial_available field)

## Response Tips

- **Connector/API listings**: Paginated via cursor-based pagination. Check `meta.cursors.next` for more pages; pass it as `cursor` param on the next request. Default page size is 20.
- **Detail endpoints**: Single object in `data`; look for nested maps like `unified_apis`, `supported_resources`, and `settings` which contain integration-specific configuration.
- **Resource endpoints**: `supported_operations` is an array of strings (e.g., create, read, update, delete); `supported_fields` and `supported_list_fields` are arrays of maps with field-level metadata.
- **Example/Schema endpoints**: `data` contains raw schema or example maps; no pagination. The example endpoint includes `workflow_examples` for multi-step usage patterns.
- **Errors**: 400 = bad filter/params (list endpoints only), 401 = missing or invalid API key, 402 = plan limit reached, 404 = entity not found.

## Anomaly Flags

- **402 Payment Required**: Surface immediately -- indicates the account has hit plan limits. Recommend the user check their Apideck subscription.
- **Connector status not "live"**: When `data.status` is anything other than `live` (e.g., `beta`, `deprecated`), warn the user that the connector may have limited support or be removed.
- **auth_only connectors**: If `data.auth_only` is true, flag that the connector only supports authentication and not data operations.
- **Empty supported_operations**: If a resource returns an empty `supported_operations` array, warn that no CRUD operations are available for that resource.
- **Pagination exhaustion**: If `meta.cursors.next` is null on the first page and `items_on_page` equals the limit, there may be exactly one page -- but confirm by noting the total is absent (this API has no total count field).
- **Deprecated or missing docs**: If `docs` array on a connector is empty, surface that no documentation links are available.
- **Virtual webhooks with rate limits**: When `webhook_support.virtual_webhooks.request_rate` is populated, flag the polling rate constraints to the user.

## Playbook

### 1. Discover and evaluate a connector

1. `GET /connector/connectors` to browse available connectors (use `filter` to narrow by name or category).
2. Pick a connector and `GET /connector/connectors/{id}` to see auth type, supported unified APIs, webhook support, and whether a free trial is available.
3. Review `unified_apis` array in the response to understand which API categories (CRM, HRIS, etc.) the connector covers.
4. Check `supported_resources` to see which data objects are available.

### 2. Inspect resource capabilities before integration

1. `GET /connector/connectors/{id}` to get the list of `supported_resources`.
2. For each resource of interest, `GET /connector/connectors/{id}/resources/{resource_id}` to check `supported_operations`, `supported_filters`, and `supported_sort_by`.
3. Fetch the schema with `GET /connector/connectors/{id}/resources/{resource_id}/unified_api/{api_id}/schema` to understand field types.
4. Fetch an example with `GET /connector/connectors/{id}/resources/{resource_id}/unified_api/{api_id}/example` to see a realistic response shape and workflow examples.

### 3. Audit API coverage across connectors

1. `GET /connector/apis` to list all unified APIs.
2. `GET /connector/apis/{id}` to see the resources and events for a specific API.
3. `GET /connector/apis/{id}/resources/{resource_id}` to inspect the resource schema and linked resources.
4. `GET /connector/apis/{id}/resources/{resource_id}/coverage` to see which connectors implement that resource and their coverage level.
5. Compare the `coverage` array entries to decide which connector best fits your needs.

### 4. Page through all connectors programmatically

1. `GET /connector/connectors?limit=20` to fetch the first page.
2. Read `meta.cursors.next` from the response.
3. If `next` is not null, `GET /connector/connectors?limit=20&cursor={next}`.
4. Repeat until `meta.cursors.next` is null.
5. Note: always include the `x-apideck-app-id` header on every request.

### 5. Look up connector documentation

1. `GET /connector/connectors/{id}` to retrieve connector details.
2. Inspect the `docs` array in the response -- each entry has an `id` and metadata.
3. `GET /connector/connectors/{id}/docs/{doc_id}` to fetch the full documentation content for a specific doc entry.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
