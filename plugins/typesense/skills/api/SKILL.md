---
name: typesense-api
description: "Typesense API skill. Use when working with Typesense for collections, synonym_sets, curation_sets. Covers 79 endpoints."
version: 1.0.0
generator: lapsh
---

# Typesense API
API version: 30.0

## Auth
ApiKey X-TYPESENSE-API-KEY in header

## Base URL
{protocol}://{hostname}:{port}

## Setup
1. Set your API key in the appropriate header
2. GET /collections -- verify access
3. POST /collections -- create first collections

## Endpoints

79 endpoints across 18 groups. See references/api-spec.lap for full details.

### collections
| Method | Path | Description |
|--------|------|-------------|
| GET | /collections | List all collections |
| POST | /collections | Create a new collection |
| GET | /collections/{collectionName} | Retrieve a single collection |
| PATCH | /collections/{collectionName} | Update a collection |
| DELETE | /collections/{collectionName} | Delete a collection |
| POST | /collections/{collectionName}/documents | Index a document |
| PATCH | /collections/{collectionName}/documents | Update documents with conditional query |
| DELETE | /collections/{collectionName}/documents | Delete a bunch of documents |
| GET | /collections/{collectionName}/documents/search | Search for documents in a collection |
| GET | /collections/{collectionName}/documents/export | Export all documents in a collection |
| POST | /collections/{collectionName}/documents/import | Import documents into a collection |
| GET | /collections/{collectionName}/documents/{documentId} | Retrieve a document |
| PATCH | /collections/{collectionName}/documents/{documentId} | Update a document |
| DELETE | /collections/{collectionName}/documents/{documentId} | Delete a document |

### synonym_sets
| Method | Path | Description |
|--------|------|-------------|
| GET | /synonym_sets | List all synonym sets |
| GET | /synonym_sets/{synonymSetName} | Retrieve a synonym set |
| PUT | /synonym_sets/{synonymSetName} | Create or update a synonym set |
| DELETE | /synonym_sets/{synonymSetName} | Delete a synonym set |
| GET | /synonym_sets/{synonymSetName}/items | List items in a synonym set |
| GET | /synonym_sets/{synonymSetName}/items/{itemId} | Retrieve a synonym set item |
| PUT | /synonym_sets/{synonymSetName}/items/{itemId} | Create or update a synonym set item |
| DELETE | /synonym_sets/{synonymSetName}/items/{itemId} | Delete a synonym set item |

### curation_sets
| Method | Path | Description |
|--------|------|-------------|
| GET | /curation_sets | List all curation sets |
| GET | /curation_sets/{curationSetName} | Retrieve a curation set |
| PUT | /curation_sets/{curationSetName} | Create or update a curation set |
| DELETE | /curation_sets/{curationSetName} | Delete a curation set |
| GET | /curation_sets/{curationSetName}/items | List items in a curation set |
| GET | /curation_sets/{curationSetName}/items/{itemId} | Retrieve a curation set item |
| PUT | /curation_sets/{curationSetName}/items/{itemId} | Create or update a curation set item |
| DELETE | /curation_sets/{curationSetName}/items/{itemId} | Delete a curation set item |

### conversations
| Method | Path | Description |
|--------|------|-------------|
| GET | /conversations/models | List all conversation models |
| POST | /conversations/models | Create a conversation model |
| GET | /conversations/models/{modelId} | Retrieve a conversation model |
| PUT | /conversations/models/{modelId} | Update a conversation model |
| DELETE | /conversations/models/{modelId} | Delete a conversation model |

### keys
| Method | Path | Description |
|--------|------|-------------|
| GET | /keys | Retrieve (metadata about) all keys. |
| POST | /keys | Create an API Key |
| GET | /keys/{keyId} | Retrieve (metadata about) a key |
| DELETE | /keys/{keyId} | Delete an API key given its ID. |

### aliases
| Method | Path | Description |
|--------|------|-------------|
| GET | /aliases | List all aliases |
| PUT | /aliases/{aliasName} | Create or update a collection alias |
| GET | /aliases/{aliasName} | Retrieve an alias |
| DELETE | /aliases/{aliasName} | Delete an alias |

### debug
| Method | Path | Description |
|--------|------|-------------|
| GET | /debug | Print debugging information |

### health
| Method | Path | Description |
|--------|------|-------------|
| GET | /health | Checks if Typesense server is ready to accept requests. |

### operations
| Method | Path | Description |
|--------|------|-------------|
| GET | /operations/schema_changes | Get the status of in-progress schema change operations |
| POST | /operations/snapshot | Creates a point-in-time snapshot of a Typesense node's state and data in the specified directory. |
| POST | /operations/vote | Triggers a follower node to initiate the raft voting process, which triggers leader re-election. |
| POST | /operations/cache/clear | Clear the cached responses of search requests in the LRU cache. |
| POST | /operations/db/compact | Compacting the on-disk database |

### config
| Method | Path | Description |
|--------|------|-------------|
| POST | /config | Toggle Slow Request Log |

### multi_search
| Method | Path | Description |
|--------|------|-------------|
| POST | /multi_search | send multiple search requests in a single HTTP request |

### analytics
| Method | Path | Description |
|--------|------|-------------|
| POST | /analytics/events | Create an analytics event |
| GET | /analytics/events | Retrieve analytics events |
| POST | /analytics/flush | Flush in-memory analytics to disk |
| GET | /analytics/status | Get analytics subsystem status |
| POST | /analytics/rules | Create analytics rule(s) |
| GET | /analytics/rules | Retrieve analytics rules |
| PUT | /analytics/rules/{ruleName} | Upserts an analytics rule |
| GET | /analytics/rules/{ruleName} | Retrieves an analytics rule |
| DELETE | /analytics/rules/{ruleName} | Delete an analytics rule |

### metrics.json
| Method | Path | Description |
|--------|------|-------------|
| GET | /metrics.json | Get current RAM, CPU, Disk & Network usage metrics. |

### stats.json
| Method | Path | Description |
|--------|------|-------------|
| GET | /stats.json | Get stats about API endpoints. |

### stopwords
| Method | Path | Description |
|--------|------|-------------|
| GET | /stopwords | Retrieves all stopwords sets. |
| PUT | /stopwords/{setId} | Upserts a stopwords set. |
| GET | /stopwords/{setId} | Retrieves a stopwords set. |
| DELETE | /stopwords/{setId} | Delete a stopwords set. |

### presets
| Method | Path | Description |
|--------|------|-------------|
| GET | /presets | Retrieves all presets. |
| GET | /presets/{presetId} | Retrieves a preset. |
| PUT | /presets/{presetId} | Upserts a preset. |
| DELETE | /presets/{presetId} | Delete a preset. |

### stemming
| Method | Path | Description |
|--------|------|-------------|
| GET | /stemming/dictionaries | List all stemming dictionaries |
| GET | /stemming/dictionaries/{dictionaryId} | Retrieve a stemming dictionary |
| POST | /stemming/dictionaries/import | Import a stemming dictionary |

### nl_search_models
| Method | Path | Description |
|--------|------|-------------|
| GET | /nl_search_models | List all NL search models |
| POST | /nl_search_models | Create a NL search model |
| GET | /nl_search_models/{modelId} | Retrieve a NL search model |
| PUT | /nl_search_models/{modelId} | Update a NL search model |
| DELETE | /nl_search_models/{modelId} | Delete a NL search model |

## Enhanced Skill Content
## Question Mapping

- "How do I search for documents in a collection?" -> GET /collections/{collectionName}/documents/search
- "How do I create a new collection with specific fields?" -> POST /collections
- "How do I add a document to my collection?" -> POST /collections/{collectionName}/documents
- "How do I bulk import documents?" -> POST /collections/{collectionName}/documents/import
- "How do I delete documents matching a filter?" -> DELETE /collections/{collectionName}/documents
- "How do I update a specific document by ID?" -> PATCH /collections/{collectionName}/documents/{documentId}
- "How do I create a scoped API key for a single collection?" -> POST /keys
- "How do I set up an alias so I can swap collections without downtime?" -> PUT /aliases/{aliasName}
- "How do I run multiple searches in one request?" -> POST /multi_search
- "How do I check if my Typesense server is healthy?" -> GET /health
- "How do I add synonyms so 'sneakers' matches 'shoes'?" -> PUT /synonym_sets/{synonymSetName}/items/{itemId}
- "How do I pin or hide specific results for a query?" -> PUT /curation_sets/{curationSetName}/items/{itemId}
- "How do I track which searches return no results?" -> POST /analytics/rules + GET /analytics/status
- "How do I export all documents from a collection?" -> GET /collections/{collectionName}/documents/export
- "How do I see server performance metrics like latency and throughput?" -> GET /stats.json

## Response Tips

- **Search**: `hits` array contains matched documents; check `found` for total count, `search_cutoff` for incomplete scans, and `facet_counts` for drill-down values. Paginate with `page` and `per_page` in request params.
- **Collections**: Returns the full schema on create/get/update; `fields` array describes every indexed attribute. 409 means a collection with that name already exists.
- **Documents**: Import returns one JSONL line per document (success or error); parse each line individually. Bulk update/delete return `num_updated`/`num_deleted` counts.
- **Multi-search**: `results` is an array matching the order of your `searches` input; each element mirrors a single search response. Check each result independently for errors.
- **Keys**: POST returns the full key value only once at creation time; subsequent GET calls return a prefix-only version. Store the key immediately.
- **Analytics**: `events` responses use flat maps; `status` shows queue depths as integers -- zero values indicate the pipeline is caught up.
- **Operations**: All operation endpoints return `{success: bool}`; a 200 with `success: false` is possible and should be treated as a failure.

## Anomaly Flags

- **Search cutoff detected**: Surface `search_cutoff: true` in search responses -- indicates the query timed out before scanning all documents, results may be incomplete.
- **Overloaded server**: Flag `overloaded_requests_per_second > 0` from `/stats.json` -- the node is rejecting requests under load.
- **Pending write batches**: Alert when `pending_write_batches` from `/stats.json` grows steadily -- write pressure is outpacing disk flushes.
- **Import partial failures**: When `/documents/import` returns 200, individual lines may still contain errors; scan each JSONL line for `success: false`.
- **API key expiration**: Keys accept `expires_at` (epoch timestamp); proactively warn when a key used in the current session is within 24 hours of expiry.
- **Health degraded**: If `GET /health` returns `ok: false` or a non-200 status, surface immediately -- the node may be unresponsive or partitioned.
- **Collection conflict (409)**: When creating a collection, a 409 means the name is taken; suggest checking existing collections or using an alias for zero-downtime swaps.
- **Slow request logging**: If `POST /config` has been used to set `log-slow-requests-time-ms`, remind the user to check server logs for flagged queries.

## Playbook

### 1. Create a Collection and Index Documents

1. POST /collections with `name`, `fields` (define at least one field with `name` and `type`), and optionally `default_sorting_field`
2. Verify creation with GET /collections/{collectionName} to confirm the schema
3. POST /collections/{collectionName}/documents/import with JSONL body and `action=create` to bulk-load documents
4. Parse each response line to confirm all rows succeeded; retry any with `success: false`
5. GET /collections/{collectionName}/documents/search with `q=*` to verify documents are indexed

### 2. Zero-Downtime Collection Swap via Aliases

1. POST /collections to create a new collection (e.g., `products_v2`) with the updated schema
2. POST /collections/products_v2/documents/import to load data into the new collection
3. GET /collections/products_v2/documents/search to validate search quality on the new collection
4. PUT /aliases/{aliasName} with `collection_name: "products_v2"` to atomically point the alias to the new collection
5. DELETE /collections/{oldCollectionName} to remove the previous collection once traffic has shifted

### 3. Set Up Search Analytics and Curation

1. POST /analytics/rules to create a rule that captures search queries into a destination analytics collection
2. Wait for query volume to accumulate, then GET /analytics/status to confirm events are flowing
3. GET /analytics/events with `user_id` and `name` to review popular and no-result queries
4. PUT /curation_sets/{curationSetName} to create a curation set with pinned (`includes`) and hidden (`excludes`) results for problem queries
5. Verify by running GET /collections/{collectionName}/documents/search with the curated query term and confirming promoted results appear at expected positions

### 4. Configure Synonyms for Better Recall

1. PUT /synonym_sets/{synonymSetName} to create a named synonym set with an empty or initial items list
2. PUT /synonym_sets/{synonymSetName}/items/{itemId} with `synonyms: ["sneakers", "shoes", "trainers"]` to add a multi-way synonym group
3. For one-way synonyms, include `root: "footwear"` so that "footwear" expands to the synonyms but not vice versa
4. PATCH /collections/{collectionName} with `synonym_sets: ["{synonymSetName}"]` to attach the set to a collection
5. Test with GET /collections/{collectionName}/documents/search using one of the synonym terms and confirm expanded results

### 5. Create Scoped API Keys for Frontend Search

1. GET /keys to review existing keys and their scopes
2. POST /keys with `actions: ["documents:search"]`, `collections: ["products"]`, and `description: "Frontend search-only"` to create a restricted key
3. Optionally set `expires_at` to an epoch timestamp for automatic expiration
4. Store the returned key value immediately (it is only shown once at creation time)
5. Use the scoped key in your frontend client; if it leaks, DELETE /keys/{keyId} to revoke and POST /keys to issue a replacement


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
