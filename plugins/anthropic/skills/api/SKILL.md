---
name: anthropic-api-fast-mode
description: "Anthropic API + fast-mode API skill. Use when working with Anthropic API + fast-mode for messages, complete, models. Covers 47 endpoints."
version: 1.0.0
generator: lapsh
---

# Anthropic API + fast-mode
API version: 253

## Auth
ApiKey x-api-key in header

## Base URL
https://api.anthropic.com

## Setup
1. Set your API key in the appropriate header
2. GET /v1/models -- verify access
3. POST /v1/messages -- create first messages

## Endpoints

47 endpoints across 9 groups. See references/api-spec.lap for full details.

### messages
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/messages | Create a Message |
| POST | /v1/messages/batches | Create a Message Batch |
| GET | /v1/messages/batches | List Message Batches |
| GET | /v1/messages/batches/{message_batch_id} | Retrieve a Message Batch |
| DELETE | /v1/messages/batches/{message_batch_id} | Delete a Message Batch |
| POST | /v1/messages/batches/{message_batch_id}/cancel | Cancel a Message Batch |
| GET | /v1/messages/batches/{message_batch_id}/results | Retrieve Message Batch results |
| POST | /v1/messages/count_tokens | Count tokens in a Message |
| POST | /v1/messages/batches?beta=true | Create a Message Batch |
| GET | /v1/messages/batches?beta=true | List Message Batches |
| GET | /v1/messages/batches/{message_batch_id}?beta=true | Retrieve a Message Batch |
| DELETE | /v1/messages/batches/{message_batch_id}?beta=true | Delete a Message Batch |
| POST | /v1/messages/batches/{message_batch_id}/cancel?beta=true | Cancel a Message Batch |
| GET | /v1/messages/batches/{message_batch_id}/results?beta=true | Retrieve Message Batch results |
| POST | /v1/messages/count_tokens?beta=true | Count tokens in a Message |

### complete
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/complete | Create a Text Completion |

### models
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/models | List Models |
| GET | /v1/models/{model_id} | Get a Model |
| GET | /v1/models/{model_id}?beta=true | Get a Model |

### files
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/files | Upload File |
| GET | /v1/files | List Files |
| GET | /v1/files/{file_id} | Get File Metadata |
| DELETE | /v1/files/{file_id} | Delete File |
| GET | /v1/files/{file_id}/content | Download File |
| GET | /v1/files/{file_id}?beta=true | Get File Metadata |
| DELETE | /v1/files/{file_id}?beta=true | Delete File |
| GET | /v1/files/{file_id}/content?beta=true | Download File |

### skills
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/skills | Create Skill |
| GET | /v1/skills | List Skills |
| GET | /v1/skills/{skill_id} | Get Skill |
| DELETE | /v1/skills/{skill_id} | Delete Skill |
| POST | /v1/skills/{skill_id}/versions | Create Skill Version |
| GET | /v1/skills/{skill_id}/versions | List Skill Versions |
| GET | /v1/skills/{skill_id}/versions/{version} | Get Skill Version |
| DELETE | /v1/skills/{skill_id}/versions/{version} | Delete Skill Version |
| GET | /v1/skills/{skill_id}?beta=true | Get Skill |
| DELETE | /v1/skills/{skill_id}?beta=true | Delete Skill |
| POST | /v1/skills/{skill_id}/versions?beta=true | Create Skill Version |
| GET | /v1/skills/{skill_id}/versions?beta=true | List Skill Versions |
| GET | /v1/skills/{skill_id}/versions/{version}?beta=true | Get Skill Version |
| DELETE | /v1/skills/{skill_id}/versions/{version}?beta=true | Delete Skill Version |

### messages?beta=true
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/messages?beta=true | Create a Message |

### models?beta=true
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/models?beta=true | List Models |

### files?beta=true
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/files?beta=true | Upload File |
| GET | /v1/files?beta=true | List Files |

### skills?beta=true
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/skills?beta=true | Create Skill |
| GET | /v1/skills?beta=true | List Skills |

## Enhanced Skill Content
## Question Mapping

- "How do I send a message to Claude?" -> POST /v1/messages
- "What models are available?" -> GET /v1/models
- "How many tokens will my prompt use?" -> POST /v1/messages/count_tokens
- "How do I process many requests at once?" -> POST /v1/messages/batches
- "What's the status of my batch job?" -> GET /v1/messages/batches/{message_batch_id}
- "How do I cancel a running batch?" -> POST /v1/messages/batches/{message_batch_id}/cancel
- "Where do I download batch results?" -> GET /v1/messages/batches/{message_batch_id}/results
- "How do I upload a file for use in conversations?" -> POST /v1/files
- "How do I download a file I uploaded?" -> GET /v1/files/{file_id}/content
- "How do I create a skill?" -> POST /v1/skills
- "How do I publish a new version of my skill?" -> POST /v1/skills/{skill_id}/versions
- "What versions exist for my skill?" -> GET /v1/skills/{skill_id}/versions
- "How do I use extended thinking or tool use?" -> POST /v1/messages (with `thinking` and `tools` optional fields)
- "How do I stream a response?" -> POST /v1/messages (set `stream: true`)
- "How do I use the legacy completion API?" -> POST /v1/complete

## Response Tips

- **Messages:** `stop_reason` indicates why generation stopped (end_turn, max_tokens, stop_sequence, tool_use). Check `usage.input_tokens` and `usage.output_tokens` for cost tracking. `content` is an array -- tool use responses contain multiple blocks.
- **Models list:** Cursor-paginated via `before_id`/`after_id` with `has_more` boolean. Default limit is 20. Use `last_id` as `after_id` for next page.
- **Batches:** `processing_status` tracks lifecycle (in_progress, ended, canceling, expired). `request_counts` breaks down per-item outcomes. `results_url` is null until the batch completes.
- **Files:** `downloadable` boolean indicates whether content retrieval is allowed. `size_bytes` is useful for quota tracking. The content endpoint returns raw file bytes, not JSON.
- **Skills:** Paginated via `next_page` token (not cursor IDs). `latest_version` is null until a version is published. `source` distinguishes user-created from system skills.
- **Token counting:** Returns only `input_tokens`. Does not estimate output tokens. Include tools/system prompt for accurate counts.
- **Errors:** All endpoints return 4XX. Expect `{"type":"error","error":{"type":"...","message":"..."}}` with types like `invalid_request_error`, `authentication_error`, `rate_limit_error`, `overloaded_error`.

## Anomaly Flags

- **Rate limit hit (429):** Surface `retry-after` header value and recommend backoff. Alert if multiple 429s occur within a short window.
- **Overloaded (529):** The API is temporarily at capacity. Distinct from rate limiting -- retry with exponential backoff rather than waiting for quota reset.
- **Batch expiration approaching:** Flag when `expires_at` is within 1 hour and `processing_status` is still `in_progress`. Results must be downloaded before expiry.
- **High error rate in batches:** Surface when `request_counts.errored` exceeds 10% of total requests. Suggest inspecting results for common failure patterns.
- **Token usage spikes:** Flag when `usage.output_tokens` equals `max_tokens` -- the response was likely truncated. Suggest increasing `max_tokens` or checking `stop_reason`.
- **Cache utilization:** When `cache_read_input_tokens` is 0 but `cache_creation_input_tokens` is high across repeated calls, caching may not be working as expected.
- **Beta endpoint drift:** If `anthropic-beta` header is missing on beta endpoints (`?beta=true`), warn that behavior may differ from documented beta features.
- **Deprecated completion API:** Flag usage of POST /v1/complete and recommend migrating to POST /v1/messages.
- **Missing anthropic-version header:** All endpoints require the `anthropic-version` common field. Surface a clear error if omitted rather than letting an opaque 400 propagate.

## Playbook

### 1. Send a Message with Streaming

1. Call `POST /v1/messages` with `stream: true`, your `model`, `messages`, and `max_tokens`.
2. Set header `x-api-key` with your API key and `anthropic-version` with the version string.
3. Read the response as server-sent events (SSE). Each event contains a delta with partial content.
4. Accumulate `content` blocks until you receive the `message_stop` event.
5. Check the final `stop_reason` to confirm the response completed naturally (`end_turn`) vs was truncated (`max_tokens`).

### 2. Run a Batch of Requests

1. Prepare an array of request objects, each with a unique `custom_id` and `params` matching the messages endpoint schema.
2. Call `POST /v1/messages/batches` with the `requests` array.
3. Note the returned `id` and `expires_at`.
4. Poll `GET /v1/messages/batches/{id}` until `processing_status` is `ended`.
5. Download results from `GET /v1/messages/batches/{id}/results`. Match results to requests using `custom_id`.
6. Check `request_counts` to verify all items succeeded. Investigate any with `errored` > 0.

### 3. Upload a File and Reference It in a Conversation

1. Call `POST /v1/files` with the file as multipart form data. Include `anthropic-beta` header if using beta features.
2. Note the returned `id`, `filename`, and `mime_type`.
3. Use the file `id` in a subsequent `POST /v1/messages` call by referencing it in the `content` array of your message.
4. To verify the upload, call `GET /v1/files/{file_id}` and confirm `downloadable` is true.
5. Clean up with `DELETE /v1/files/{file_id}` when the file is no longer needed.

### 4. Create and Version a Skill

1. Call `POST /v1/skills` to create a new skill. Note the returned `id`.
2. Call `POST /v1/skills/{skill_id}/versions` with the skill content to publish version 1.
3. Verify by calling `GET /v1/skills/{skill_id}` -- `latest_version` should now be populated.
4. To update, call `POST /v1/skills/{skill_id}/versions` again with updated content. A new version is created automatically.
5. List all versions with `GET /v1/skills/{skill_id}/versions` to confirm the history.

### 5. Estimate Cost Before Sending

1. Construct your full message payload including `messages`, `model`, `system` prompt, and any `tools`.
2. Call `POST /v1/messages/count_tokens` with the same parameters.
3. Read `input_tokens` from the response to estimate input cost.
4. If tokens exceed your budget, trim the conversation history or system prompt and re-count.
5. Once satisfied, send the actual request via `POST /v1/messages` with the same payload.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
