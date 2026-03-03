---
name: vectara-rest-api
description: "Vectara REST API skill. Use when working with Vectara REST for compute-account-size, compute-corpus-size, create-api-key. Covers 29 endpoints."
version: 1.0.0
generator: lapsh
---

# Vectara REST API
API version: 1.0.0

## Auth
OAuth2 | ApiKey x-api-key in header

## Base URL
https://api.vectara.io

## Setup
1. Set your API key in the appropriate header
3. POST /v1/compute-account-size -- create first compute-account-size

## Endpoints

29 endpoints across 29 groups. See references/api-spec.lap for full details.

### compute-account-size
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/compute-account-size | Computes the amount of quota consumed across the entire Vectara account. |

### compute-corpus-size
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/compute-corpus-size | Computes the amount of quota consumed by a corpus. This capability is useful for administrators to track and monitor the amount |

### create-api-key
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/create-api-key | Creates an API key that you bind with a specific corpus or multiple corpora. You can create an API key that only gives access to query data (read-only) or an API key that gives access to both querying and serving (read-write). |

### create-corpus
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/create-corpus | Creates a corpus, which is a container to store data in. |

### delete-api-key
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/delete-api-key | Deletes API keys to help you manage the security and lifecycle of API keys in your application. |

### delete-conversations
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/delete-conversations | Delete conversations from the chat history corpus. This is useful for data management to help ensure that you maintain data hygiene and support compliance with data retention policies. |

### delete-corpus
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/delete-corpus | Deletes a corpus and all of the data contained inside of the corpus. |

### delete-doc
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/delete-doc | Delete documents from a corpus. |

### delete-turns
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/delete-turns | Deletes specific turns from a conversation within the chat history corpus. This enables developers to remove inaccurate or inappropriate responses from the conversation history. |

### disable-turns
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/disable-turns | Disables specific turns from a conversation within the chat history corpus. This is useful for excluding specific turns from a conversation. |

### enable-api-key
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/enable-api-key | Enables or disables a specific API key. |

### get-usage-metrics
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/get-usage-metrics | Displays usage information about indexing and query operations in a corpus. This helps administrators in analyzing and managing resource consumption more efficiently for specific corpora. |

### index
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/index | This is the "standard" Indexing API for indexing semi-structured, text-heavy "documents."  Indexing data into Vectara is typically very fast: within a few seconds. |

### list-api-keys
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/list-api-keys | Lists the API keys and the associated corpora names and IDs. |

### list-conversations
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/list-conversations | List all the conversations in a specific corpus. This data enables developers to monitor chatbot interactions and understand how users engage with the data. Pagination lets developers navigate through large datasets. |

### list-corpora
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/list-corpora | Lists all corpora accessible to the OAuth client. |

### list-documents
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/list-documents | Lists information about each document ingested into the corpus including the Document ID and metadata. This is useful for managing the lifecycle of documents and a quick way to check which documents are already in the index. |

### list-jobs
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/list-jobs | List the jobs associated with this account.  Jobs are background processes like [replacing the filterable metadata attributes](https://docs.vectara.com/docs/rest-api/replace-corpus-filter-attrs). |

### list-users
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/list-users | Lists the users in your account along with their corpus access and customer-level authorizations. |

### manage-user
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/manage-user | Lets you manage users in your account by adding, deleting, enabling, or disabling users. You can also reset their passwords and edit user roles. This endpoint can help you streamline your onboarding process by programmatically adding new users, assigning appropriate roles, and setting up permissions. |

### query
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/query | Search for relevant results, highlight relevant snippets, and do |

### read-conversations
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/read-conversations | Retrieves detailed information about specific conversations. This information enables developers to analyze the flow of user chats and understand the context of interactions, which helps in refining chatbot responses. You can read up to 100 conversations. |

### read-corpus
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/read-corpus | Displays detailed information about corpora within your account including basic information, metadata, and whether it is enabled or disabled. |

### replace-corpus-filter-attrs
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/replace-corpus-filter-attrs | Updates the filterable metadata fields for the corpus. |

### reset-corpus
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/reset-corpus | Resets a corpus by removing all of the documents inside of it. |

### stream-query
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/stream-query | Stream responses as you search for relevant results, highlight relevant snippets, and do |

### update-corpus-enablement
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/update-corpus-enablement | Lets you enable or disable a corpus. This is useful when you need to take the corpus offline without having to delete the corpus. |

### core
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/core/index | This API is intended to be used by experts.  It gives you fine-grained control over chunking |

### upload
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/upload | The File Upload API can be used to index binary files like PDFs, Word Documents, and similar. |

## Enhanced Skill Content
## Question Mapping

- "How do I search my corpus for documents?" -> POST /v1/query
- "How do I stream search results in real time?" -> POST /v1/stream-query
- "How do I add a document to a corpus?" -> POST /v1/index
- "How do I upload a file to Vectara?" -> POST /v1/upload
- "How do I create a new corpus?" -> POST /v1/create-corpus
- "How do I list all my corpora?" -> POST /v1/list-corpora
- "How do I delete a document from a corpus?" -> POST /v1/delete-doc
- "How do I check my account storage usage?" -> POST /v1/compute-account-size
- "How do I create and manage API keys?" -> POST /v1/create-api-key, POST /v1/list-api-keys, POST /v1/delete-api-key, POST /v1/enable-api-key
- "How do I view conversation history for chat?" -> POST /v1/list-conversations, POST /v1/read-conversations
- "How do I remove old conversation turns?" -> POST /v1/delete-turns, POST /v1/disable-turns
- "How do I get usage metrics for a corpus over a time window?" -> POST /v1/get-usage-metrics
- "How do I manage users and their roles?" -> POST /v1/manage-user, POST /v1/list-users
- "How do I wipe all data in a corpus without deleting it?" -> POST /v1/reset-corpus
- "How do I update filter attributes on a corpus?" -> POST /v1/replace-corpus-filter-attrs

## Response Tips

- **Query/Stream-Query**: Responses contain `responseSet` arrays with nested document matches, summary text, and `metrics` (encode/retrieval/rerank timings) -- always check `status` arrays at multiple nesting levels for partial failures.
- **List endpoints** (corpora, documents, conversations, API keys, jobs, users): All use cursor-based pagination via `pageKey`/`nextPageKey` -- pass the returned key into the next request; an empty or absent key means no more pages.
- **Mutation endpoints** (create, delete, reset, update): Return a top-level `status` map with `code` and `statusDetail` -- treat any `code` other than `"OK"` as an error and read `statusDetail` for diagnostics.
- **Index/Upload**: Return `quotaConsumed` with `numChars` and `numMetadataChars` as string-encoded integers -- parse these to track indexing budget.
- **Stream-Query**: Returns chunked results with `result.summary.done` as a boolean sentinel -- keep consuming until `done: true`; intermediate chunks carry partial summary text and chat metadata.
- **Jobs** (replace-corpus-filter-attrs, etc.): Some mutations return a `jobId` -- poll via `list-jobs` filtering by that ID until state shows completion.

## Anomaly Flags

- **Quota exhaustion**: Surface `quotaConsumed` values from index/upload responses when `numChars` approaches known account limits; flag 507 (Insufficient Storage) errors immediately.
- **Partial failures in batch queries**: `status` arrays inside `responseSet` can contain per-corpus errors even when the HTTP response is 200 -- alert when any nested status code is not `"OK"`.
- **Pagination loops**: If `pageKey` in a list response is identical to the one sent, flag a potential infinite loop.
- **Slow query metrics**: Surface `metrics.retrievalMs` or `metrics.rerankMs` values that exceed typical thresholds (e.g., >5000ms) as performance warnings.
- **Auth errors (401/403)**: Distinguish between expired OAuth2 tokens (refresh needed) and invalid API keys (reconfiguration needed); suggest corrective action.
- **Corpus disabled**: `update-corpus-enablement` can silently disable a corpus -- flag when queries return empty results against a recently disabled corpus.
- **409 Conflict on upload**: Indicates a duplicate document ID -- surface the conflicting `documentId` and suggest delete-then-reupload or a new ID.
- **Factual consistency score**: When `factualConsistencyScore: true` is requested in summaries, flag scores below 0.5 as low-confidence answers.

## Playbook

### 1. Index a Document and Verify It

1. Call `POST /v1/create-corpus` with a `name` and optional `filterAttributes` to set up the target corpus. Note the returned `corpusId`.
2. Call `POST /v1/index` with `customerId`, `corpusId`, and a `document` object containing `documentId`, `title`, `text` sections, and optional `metadataJson`.
3. Check the response `status.code` is `"OK"` and note `quotaConsumed`.
4. Call `POST /v1/list-documents` with the `corpusId` and verify the new `documentId` appears in the results.
5. Call `POST /v1/compute-corpus-size` with the `corpusId` to confirm the size increased.

### 2. Run a Semantic Search with Summarization

1. Call `POST /v1/query` with a `query` array containing your search text, target `corpusKey` (with `corpusId`), `numResults`, and a `summary` block specifying `summarizerPromptName`, `maxSummarizedResults`, and `responseLang`.
2. Parse `responseSet[0].response` for ranked document matches with scores.
3. Read `responseSet[0].summary[0].text` for the generated answer.
4. If `factualConsistencyScore` was enabled, check `factualConsistency.score` -- values below 0.5 warrant a caveat to the user.
5. Review `metrics` to assess query performance and decide if tuning (e.g., adjusting `numResults` or `lexicalInterpolationConfig`) is needed.

### 3. Manage a Conversational Chat Session

1. Start a query with `POST /v1/query` or `POST /v1/stream-query`, including a `chat` object inside the `summary` block (omit `conversationId` for a new session).
2. Extract `conversationId` and `turnId` from the response's `summary.chat` field.
3. For follow-up questions, pass the same `conversationId` in the `chat` object to maintain context.
4. To review history, call `POST /v1/read-conversations` with the `conversationId`.
5. To prune context, call `POST /v1/disable-turns` or `POST /v1/delete-turns` with specific `turnId` values.
6. To end and clean up, call `POST /v1/delete-conversations` with the `conversationId`.

### 4. Rotate API Keys Safely

1. Call `POST /v1/list-api-keys` to inventory existing keys and their types/corpus bindings.
2. Call `POST /v1/create-api-key` with a new `description`, `apiKeyType`, and target `corpusId` list.
3. Update your application config to use the new key.
4. Call `POST /v1/enable-api-key` with `keyId` of the old key and `enable: false` to disable it.
5. Monitor for 401 errors in logs to confirm nothing still uses the old key.
6. Call `POST /v1/delete-api-key` with the old `keyId` to permanently remove it.

### 5. Bulk Upload Files to a Corpus

1. Call `POST /v1/read-corpus` with the target `corpusId` and `readFilterAttributes: true` to confirm the corpus exists and check its schema.
2. For each file, call `POST /v1/upload` with query params `c` (customer ID) and `o` (corpus ID), attaching the file as multipart form data. Set `d: true` to extract and index document content.
3. Check each response for `status` -- handle 409 (duplicate) by either skipping or deleting the existing doc first with `POST /v1/delete-doc`.
4. After all uploads, call `POST /v1/list-jobs` filtered by `corpusId` to verify all indexing jobs completed successfully.
5. Call `POST /v1/compute-corpus-size` to confirm the final indexed size matches expectations.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
