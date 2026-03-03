---
name: mistral-ai-api
description: "Mistral AI API skill. Use when working with Mistral AI for models, conversations, agents. Covers 71 endpoints."
version: 1.0.0
generator: lapsh
---

# Mistral AI API
API version: 1.0.0

## Auth
Bearer bearer

## Base URL
https://api.mistral.ai

## Setup
1. Set Authorization header with your Bearer token
2. GET /v1/models -- verify access
3. POST /v1/conversations -- create first conversations

## Endpoints

71 endpoints across 15 groups. See references/api-spec.lap for full details.

### models
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/models | List Models |
| GET | /v1/models/{model_id} | Retrieve Model |
| DELETE | /v1/models/{model_id} | Delete Model |

### conversations
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/conversations | Create a conversation and append entries to it. |
| GET | /v1/conversations | List all created conversations. |
| GET | /v1/conversations/{conversation_id} | Retrieve a conversation information. |
| DELETE | /v1/conversations/{conversation_id} | Delete a conversation. |
| POST | /v1/conversations/{conversation_id} | Append new entries to an existing conversation. |
| GET | /v1/conversations/{conversation_id}/history | Retrieve all entries in a conversation. |
| GET | /v1/conversations/{conversation_id}/messages | Retrieve all messages in a conversation. |
| POST | /v1/conversations/{conversation_id}/restart | Restart a conversation starting from a given entry. |
| POST | /v1/conversations/{conversation_id}#stream | Append new entries to an existing conversation. |
| POST | /v1/conversations/{conversation_id}/restart#stream | Restart a conversation starting from a given entry. |

### agents
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/agents | Create a agent that can be used within a conversation. |
| GET | /v1/agents | List agent entities. |
| GET | /v1/agents/{agent_id} | Retrieve an agent entity. |
| PATCH | /v1/agents/{agent_id} | Update an agent entity. |
| DELETE | /v1/agents/{agent_id} | Delete an agent entity. |
| PATCH | /v1/agents/{agent_id}/version | Update an agent version. |
| GET | /v1/agents/{agent_id}/versions | List all versions of an agent. |
| GET | /v1/agents/{agent_id}/versions/{version} | Retrieve a specific version of an agent. |
| PUT | /v1/agents/{agent_id}/aliases | Create or update an agent version alias. |
| GET | /v1/agents/{agent_id}/aliases | List all aliases for an agent. |
| POST | /v1/agents/completions | Agents Completion |

### conversations#stream
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/conversations#stream | Create a conversation and append entries to it. |

### files
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/files | Upload File |
| GET | /v1/files | List Files |
| GET | /v1/files/{file_id} | Retrieve File |
| DELETE | /v1/files/{file_id} | Delete File |
| GET | /v1/files/{file_id}/content | Download File |
| GET | /v1/files/{file_id}/url | Get Signed Url |

### fine_tuning
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/fine_tuning/jobs | Get Fine Tuning Jobs |
| POST | /v1/fine_tuning/jobs | Create Fine Tuning Job |
| GET | /v1/fine_tuning/jobs/{job_id} | Get Fine Tuning Job |
| POST | /v1/fine_tuning/jobs/{job_id}/cancel | Cancel Fine Tuning Job |
| POST | /v1/fine_tuning/jobs/{job_id}/start | Start Fine Tuning Job |
| PATCH | /v1/fine_tuning/models/{model_id} | Update Fine Tuned Model |
| POST | /v1/fine_tuning/models/{model_id}/archive | Archive Fine Tuned Model |
| DELETE | /v1/fine_tuning/models/{model_id}/archive | Unarchive Fine Tuned Model |

### batch
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/batch/jobs | Get Batch Jobs |
| POST | /v1/batch/jobs | Create Batch Job |
| GET | /v1/batch/jobs/{job_id} | Get Batch Job |
| POST | /v1/batch/jobs/{job_id}/cancel | Cancel Batch Job |

### chat
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/chat/completions | Chat Completion |
| POST | /v1/chat/moderations | Chat Moderations |
| POST | /v1/chat/classifications | Chat Classifications |

### fim
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/fim/completions | Fim Completion |

### embeddings
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/embeddings | Embeddings |

### moderations
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/moderations | Moderations |

### ocr
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/ocr | OCR |

### classifications
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/classifications | Classifications |

### audio
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/audio/transcriptions | Create Transcription |
| POST | /v1/audio/transcriptions#stream | Create Streaming Transcription (SSE) |

### libraries
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/libraries | List all libraries you have access to. |
| POST | /v1/libraries | Create a new Library. |
| GET | /v1/libraries/{library_id} | Detailed information about a specific Library. |
| DELETE | /v1/libraries/{library_id} | Delete a library and all of it's document. |
| PUT | /v1/libraries/{library_id} | Update a library. |
| GET | /v1/libraries/{library_id}/documents | List documents in a given library. |
| POST | /v1/libraries/{library_id}/documents | Upload a new document. |
| GET | /v1/libraries/{library_id}/documents/{document_id} | Retrieve the metadata of a specific document. |
| PUT | /v1/libraries/{library_id}/documents/{document_id} | Update the metadata of a specific document. |
| DELETE | /v1/libraries/{library_id}/documents/{document_id} | Delete a document. |
| GET | /v1/libraries/{library_id}/documents/{document_id}/text_content | Retrieve the text content of a specific document. |
| GET | /v1/libraries/{library_id}/documents/{document_id}/status | Retrieve the processing status of a specific document. |
| GET | /v1/libraries/{library_id}/documents/{document_id}/signed-url | Retrieve the signed URL of a specific document. |
| GET | /v1/libraries/{library_id}/documents/{document_id}/extracted-text-signed-url | Retrieve the signed URL of text extracted from a given document. |
| POST | /v1/libraries/{library_id}/documents/{document_id}/reprocess | Reprocess a document. |
| GET | /v1/libraries/{library_id}/share | List all of the access to this library. |
| PUT | /v1/libraries/{library_id}/share | Create or update an access level. |
| DELETE | /v1/libraries/{library_id}/share | Delete an access level. |

## Enhanced Skill Content
## Question Mapping

- "What models are available?" -> GET /v1/models
- "How do I send a chat message to Mistral?" -> POST /v1/chat/completions
- "Can I get code completions with fill-in-the-middle?" -> POST /v1/fim/completions
- "How do I create an agent with custom instructions?" -> POST /v1/agents
- "How do I start a multi-turn conversation?" -> POST /v1/conversations
- "How do I continue an existing conversation?" -> POST /v1/conversations/{conversation_id}
- "How do I upload a training file for fine-tuning?" -> POST /v1/files
- "How do I kick off a fine-tuning job?" -> POST /v1/fine_tuning/jobs
- "How do I run batch inference across many inputs?" -> POST /v1/batch/jobs
- "How do I extract text from a PDF or image?" -> POST /v1/ocr
- "How do I check if content violates safety policies?" -> POST /v1/moderations
- "How do I generate embeddings for semantic search?" -> POST /v1/embeddings
- "How do I create a knowledge library and upload documents?" -> POST /v1/libraries then POST /v1/libraries/{library_id}/documents
- "How do I share a library with my team?" -> PUT /v1/libraries/{library_id}/share
- "How do I transcribe an audio file?" -> POST /v1/audio/transcriptions

## Response Tips

- **Models**: `data` is an array of model objects; the top-level `object` field is always a list descriptor.
- **Chat/FIM/Agent completions**: Response shape mirrors OpenAI; look for `choices[].message.content` and `usage` for token counts. Streaming endpoints (`#stream`) return SSE chunks, not JSON.
- **Conversations**: `outputs` is an array of agent actions/messages; `usage` includes `connector_tokens` when tools/connectors fire. Pagination uses `page` (0-indexed) and `page_size` (default 100).
- **Agents**: Versioned resources -- `version` is an int that auto-increments on PATCH; `versions` array lists all available version numbers. Use aliases to pin stable references.
- **Files**: `created_at` is a Unix timestamp (int), not ISO string. `num_lines` and `mimetype` may be null until processing completes.
- **Fine-tuning/Batch jobs**: Poll `status` field for progress. Batch jobs include `total_requests`, `completed_requests`, `succeeded_requests`, `failed_requests` for granular tracking.
- **Libraries/Documents**: Document listing returns structured `pagination` with `has_more`, `total_pages`, `current_page` -- the only endpoint group using this richer pagination model. `processing_status` tracks async ingestion.
- **OCR**: Response is page-level; `pages` array contains per-page results with `usage_info.pages_processed` for billing.
- **Errors**: All mutating endpoints return 422 for validation failures. DELETE endpoints return either 200 (with confirmation body) or 204 (no body) depending on the resource.

## Anomaly Flags

- **Token usage spikes**: Surface `usage.total_tokens` when it exceeds expected thresholds, especially `connector_tokens` in conversations which indicate hidden tool/connector costs.
- **Batch job failures**: Alert when `failed_requests` > 0 or `errors` array is non-empty on batch job status checks.
- **Fine-tuning dry run**: Flag when `dry_run` is set -- no job is actually created, just validated. Easy to miss.
- **Document processing stuck**: Surface when `processing_status` remains non-terminal after repeated polls on library documents.
- **Model deletion**: Warn before DELETE /v1/models/{model_id} -- this permanently removes fine-tuned models and cannot be undone.
- **Agent version drift**: Flag when the active `version` differs from the latest in `versions` array, indicating the agent may be pinned to an old version.
- **File signature null**: When `signature` is null on a file, the file may still be processing or validation is incomplete.
- **Batch timeout**: `timeout_hours` defaults to 24 -- surface this default so users are aware of auto-cancellation.
- **Invalid sample skip**: Fine-tuning `invalid_sample_skip_percentage` defaults to 0, meaning any bad sample fails the job. Flag this if training data quality is uncertain.

## Playbook

### 1. Fine-tune a custom model

1. Upload your JSONL training file: `POST /v1/files` with purpose set to fine-tuning.
2. Note the returned `id` (UUID).
3. Create the fine-tuning job: `POST /v1/fine_tuning/jobs` with the `model` (e.g., `mistral-small-latest`), `training_files: [{file_id: "<id>"}]`, and `hyperparameters`.
4. If `auto_start` is false, explicitly start: `POST /v1/fine_tuning/jobs/{job_id}/start`.
5. Poll job status: `GET /v1/fine_tuning/jobs/{job_id}` until `status` is `succeeded`.
6. The resulting model appears in `GET /v1/models` and can be used in chat completions.

### 2. Build and iterate on an agent

1. Create the agent: `POST /v1/agents` with `model`, `name`, `instructions`, and optional `tools`.
2. Note the returned `id` and `version` (starts at 1).
3. Test it: `POST /v1/agents/completions` with `agent_id` and `messages`.
4. Refine by patching: `PATCH /v1/agents/{agent_id}` with updated fields. This auto-increments `version`.
5. Pin a stable release: `PUT /v1/agents/{agent_id}/aliases` with `alias: "production"` and the desired `version`.
6. Compare versions: `GET /v1/agents/{agent_id}/versions/{version}` to diff configurations.

### 3. Run batch inference at scale

1. Prepare a JSONL file with one request per line matching the target endpoint schema.
2. Upload it: `POST /v1/files`.
3. Create the batch job: `POST /v1/batch/jobs` with `endpoint` (e.g., `/v1/chat/completions`), `input_files: [file_id]`, and optional `model`.
4. Poll: `GET /v1/batch/jobs/{job_id}` -- check `completed_requests` vs `total_requests`.
5. When `status` is terminal, download results via `output_file` and check `error_file` for failures.

### 4. Build a knowledge library with document search

1. Create a library: `POST /v1/libraries` with `name` and optional `description`.
2. Upload documents: `POST /v1/libraries/{library_id}/documents` (supports multiple formats).
3. Poll processing: `GET /v1/libraries/{library_id}/documents/{document_id}/status` until `processing_status` is complete.
4. Browse documents: `GET /v1/libraries/{library_id}/documents` with `search`, `sort_by`, and pagination params.
5. Retrieve extracted text: `GET /v1/libraries/{library_id}/documents/{document_id}/text_content`.
6. Share with collaborators: `PUT /v1/libraries/{library_id}/share` with target user/workspace UUID and `level` (Viewer/Editor).

### 5. Multi-turn conversation with streaming

1. Start a new conversation: `POST /v1/conversations` with initial input. Note the returned `conversation_id`.
2. Continue with streaming: `POST /v1/conversations/{conversation_id}#stream` to get SSE chunks in real time.
3. Review full history: `GET /v1/conversations/{conversation_id}/messages` for the message log, or `/history` for the raw entry log.
4. If the conversation goes off track: `POST /v1/conversations/{conversation_id}/restart#stream` to reset from a checkpoint.
5. Clean up: `DELETE /v1/conversations/{conversation_id}` when done.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
