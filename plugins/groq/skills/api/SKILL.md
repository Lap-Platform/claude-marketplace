---
name: groqcloud-api-swagger
description: "GroqCloud API Swagger API skill. Use when working with GroqCloud API Swagger for openai. Covers 7 endpoints."
version: 1.0.0
generator: lapsh
---

# GroqCloud API Swagger
API version: 2.0

## Auth
Bearer bearer

## Base URL
https://api.groq.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /openai/v1/models -- verify access
3. POST /openai/v1/audio/transcriptions -- create first transcriptions

## Endpoints

7 endpoints across 1 groups. See references/api-spec.lap for full details.

### openai
| Method | Path | Description |
|--------|------|-------------|
| POST | /openai/v1/audio/transcriptions | Transcribes audio into the input language. |
| POST | /openai/v1/audio/translations | Translates audio into English. |
| POST | /openai/v1/chat/completions | Creates a model response for the given chat conversation. |
| POST | /openai/v1/embeddings | Creates an embedding vector representing the input text. |
| GET | /openai/v1/models | List models |
| DELETE | /openai/v1/models/{model} | Delete model |
| GET | /openai/v1/models/{model} | Get model |

## Enhanced Skill Content
## Question Mapping

- "How do I send a chat message to Groq?" -> POST /openai/v1/chat/completions
- "Can I stream a response from Groq?" -> POST /openai/v1/chat/completions (set `stream: true`)
- "What models are available on Groq?" -> GET /openai/v1/models
- "How do I check details for a specific model?" -> GET /openai/v1/models/{model}
- "How do I delete a fine-tuned model?" -> DELETE /openai/v1/models/{model}
- "How do I transcribe an audio file?" -> POST /openai/v1/audio/transcriptions
- "Can I translate audio to English?" -> POST /openai/v1/audio/translations
- "How do I generate embeddings for text?" -> POST /openai/v1/embeddings
- "How do I call a function/tool through Groq?" -> POST /openai/v1/chat/completions (use `tools` and `tool_choice`)
- "How do I control randomness in completions?" -> POST /openai/v1/chat/completions (use `temperature` or `top_p`)
- "How do I get token usage stats for a request?" -> POST /openai/v1/chat/completions (read `usage` in response)
- "How do I limit response length?" -> POST /openai/v1/chat/completions (set `max_tokens`)
- "Can I get log probabilities for tokens?" -> POST /openai/v1/chat/completions (set `logprobs: true`, `top_logprobs`)
- "How do I get JSON output from the model?" -> POST /openai/v1/chat/completions (set `response_format: {type: "json_object"}`)

## Response Tips

- **Chat completions**: Response nests generated text inside `choices[].message.content`; `usage` includes Groq-specific timing fields (`completion_time`, `prompt_time`, `queue_time`) useful for performance profiling.
- **Models**: `GET /openai/v1/models` returns a flat list under `data`; no pagination -- the full catalog comes in one response.
- **Embeddings**: Vectors are in `data[].embedding`; set `encoding_format` to `base64` for smaller payloads over the wire.
- **Audio**: Both transcription and translation return a simple `{text}` object -- no segments or timestamps at this level.
- **Errors**: Expect standard HTTP error codes; 429 signals rate limiting, 401 means bad or missing Bearer token, 404 on model endpoints means the model ID does not exist.

## Anomaly Flags

- **Rate limit headers**: Surface `x-ratelimit-remaining` and `retry-after` headers when requests return 429; warn the user before they hit the wall if remaining count is low.
- **Queue time spikes**: If `usage.queue_time` exceeds `usage.completion_time`, flag that the request spent more time waiting than generating -- the user may want to retry or switch models.
- **Model deletion on non-fine-tuned models**: `DELETE /openai/v1/models/{model}` on a base model will fail; warn if the user targets a model whose `owned_by` is not their org.
- **Token budget overrun**: When `usage.total_tokens` approaches known model context limits, proactively warn that the conversation may need truncation.
- **Deprecated or unknown model IDs**: If a model ID passed to chat/embeddings is not in the list returned by `GET /openai/v1/models`, flag it before sending the request.
- **Stream mode misuse**: If the user sets `stream: true` but does not handle server-sent events, warn that the response format changes from JSON to SSE chunks.

## Playbook

### 1. Basic Chat Completion

1. Call `GET /openai/v1/models` to list available models and pick one (e.g., `llama-3.3-70b-versatile`).
2. Send `POST /openai/v1/chat/completions` with `model` and `messages` array (at minimum a user message).
3. Read the reply from `choices[0].message.content`.
4. Check `usage.total_tokens` to track consumption.

### 2. Tool-Augmented Chat (Function Calling)

1. Define your tools in the `tools` array, each with `type: "function"` and a `function` object containing `name`, `description`, and `parameters` (JSON Schema).
2. Send `POST /openai/v1/chat/completions` with the tools and your messages.
3. If the response `choices[0].message.tool_calls` is present, execute the requested function locally.
4. Append the tool result as a message with `role: "tool"` and the matching `tool_call_id`.
5. Send the updated messages back to get the model's final answer.

### 3. Audio Transcription and Translation

1. Prepare an audio file (mp3, wav, m4a, etc.).
2. Send `POST /openai/v1/audio/transcriptions` with the file as multipart form data to get text in the original language.
3. If translation to English is needed, send `POST /openai/v1/audio/translations` instead.
4. Extract the transcribed/translated text from `response.text`.

### 4. Generating and Using Embeddings

1. Call `POST /openai/v1/embeddings` with `model` set to an embedding model and `input` set to your text (string or array of strings).
2. Retrieve vectors from `data[].embedding`.
3. Store vectors in your vector database for similarity search.
4. For smaller payloads, set `encoding_format: "base64"` and decode client-side.

### 5. Model Discovery and Cleanup

1. Call `GET /openai/v1/models` to see all models available to your account.
2. For details on a specific model, call `GET /openai/v1/models/{model}` to see `created`, `owned_by`, and other metadata.
3. To remove a fine-tuned model you no longer need, call `DELETE /openai/v1/models/{model}`.
4. Confirm deletion by checking that `deleted: true` in the response.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
