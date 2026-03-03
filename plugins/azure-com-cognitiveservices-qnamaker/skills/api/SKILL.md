---
name: qnamaker-client
description: "QnAMaker Client API skill. Use when working with QnAMaker Client for endpointSettings, endpointkeys, alterations. Covers 15 endpoints."
version: 1.0.0
generator: lapsh
---

# QnAMaker Client
API version: 4.0

## Auth
ApiKey Ocp-Apim-Subscription-Key in header

## Base URL
Not specified.

## Setup
1. Set your API key in the appropriate header
2. GET /endpointSettings -- verify access
3. POST /knowledgebases/{kbId} -- create first knowledgebases

## Endpoints

15 endpoints across 5 groups. See references/api-spec.lap for full details.

### endpointSettings
| Method | Path | Description |
|--------|------|-------------|
| GET | /endpointSettings | Gets endpoint settings for an endpoint. |
| PATCH | /endpointSettings | Updates endpoint settings for an endpoint. |

### endpointkeys
| Method | Path | Description |
|--------|------|-------------|
| GET | /endpointkeys | Gets endpoint keys for an endpoint |
| PATCH | /endpointkeys/{keyType} | Re-generates an endpoint key. |

### alterations
| Method | Path | Description |
|--------|------|-------------|
| GET | /alterations | Download alterations from runtime. |
| PUT | /alterations | Replace alterations data. |

### knowledgebases
| Method | Path | Description |
|--------|------|-------------|
| GET | /knowledgebases | Gets all knowledgebases for a user. |
| GET | /knowledgebases/{kbId} | Gets details of a specific knowledgebase. |
| DELETE | /knowledgebases/{kbId} | Deletes the knowledgebase and all its data. |
| POST | /knowledgebases/{kbId} | Publishes all changes in test index of a knowledgebase to its prod index. |
| PUT | /knowledgebases/{kbId} | Replace knowledgebase contents. |
| PATCH | /knowledgebases/{kbId} | Asynchronous operation to modify a knowledgebase. |
| POST | /knowledgebases/create | Asynchronous operation to create a new knowledgebase. |
| GET | /knowledgebases/{kbId}/{environment}/qna | Download the knowledgebase. |

### operations
| Method | Path | Description |
|--------|------|-------------|
| GET | /operations/{operationId} | Gets details of a specific long running operation. |

## Enhanced Skill Content
## Question Mapping

- "What are my current endpoint settings?" -> GET /endpointSettings
- "How do I enable active learning for my QnA service?" -> PATCH /endpointSettings
- "What are my endpoint keys?" -> GET /endpointkeys
- "How do I refresh or rotate an endpoint key?" -> PATCH /endpointkeys/{keyType}
- "What word alterations (synonyms) are configured?" -> GET /alterations
- "How do I add synonym mappings to improve matching?" -> PUT /alterations
- "List all my knowledgebases." -> GET /knowledgebases
- "Get details for a specific knowledgebase." -> GET /knowledgebases/{kbId}
- "How do I create a new knowledgebase?" -> POST /knowledgebases/create
- "How do I add QnA pairs or URLs to an existing knowledgebase?" -> PATCH /knowledgebases/{kbId}
- "How do I fully replace a knowledgebase's content?" -> PUT /knowledgebases/{kbId}
- "How do I delete a knowledgebase?" -> DELETE /knowledgebases/{kbId}
- "How do I publish a knowledgebase to production?" -> POST /knowledgebases/{kbId}
- "How do I download QnA pairs from test or prod?" -> GET /knowledgebases/{kbId}/{environment}/qna
- "How do I check the status of a long-running operation?" -> GET /operations/{operationId}

## Response Tips

- **endpointSettings**: Returns a flat settings object. A 204 on PATCH means success with no body -- do not attempt to parse a response.
- **endpointkeys**: GET returns `primaryEndpointKey` and `secondaryEndpointKey`. After PATCH rotation, the new key is in the response -- capture it immediately.
- **alterations**: GET returns a `wordAlterations` array of `{alterations: string[]}` groups. PUT replaces all alterations wholesale -- always GET first to avoid data loss.
- **knowledgebases**: GET list returns `{knowledgebases: [...]}` wrapper. Individual GET returns the KB object directly. Look for `lastChangedTimestamp` and `lastPublishedTimestamp` to gauge freshness.
- **knowledgebases (mutating)**: PATCH returns 202 with an `Operation-Location` header -- you must poll that operation to confirm completion. PUT/POST/{kbId} return 204 (synchronous). POST /create returns 202 with operation tracking.
- **operations**: The `operationState` field cycles through `NotStarted` -> `Running` -> `Succeeded`/`Failed`. Check `errorResponse` when state is `Failed`.
- **knowledgebases QnA download**: Filter with `source` and `changedSince` query params to avoid pulling the entire corpus. The `environment` path param must be `test` or `prod`.

## Anomaly Flags

- **202 without polling**: If a PATCH or POST returns 202, always extract the `Operation-Location` header and poll GET /operations/{operationId}. Surface a warning if the caller ignores it.
- **Operation stuck or failed**: If polling shows `operationState` remains `Running` beyond 5 minutes, or transitions to `Failed`, surface the `errorResponse.message` immediately.
- **Empty knowledgebase list**: If GET /knowledgebases returns an empty array, flag this -- the user may be hitting the wrong subscription or region.
- **Key rotation without capture**: After PATCH /endpointkeys, if the new key value is not stored or acknowledged, warn that the old key is now invalid and requests will start failing.
- **Alterations full replacement**: Surface a confirmation before PUT /alterations since it replaces all synonyms. A partial update is not supported by this endpoint.
- **Stale publish state**: If `lastChangedTimestamp` is significantly after `lastPublishedTimestamp`, flag that the production endpoint is serving outdated content.
- **Auth errors (401/403)**: The `Ocp-Apim-Subscription-Key` header is required on every call. Surface clear guidance to check the key if auth fails.

## Playbook

### 1. Create and publish a new knowledgebase

1. POST /knowledgebases/create with `name`, `qnaList` or `urls` in the payload
2. Extract the `Operation-Location` header from the 202 response
3. Poll GET /operations/{operationId} until `operationState` is `Succeeded`
4. Note the `resourceLocation` in the operation result -- it contains the new `kbId`
5. POST /knowledgebases/{kbId} to publish the knowledgebase to production
6. GET /endpointkeys to retrieve the runtime endpoint key for querying

### 2. Update a knowledgebase with new QnA pairs

1. GET /knowledgebases/{kbId} to confirm the KB exists and check current state
2. PATCH /knowledgebases/{kbId} with an `add`, `update`, or `delete` block in `updateKb`
3. Extract the `Operation-Location` header from the 202 response
4. Poll GET /operations/{operationId} until `operationState` is `Succeeded`
5. POST /knowledgebases/{kbId} to republish so changes are live in production

### 3. Configure synonyms for better answer matching

1. GET /alterations to retrieve current synonym groups
2. Append new `{alterations: ["word1", "word2"]}` entries to the existing list
3. PUT /alterations with the full updated `wordAlterations` array
4. Verify 204 response -- no polling needed, this is synchronous

### 4. Rotate endpoint keys safely

1. GET /endpointkeys to see current primary and secondary keys
2. Update all consuming applications to use the secondary key
3. PATCH /endpointkeys/PrimaryKey to rotate the primary key
4. Capture the new primary key from the 200 response
5. Update consuming applications to use the new primary key
6. Optionally repeat for the secondary key

### 5. Audit and export knowledgebase content

1. GET /knowledgebases to list all KBs and identify target `kbId` values
2. GET /knowledgebases/{kbId} for each KB to check `lastPublishedTimestamp`
3. GET /knowledgebases/{kbId}/prod/qna to export production QnA pairs
4. GET /knowledgebases/{kbId}/test/qna to export test QnA pairs (use `changedSince` to scope to recent edits)
5. Compare test vs prod to identify unpublished changes


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
