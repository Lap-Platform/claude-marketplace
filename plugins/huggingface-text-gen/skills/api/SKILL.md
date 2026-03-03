---
name: text-generation-inference
description: "Text Generation Inference API skill. Use when working with Text Generation Inference for root, chat_tokenize, generate. Covers 12 endpoints."
version: 1.0.0
generator: lapsh
---

# Text Generation Inference
API version: 3.3.6-dev0

## Auth
No authentication required.

## Base URL
Not specified.

## Setup
1. No auth setup needed
2. GET /health -- verify access
3. POST / -- create first resource

## Endpoints

12 endpoints across 12 groups. See references/api-spec.lap for full details.

### root
| Method | Path | Description |
|--------|------|-------------|
| POST | / | Generate tokens if `stream == false` or a stream of token if `stream == true` |

### chat_tokenize
| Method | Path | Description |
|--------|------|-------------|
| POST | /chat_tokenize | Template and tokenize ChatRequest |

### generate
| Method | Path | Description |
|--------|------|-------------|
| POST | /generate | Generate tokens |

### generate_stream
| Method | Path | Description |
|--------|------|-------------|
| POST | /generate_stream | Generate a stream of token using Server-Sent Events |

### health
| Method | Path | Description |
|--------|------|-------------|
| GET | /health | Health check method |

### info
| Method | Path | Description |
|--------|------|-------------|
| GET | /info | Text Generation Inference endpoint info |

### invocations
| Method | Path | Description |
|--------|------|-------------|
| POST | /invocations | Generate tokens from Sagemaker request |

### metrics
| Method | Path | Description |
|--------|------|-------------|
| GET | /metrics | Prometheus metrics scrape endpoint |

### tokenize
| Method | Path | Description |
|--------|------|-------------|
| POST | /tokenize | Tokenize inputs |

### chat
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/chat/completions | Generate tokens |

### completions
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/completions | Generate tokens |

### models
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/models | Get model info |

## Enhanced Skill Content
## Question Mapping

- "How do I generate text from a prompt?" -> POST /generate
- "How do I stream text generation in real time?" -> POST /generate_stream
- "How do I send a chat message with conversation history?" -> POST /v1/chat/completions
- "How do I complete a text prompt using the OpenAI-compatible endpoint?" -> POST /v1/completions
- "Is the inference server healthy and ready to accept requests?" -> GET /health
- "What model is currently loaded and what are its limits?" -> GET /info
- "How many tokens does my input text use?" -> POST /tokenize
- "How do I see what my chat template looks like after tokenization?" -> POST /chat_tokenize
- "What models are available on this server?" -> GET /v1/models
- "How do I call a tool or function from a chat completion?" -> POST /v1/chat/completions (with `tools` and `tool_choice`)
- "How do I get Prometheus metrics for monitoring?" -> GET /metrics
- "How do I use this behind a SageMaker endpoint?" -> POST /invocations
- "How do I generate text with a specific LoRA adapter?" -> POST /generate (with `parameters.adapter_id`)
- "How do I constrain output to a specific grammar or JSON schema?" -> POST /generate (with `parameters.grammar`)
- "How do I get token-level log probabilities from a chat response?" -> POST /v1/chat/completions (with `logprobs: true`)

## Response Tips

- **Generation endpoints** (`/`, `/generate`, `/generate_stream`): Response contains `generated_text` as a string; set `details: true` in parameters to get token-level metadata including `finish_reason`, `generated_tokens`, and per-token probabilities. Streaming returns server-sent events, not JSON.
- **Chat/Completions** (`/v1/chat/completions`, `/v1/completions`): OpenAI-compatible shape -- results are in `choices[]` array, token counts in `usage` object. When `stream: true`, responses arrive as SSE `data:` lines with a final `data: [DONE]` sentinel.
- **Info/Models** (`/info`, `/v1/models`): Single object responses with no pagination. `/info` returns server limits (`max_input_tokens`, `max_total_tokens`) that should inform request construction.
- **Tokenize** (`/tokenize`, `/chat_tokenize`): Returns token arrays. `/chat_tokenize` also returns the `templated_text` showing the fully rendered chat template.
- **Health/Metrics** (`/health`, `/metrics`): `/health` returns empty 200 on success, 503 when overloaded. `/metrics` returns Prometheus text format, not JSON.
- **Errors**: 422 = invalid parameters, 424 = generation failure (model error), 429 = rate limited (back off and retry), 500 = internal server error. 503 from `/health` means the server is not ready.

## Anomaly Flags

- **429 Too Many Requests**: Rate limit hit. Surface immediately with a retry-after recommendation. Back off exponentially before retrying.
- **424 Generation Failed**: The model encountered an error during generation (e.g., out of memory, bad input). Surface the error details and suggest reducing `max_new_tokens` or input length.
- **503 from /health**: Server is overloaded or starting up. Alert the user that the service is temporarily unavailable.
- **Token count approaching limits**: If `prompt_tokens` in a response is close to `max_input_tokens` (from `/info`), warn that longer inputs will be truncated or rejected.
- **`max_total_tokens` saturation**: When `prompt_tokens + completion_tokens` nears `max_total_tokens`, flag that generation was likely cut short.
- **`best_of` > 1 with streaming**: This combination is unsupported. Flag if the user attempts it.
- **Watermark enabled**: If `watermark: true` is set, note that output contains invisible watermarking which may affect downstream use.
- **Empty `generated_text`**: May indicate the model hit a stop sequence immediately or `max_new_tokens` was set to 0. Surface as a potential misconfiguration.

## Playbook

### 1. Basic Text Generation with Quality Control

1. Call `GET /info` to retrieve `max_input_tokens` and `max_total_tokens`.
2. Call `POST /tokenize` with your input to check token count against limits.
3. Call `POST /generate` with `inputs`, setting `parameters.max_new_tokens` to stay within `max_total_tokens - prompt_tokens`.
4. Set `parameters.details: true` to inspect `finish_reason` -- confirm it is `end_of_sequence_token` rather than `length` (which means output was truncated).

### 2. OpenAI-Compatible Chat with Tool Use

1. Call `GET /v1/models` to confirm the loaded model and its ID.
2. Build a `messages` array with system, user, and assistant roles.
3. Define tools in the `tools` array, each with `type: "function"` and a `function` object containing `name`, `description`, and JSON schema `arguments`.
4. Call `POST /v1/chat/completions` with `messages`, `tools`, and optionally `tool_choice` to force or auto-select tool use.
5. Parse `choices[0].message.tool_calls` to extract function names and arguments, execute them, then append results as tool-role messages and call again.

### 3. Streaming Generation with Monitoring

1. Call `GET /health` to verify the server is ready (expect 200).
2. Call `POST /generate_stream` with `inputs` and desired `parameters`.
3. Consume the SSE stream, processing each `data:` line as a JSON object containing a `token` field with incremental text.
4. Monitor for error events in the stream (HTTP errors surface as SSE error events).
5. After the stream ends, call `GET /metrics` to check queue depth and latency percentiles for operational awareness.

### 4. Adapter-Based Generation (LoRA)

1. Call `GET /info` to verify the server supports adapters (check `model_id` and configuration).
2. Call `POST /generate` with `inputs` and `parameters.adapter_id` set to the desired LoRA adapter name.
3. Set `parameters.details: true` to verify the adapter was applied (adapter info appears in details).
4. Compare outputs with and without the adapter to validate behavior differences.

### 5. Pre-flight Validation for Batch Processing

1. Call `GET /health` to confirm service availability.
2. Call `GET /info` to read `max_concurrent_requests`, `max_client_batch_size`, `max_input_tokens`, and `max_stop_sequences`.
3. For each input in your batch, call `POST /tokenize` to validate token counts are within `max_input_tokens`.
4. Send requests to `POST /generate` respecting `max_concurrent_requests` as your concurrency limit.
5. Monitor `GET /metrics` periodically to track queue saturation and adjust throughput.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
