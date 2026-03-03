---
name: openrouter-api
description: "OpenRouter API skill. Use when working with OpenRouter for responses, messages, activity. Covers 36 endpoints."
version: 1.0.0
generator: lapsh
---

# OpenRouter API
API version: 1.0.0

## Auth
Bearer bearer | Bearer bearer

## Base URL
https://openrouter.ai/api/v1

## Setup
1. Set Authorization header with your Bearer token
2. GET /activity -- verify access
3. POST /responses -- create first responses

## Endpoints

36 endpoints across 14 groups. See references/api-spec.lap for full details.

### responses
| Method | Path | Description |
|--------|------|-------------|
| POST | /responses | Create a response |

### messages
| Method | Path | Description |
|--------|------|-------------|
| POST | /messages | Create a message |

### activity
| Method | Path | Description |
|--------|------|-------------|
| GET | /activity | Get user activity grouped by endpoint |

### chat
| Method | Path | Description |
|--------|------|-------------|
| POST | /chat/completions | Create a chat completion |

### credits
| Method | Path | Description |
|--------|------|-------------|
| GET | /credits | Get remaining credits |
| POST | /credits/coinbase | Create a Coinbase charge for crypto payment |

### embeddings
| Method | Path | Description |
|--------|------|-------------|
| POST | /embeddings | Submit an embedding request |
| GET | /embeddings/models | List all embeddings models |

### generation
| Method | Path | Description |
|--------|------|-------------|
| GET | /generation | Get request & usage metadata for a generation |

### models
| Method | Path | Description |
|--------|------|-------------|
| GET | /models/count | Get total count of available models |
| GET | /models | List all models and their properties |
| GET | /models/user | List models filtered by user provider preferences, privacy settings, and guardrails |
| GET | /models/{author}/{slug}/endpoints | List all endpoints for a model |

### endpoints
| Method | Path | Description |
|--------|------|-------------|
| GET | /endpoints/zdr | Preview the impact of ZDR on the available endpoints |

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers | List all providers |

### keys
| Method | Path | Description |
|--------|------|-------------|
| GET | /keys | List API keys |
| POST | /keys | Create a new API key |
| PATCH | /keys/{hash} | Update an API key |
| DELETE | /keys/{hash} | Delete an API key |
| GET | /keys/{hash} | Get a single API key |

### guardrails
| Method | Path | Description |
|--------|------|-------------|
| GET | /guardrails | List guardrails |
| POST | /guardrails | Create a guardrail |
| GET | /guardrails/{id} | Get a guardrail |
| PATCH | /guardrails/{id} | Update a guardrail |
| DELETE | /guardrails/{id} | Delete a guardrail |
| GET | /guardrails/assignments/keys | List all key assignments |
| GET | /guardrails/assignments/members | List all member assignments |
| GET | /guardrails/{id}/assignments/keys | List key assignments for a guardrail |
| POST | /guardrails/{id}/assignments/keys | Bulk assign keys to a guardrail |
| GET | /guardrails/{id}/assignments/members | List member assignments for a guardrail |
| POST | /guardrails/{id}/assignments/members | Bulk assign members to a guardrail |
| POST | /guardrails/{id}/assignments/keys/remove | Bulk unassign keys from a guardrail |
| POST | /guardrails/{id}/assignments/members/remove | Bulk unassign members from a guardrail |

### key
| Method | Path | Description |
|--------|------|-------------|
| GET | /key | Get current API key |

### auth
| Method | Path | Description |
|--------|------|-------------|
| POST | /auth/keys | Exchange authorization code for API key |
| POST | /auth/keys/code | Create authorization code |

## Enhanced Skill Content
## Question Mapping

- "How do I send a chat completion request?" -> POST /chat/completions
- "How much credit do I have left?" -> GET /credits
- "What models are available on OpenRouter?" -> GET /models
- "How do I generate embeddings for text?" -> POST /embeddings
- "What happened with a specific generation?" -> GET /generation?id={id}
- "How do I create a new API key?" -> POST /keys
- "How do I set a spending limit on a key?" -> PATCH /keys/{hash}
- "How do I delete an API key?" -> DELETE /keys/{hash}
- "What is my current key's usage and rate limit?" -> GET /key
- "How do I restrict which models a team member can use?" -> POST /guardrails then POST /guardrails/{id}/assignments/members
- "Which providers support zero data retention?" -> GET /endpoints/zdr
- "How do I top up credits with crypto?" -> POST /credits/coinbase
- "What models does a specific author offer?" -> GET /models/{author}/{slug}/endpoints
- "How do I authenticate a third-party app via OAuth PKCE?" -> POST /auth/keys/code then POST /auth/keys
- "What is my API usage for a specific date?" -> GET /activity?date={date}

## Response Tips

- **Chat/Responses/Messages**: Response body includes `usage` with token breakdowns (prompt, completion, cached, reasoning) -- always check `usage.total_tokens` and `total_cost` from generation details for billing accuracy.
- **Models**: `data` is a flat array of all models -- filter client-side by `category` param or post-hoc; no pagination, expect large payloads.
- **Keys/Guardrails**: List endpoints return `data` arrays with `offset`-based pagination; check `total_count` on guardrails to know if more pages exist.
- **Credits**: Nested under `data` map -- access as `response.data.total_credits` and `response.data.total_usage`, not top-level.
- **Generation**: Single-object response with nullable fields (e.g., `upstream_id`, `cache_discount`, `native_tokens_reasoning`) -- check for null before using.
- **Errors**: All endpoints share a common error pattern; 402 means insufficient credits, 429 means rate limited, 529 means the upstream provider is overloaded.

## Anomaly Flags

- **Rate limit approaching**: Surface when `GET /key` shows `rate_limit.requests` is high relative to `rate_limit.interval`, or when 429 errors start appearing.
- **Credits running low**: Alert when `GET /credits` shows `total_usage` approaching `total_credits` (< 10% remaining).
- **Key expiring soon**: Flag when `GET /keys/{hash}` returns an `expires_at` within 48 hours.
- **Spending limit nearly exhausted**: Warn when `limit_remaining` on a key is below 10% of `limit`.
- **Deprecated or unusual status codes**: Surface 524 (upstream timeout) and 529 (upstream overload) distinctly -- these are not standard HTTP codes and indicate provider-side issues, not client errors.
- **Free tier restrictions**: Flag when `GET /key` returns `is_free_tier: true`, as this limits available models and throughput.
- **Zero data retention failures**: If `provider.zdr: true` was requested but the generation response shows a non-ZDR provider, alert the user to a potential data policy mismatch.

## Playbook

### 1. Send a Chat Completion and Track Cost

1. `POST /chat/completions` with `model`, `messages`, and desired parameters.
2. Extract `id` from the response (the generation ID).
3. `GET /generation?id={id}` to retrieve `total_cost`, `tokens_prompt`, `tokens_completion`, and `provider_name`.
4. Optionally check `GET /credits` to confirm remaining balance.

### 2. Create and Budget-Cap an API Key

1. `POST /keys` with `name`, `limit` (USD cap), and `limit_reset` (e.g., `monthly`).
2. Save the returned `key` value -- it is only shown once.
3. Optionally `POST /guardrails` to create a guardrail restricting models or providers.
4. `POST /guardrails/{id}/assignments/keys` with the key hash to attach the guardrail.
5. Verify with `GET /keys/{hash}` to confirm `limit`, `limit_remaining`, and guardrail assignment.

### 3. Set Up OAuth PKCE App Authentication

1. Generate a `code_verifier` and derive a `code_challenge` (SHA-256, base64url).
2. `POST /auth/keys/code` with `callback_url`, `code_challenge`, and `code_challenge_method: "S256"`.
3. Redirect the user to OpenRouter's auth page with the returned `id`.
4. On callback, extract the `code` parameter from the redirect URL.
5. `POST /auth/keys` with `code` and `code_verifier` to receive the API key.

### 4. Compare Models Before Choosing One

1. `GET /models` to list all available models (optionally filter by `category`).
2. Identify candidate models and note their IDs (format: `{author}/{slug}`).
3. `GET /models/{author}/{slug}/endpoints` for each candidate to see provider endpoints, pricing, and context lengths.
4. `GET /endpoints/zdr` if zero data retention is required -- cross-reference with candidate endpoints.
5. Use the chosen model in `POST /chat/completions` with `provider.only` to pin a specific provider if needed.

### 5. Enforce Team Guardrails

1. `POST /guardrails` with `name`, `limit_usd`, `reset_interval`, and optionally `allowed_models` or `enforce_zdr`.
2. List team member keys with `GET /keys`.
3. `POST /guardrails/{id}/assignments/keys` with the relevant `key_hashes` array.
4. Or assign by member: `POST /guardrails/{id}/assignments/members` with `member_user_ids`.
5. Verify assignments with `GET /guardrails/{id}/assignments/keys` or `GET /guardrails/{id}/assignments/members`.
6. To revoke, use `POST /guardrails/{id}/assignments/keys/remove` or `POST /guardrails/{id}/assignments/members/remove`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
