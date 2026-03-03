---
name: meilisearch-core-api
description: "Meilisearch Core API skill. Use when working with Meilisearch Core for dumps, snapshots, health. Covers 73 endpoints."
version: 1.0.0
generator: lapsh
---

# Meilisearch Core API
API version: 1.7.0

## Auth
Bearer bearer

## Base URL
{protocol}://{domain}:{port}

## Setup
1. Set Authorization header with your Bearer token
2. GET /health -- verify access
3. POST /dumps -- create first dumps

## Endpoints

73 endpoints across 12 groups. See references/api-spec.lap for full details.

### dumps
| Method | Path | Description |
|--------|------|-------------|
| POST | /dumps | Create a Dump |

### snapshots
| Method | Path | Description |
|--------|------|-------------|
| POST | /snapshots | Create a Snapshot |

### health
| Method | Path | Description |
|--------|------|-------------|
| GET | /health | Get health |

### indexes
| Method | Path | Description |
|--------|------|-------------|
| GET | /indexes | List Indexes |
| POST | /indexes | Create Index |
| GET | /indexes/{indexUid} | Get Index |
| PATCH | /indexes/{indexUid} | Update Index |
| DELETE | /indexes/{indexUid} | Delete Index |
| GET | /indexes/{indexUid}/documents | Get Documents |
| POST | /indexes/{indexUid}/documents | Add or replace documents |
| PUT | /indexes/{indexUid}/documents | Add or update documents |
| DELETE | /indexes/{indexUid}/documents | Delete all documents |
| POST | /indexes/{indexUid}/documents/fetch | Get Documents |
| POST | /indexes/{indexUid}/documents/delete-batch | Delete documents |
| POST | /indexes/{indexUid}/documents/delete | Delete documents |
| GET | /indexes/{indexUid}/documents/{documentId} | Get one document |
| DELETE | /indexes/{indexUid}/documents/{documentId} | Delete one document |
| GET | /indexes/{indexUid}/search | Search |
| POST | /indexes/{indexUid}/search | Search |
| POST | /indexes/{indexUid}/facet-search | Facet Search |
| GET | /indexes/{indexUid}/settings | Get settings |
| PATCH | /indexes/{indexUid}/settings | Update settings |
| DELETE | /indexes/{indexUid}/settings | Reset settings |
| GET | /indexes/{indexUid}/settings/synonyms | Get synonyms |
| PUT | /indexes/{indexUid}/settings/synonyms | Update synonyms |
| DELETE | /indexes/{indexUid}/settings/synonyms | Reset synonyms |
| GET | /indexes/{indexUid}/settings/sortable-attributes | Get sortable attributes |
| PUT | /indexes/{indexUid}/settings/sortable-attributes | Update sortable attributes |
| DELETE | /indexes/{indexUid}/settings/sortable-attributes | Reset sortable attributes |
| GET | /indexes/{indexUid}/settings/stop-words | Get stop-words |
| PUT | /indexes/{indexUid}/settings/stop-words | Update stop-words |
| DELETE | /indexes/{indexUid}/settings/stop-words | Reset stop-words |
| GET | /indexes/{indexUid}/settings/ranking-rules | Get ranking rules |
| PUT | /indexes/{indexUid}/settings/ranking-rules | Update ranking rules |
| DELETE | /indexes/{indexUid}/settings/ranking-rules | Reset ranking rules |
| GET | /indexes/{indexUid}/settings/typo-tolerance | Get typo tolerance configuration |
| PATCH | /indexes/{indexUid}/settings/typo-tolerance | Update typo tolerance settings |
| DELETE | /indexes/{indexUid}/settings/typo-tolerance | Reset typo tolerance settings to the default configuration |
| GET | /indexes/{indexUid}/settings/pagination | Get pagination configuration |
| PATCH | /indexes/{indexUid}/settings/pagination | Update pagination settings |
| DELETE | /indexes/{indexUid}/settings/pagination | Reset pagination settings to the default configuration |
| GET | /indexes/{indexUid}/settings/faceting | Get faceting configuration |
| PATCH | /indexes/{indexUid}/settings/faceting | Update faceting settings |
| DELETE | /indexes/{indexUid}/settings/faceting | Reset faceting settings to the default configuration |
| GET | /indexes/{indexUid}/settings/filterable-attributes | Get Filterable Attributes |
| PUT | /indexes/{indexUid}/settings/filterable-attributes | Update Filterable Attributes |
| DELETE | /indexes/{indexUid}/settings/filterable-attributes | Reset Filterable Attributes |
| GET | /indexes/{indexUid}/settings/distinct-attribute | Get distinct attribute |
| PUT | /indexes/{indexUid}/settings/distinct-attribute | Update distinct attribute |
| DELETE | /indexes/{indexUid}/settings/distinct-attribute | Reset distinct attribute |
| GET | /indexes/{indexUid}/settings/searchable-attributes | Get searchable attributes |
| PUT | /indexes/{indexUid}/settings/searchable-attributes | Update searchable attributes |
| DELETE | /indexes/{indexUid}/settings/searchable-attributes | Reset searchable attributes |
| GET | /indexes/{indexUid}/settings/displayed-attributes | Get displayed attributes |
| PUT | /indexes/{indexUid}/settings/displayed-attributes | Update displayed attributes |
| DELETE | /indexes/{indexUid}/settings/displayed-attributes | Reset displayed attributes |
| GET | /indexes/{indexUid}/stats | Get stat of an index |

### multi-search
| Method | Path | Description |
|--------|------|-------------|
| POST | /multi-search | Multi Search |

### keys
| Method | Path | Description |
|--------|------|-------------|
| GET | /keys | Get API Keys |
| POST | /keys | Create an API Key |
| GET | /keys/{uid_or_key} | Get an API key from its uid or key field. |
| DELETE | /keys/{uid_or_key} | Delete an API key specified by its uid or key field. |
| PATCH | /keys/{uid_or_key} | Update an API key specified by its uid or key field. |

### stats
| Method | Path | Description |
|--------|------|-------------|
| GET | /stats | Get stats of all indexes |

### version
| Method | Path | Description |
|--------|------|-------------|
| GET | /version | Get version of Meilisearch |

### tasks
| Method | Path | Description |
|--------|------|-------------|
| GET | /tasks | Get all tasks |
| DELETE | /tasks | Delete tasks |
| GET | /tasks/:taskUid | Get a task |
| POST | /tasks/cancel | Cancel tasks |

### swap-indexes
| Method | Path | Description |
|--------|------|-------------|
| POST | /swap-indexes | Swap Indexes |

### experimental-features
| Method | Path | Description |
|--------|------|-------------|
| GET | /experimental-features | (EXPERIMENTAL) Get the status of runtime experimental features |
| PATCH | /experimental-features | (EXPERIMENTAL) Set the status of runtime experimental features |

### metrics
| Method | Path | Description |
|--------|------|-------------|
| GET | /metrics | (EXPERIMENTAL) Get prometheus format metrics for observability and monitoring |

## Enhanced Skill Content
## Question Mapping

- "Is Meilisearch running?" -> GET /health
- "What indexes exist?" -> GET /indexes
- "How do I create a new index?" -> POST /indexes
- "How do I search for documents?" -> POST /indexes/{indexUid}/search
- "How do I add documents to an index?" -> POST /indexes/{indexUid}/documents
- "What is the status of my task?" -> GET /tasks/:taskUid
- "How do I delete an index?" -> DELETE /indexes/{indexUid}
- "How do I filter search results by a field?" -> POST /indexes/{indexUid}/search (set `filter` and ensure field is in filterable-attributes)
- "How do I search across multiple indexes at once?" -> POST /multi-search
- "How do I create an API key with limited permissions?" -> POST /keys
- "What are the current settings for my index?" -> GET /indexes/{indexUid}/settings
- "How do I make a field sortable?" -> PUT /indexes/{indexUid}/settings/sortable-attributes
- "How do I get facet counts for a search?" -> POST /indexes/{indexUid}/search (include `facets` parameter)
- "How do I cancel a running task?" -> POST /tasks/cancel
- "How do I swap two indexes with zero downtime?" -> POST /swap-indexes

## Response Tips

- **Search endpoints**: `estimatedTotalHits` is approximate when using offset/limit pagination; switch to `page`/`hitsPerPage` for exact `totalHits` and `totalPages`. Check `processingTimeMs` for performance.
- **List endpoints** (indexes, documents, keys): All return `{results, limit, offset, total}` -- paginate by incrementing `offset` by `limit` until `offset >= total`.
- **Tasks**: Use `from`/`next` cursor pagination (not offset). The `next` field gives the `from` value for the next page; `null` means no more results. Task `status` is one of: `enqueued`, `processing`, `succeeded`, `failed`, `canceled`.
- **Write operations**: Nearly all mutating endpoints return `202 Accepted` with a `taskUid` -- the operation is async. Always poll `GET /tasks/:taskUid` to confirm completion.
- **Errors**: All errors return `{message, code, type, link}`. The `link` field points to Meilisearch docs for that specific error code.
- **Keys**: `POST /keys` returns `200` (not `202`) because key creation is synchronous, unlike index/document operations.

## Anomaly Flags

- **202 without follow-up**: Any write operation returns a `taskUid` -- surface a reminder to poll the task status if the caller does not check it.
- **Task failures**: When polling a task, flag `status: "failed"` immediately and extract `error.message` and `error.code` for the user.
- **Index not found (404)**: Common when the `indexUid` is misspelled or the index creation task has not completed yet. Suggest checking pending tasks.
- **413 Payload Too Large**: Returned when document batch exceeds the configured limit. Suggest splitting the payload into smaller batches.
- **Slow search**: If `processingTimeMs` exceeds 500ms, suggest reviewing ranking rules, filterable attributes, and dataset size.
- **Pagination ceiling**: The default `maxTotalHits` is 1000. If users report missing results beyond offset 1000, surface that the pagination setting needs updating via `PATCH /indexes/{indexUid}/settings/pagination`.
- **Experimental features enabled**: Flag when `vectorStore` or `exportPuffinReports` is enabled, as these may change or be removed in future versions.
- **Key expiration**: When listing or inspecting API keys, flag any key where `expiresAt` is approaching or already past.

## Playbook

### 1. Set Up a New Searchable Index

1. `POST /indexes` with `{"uid": "movies", "primaryKey": "id"}` -- note the returned `taskUid`
2. `GET /tasks/:taskUid` -- poll until `status` is `succeeded`
3. `PUT /indexes/movies/settings/filterable-attributes` with `["genre", "year"]`
4. `PUT /indexes/movies/settings/sortable-attributes` with `["year", "rating"]`
5. `POST /indexes/movies/documents` with your JSON document array
6. `GET /tasks/:taskUid` -- poll the document indexing task until `succeeded`
7. `POST /indexes/movies/search` with `{"q": "test"}` to verify

### 2. Perform a Filtered, Faceted Search

1. Confirm the field is filterable: `GET /indexes/{indexUid}/settings/filterable-attributes`
2. If not listed, add it: `PUT /indexes/{indexUid}/settings/filterable-attributes` and wait for the task to complete
3. `POST /indexes/{indexUid}/search` with `{"q": "action", "filter": "year > 2020", "facets": ["genre"], "sort": ["rating:desc"], "limit": 10}`
4. Read `facetDistribution` from the response for sidebar counts
5. Paginate with `page` and `hitsPerPage` for exact total counts

### 3. Zero-Downtime Index Rebuild

1. `POST /indexes` to create a temporary index (e.g., `movies-v2`) with the same primary key
2. Configure settings on `movies-v2` to match production: `PATCH /indexes/movies-v2/settings`
3. `POST /indexes/movies-v2/documents` -- index the full updated dataset
4. Poll the task until `succeeded`
5. `POST /swap-indexes` with `[{"indexes": ["movies", "movies-v2"]}]` -- atomic swap
6. Poll the swap task until `succeeded`
7. `DELETE /indexes/movies-v2` to clean up the old data (now in the temp name)

### 4. Manage API Keys with Least Privilege

1. `GET /keys` to list existing keys and audit their `actions` and `indexes` scopes
2. `POST /keys` with `{"actions": ["search"], "indexes": ["movies"], "expiresAt": "2027-01-01T00:00:00Z", "description": "Frontend search only"}` for a read-only key
3. Store the returned `key` value securely -- it cannot be retrieved again
4. To rotate: create a new key, update clients, then `DELETE /keys/{uid_or_key}` the old one

### 5. Monitor and Troubleshoot Async Operations

1. `GET /tasks?statuses=failed&limit=5` to find recent failures
2. For each failed task, inspect `error.code` and `error.message` for root cause
3. `GET /tasks?statuses=processing` to check for long-running tasks that may be blocking the queue
4. `POST /tasks/cancel?statuses=enqueued&beforeEnqueuedAt=2026-01-01T00:00:00Z` to clear stale queued tasks
5. `DELETE /tasks?statuses=succeeded,canceled&beforeFinishedAt=2026-01-01T00:00:00Z` to clean up old task history


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
