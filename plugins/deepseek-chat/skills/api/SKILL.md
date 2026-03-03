---
name: deepseek-chat-completion-api
description: "DeepSeek Chat Completion API skill. Use when working with DeepSeek Chat Completion for chat. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# DeepSeek Chat Completion API
API version: 1.0.0

## Auth
No authentication required.

## Base URL
https://api.deepseek.com

## Setup
1. No auth setup needed
3. POST /chat/completions -- create first completions

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### chat
| Method | Path | Description |
|--------|------|-------------|
| POST | /chat/completions | Create Chat Completion |

## Enhanced Skill Content
## Question Mapping

- "How do I send a message to DeepSeek?" -> POST /chat/completions
- "How do I use the deepseek-reasoner model?" -> POST /chat/completions (set model to `deepseek-reasoner`)
- "How do I stream a chat response?" -> POST /chat/completions (set `stream: true`)
- "How do I limit the response length?" -> POST /chat/completions (set `max_tokens`)
- "How do I call functions/tools with DeepSeek?" -> POST /chat/completions (set `tools` and `tool_choice`)
- "How do I get JSON output from DeepSeek?" -> POST /chat/completions (set `response_format: {type: "json_object"}`)
- "How do I set a system prompt?" -> POST /chat/completions (add a message with `role: "system"`)
- "How do I adjust creativity/randomness?" -> POST /chat/completions (adjust `temperature` or `top_p`)
- "How do I reduce repetition in responses?" -> POST /chat/completions (increase `frequency_penalty` or `presence_penalty`)
- "How do I get token log probabilities?" -> POST /chat/completions (set `logprobs: true`, optionally `top_logprobs`)
- "How do I make the model stop at a specific string?" -> POST /chat/completions (set `stop` sequences)
- "How do I check how many tokens a request used?" -> POST /chat/completions (inspect `usage` in response)
- "How do I have a multi-turn conversation?" -> POST /chat/completions (pass full message history in `messages` array)

## Response Tips

- **Chat completions**: Response contains `choices[]` with generated messages; check `choices[0].message.content` for the reply. `usage` holds `prompt_tokens`, `completion_tokens`, and `total_tokens` for cost tracking. When streaming, read incremental `choices[0].delta` chunks until `finish_reason` is non-null.

## Anomaly Flags

- **High token usage**: Surface `usage.total_tokens` when it approaches `max_tokens` -- the response may have been truncated (check `finish_reason: "length"`)
- **Finish reason**: Flag `finish_reason: "content_filter"` immediately -- content was blocked by safety filters
- **Tool calls incomplete**: If `finish_reason: "tool_calls"` appears, the model expects tool results before it can continue
- **Model mismatch**: Alert if the response `model` field differs from the requested model -- may indicate fallback or deprecation
- **Stream errors**: Surface mid-stream disconnections or malformed SSE chunks; partial responses may need retry
- **System fingerprint changes**: A changed `system_fingerprint` between calls may indicate backend model updates affecting reproducibility

## Playbook

### 1. Simple Chat Message

1. Set `model` to `deepseek-chat`
2. Build `messages` array with at least one entry: `{role: "user", content: "Your question here"}`
3. POST to `/chat/completions`
4. Read `choices[0].message.content` from the response

### 2. Multi-Turn Conversation with System Prompt

1. Start `messages` with `{role: "system", content: "You are a helpful assistant."}`
2. Append `{role: "user", content: "First question"}`
3. POST to `/chat/completions`, read the assistant reply
4. Append `{role: "assistant", content: "<reply from step 3>"}` to messages
5. Append next `{role: "user", content: "Follow-up question"}` and POST again

### 3. Streaming Response

1. Set `stream: true` in the request body
2. Optionally set `stream_options` for usage reporting in the stream
3. POST to `/chat/completions`
4. Read SSE chunks; concatenate `choices[0].delta.content` values
5. Stop when `choices[0].finish_reason` is `"stop"`

### 4. Tool/Function Calling

1. Define tools in the `tools` array (each with `type: "function"`, name, description, and parameters schema)
2. Optionally set `tool_choice` to force or suggest a specific function
3. POST to `/chat/completions`
4. If `finish_reason` is `"tool_calls"`, parse `choices[0].message.tool_calls` for function name and arguments
5. Execute the function locally, then POST again with the tool result appended as `{role: "tool", content: "<result>"}` to get the final answer

### 5. Reasoning with deepseek-reasoner

1. Set `model` to `deepseek-reasoner`
2. Build `messages` with the problem to reason about
3. POST to `/chat/completions`
4. Read `choices[0].message.content` for the reasoned answer
5. Check `usage` to monitor token consumption -- reasoning models tend to use more tokens


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
