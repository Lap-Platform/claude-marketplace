---
name: shakespeare-api
description: "Shakespeare API skill. Use when working with Shakespeare for shakespeare. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# Shakespeare API
API version: 1.5

## Auth
ApiKey X-Fungenerators-Api-Secret in header

## Base URL
http://api.fungenerators.com

## Setup
1. Set your API key in the appropriate header
2. GET /shakespeare/generate/name -- verify access

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### shakespeare
| Method | Path | Description |
|--------|------|-------------|
| GET | /shakespeare/generate/name | Generate random Shakespearen names. |
| GET | /shakespeare/generate/insult | Generate random Shakespeare style insults. |
| GET | /shakespeare/generate/lorem-ipsum | Generate Shakespeare lorem ipsum. |
| GET | /shakespeare/translate | Translate from English to Shakespeare English. |
| GET | /shakespeare/quote | Get a random Shakespeare quote. |

## Enhanced Skill Content
## Question Mapping

- "Generate a Shakespearean name?" -> GET /shakespeare/generate/name
- "Give me a random Shakespeare-style name with a specific variation?" -> GET /shakespeare/generate/name
- "Generate multiple Shakespearean names at once?" -> GET /shakespeare/generate/name (use limit param)
- "Insult me like Shakespeare would?" -> GET /shakespeare/generate/insult
- "Give me 5 Shakespearean insults?" -> GET /shakespeare/generate/insult (limit=5)
- "Generate lorem ipsum text in Shakespearean style?" -> GET /shakespeare/generate/lorem-ipsum
- "Get Shakespearean filler text as sentences or paragraphs?" -> GET /shakespeare/generate/lorem-ipsum (use type param)
- "Translate this phrase into Shakespearean English?" -> GET /shakespeare/translate
- "How would Shakespeare say 'you are wrong'?" -> GET /shakespeare/translate (text=you are wrong)
- "Give me a random Shakespeare quote?" -> GET /shakespeare/quote
- "I need placeholder text for a Renaissance-themed project?" -> GET /shakespeare/generate/lorem-ipsum
- "Convert modern English to Early Modern English?" -> GET /shakespeare/translate
- "Generate a batch of lorem ipsum paragraphs?" -> GET /shakespeare/generate/lorem-ipsum (type=paragraphs, limit=N)

## Response Tips

- **Name/Insult/Quote generators**: Response body contains the generated text. When `limit` > 1, expect an array of results rather than a single string.
- **Lorem Ipsum**: The `type` parameter controls output granularity (words, sentences, paragraphs). Default behavior varies -- check the response shape to confirm.
- **Translate**: Returns the translated text. Input goes in the `text` query param -- URL-encode special characters and punctuation.
- **All endpoints**: 401 means the `X-Fungenerators-Api-Secret` header is missing or invalid. No other documented error codes -- treat unexpected status codes (429, 500) as transient.

## Anomaly Flags

- **401 on any call**: API key is missing, expired, or malformed. Surface immediately -- no endpoint will work until auth is fixed.
- **Empty or null results**: Generator endpoints may occasionally return empty arrays when the service is degraded. Flag if results come back empty despite valid parameters.
- **Rate limiting (429)**: Not documented but likely enforced. If responses slow down or return 429, surface the limit and suggest backing off.
- **Unusually short translation output**: If `/shakespeare/translate` returns text significantly shorter than input, the translation may have silently failed or truncated.
- **Deprecated API base URL**: The base URL uses plain HTTP (`http://api.fungenerators.com`). Flag this as a security concern -- check if HTTPS is available and prefer it.

## Playbook

### 1. Generate a themed character name list

1. Call `GET /shakespeare/generate/name` with `limit=10` to get a batch of names.
2. If you need a specific style, add the `variation` parameter.
3. Parse the response array and present the names as a numbered list.
4. Re-roll any you dislike by calling again with `limit=1`.

### 2. Translate a block of modern text to Shakespearean English

1. Split long text into sentence-sized chunks (the API may truncate long inputs).
2. For each chunk, call `GET /shakespeare/translate?text=<url-encoded-chunk>`.
3. Concatenate the translated results in order.
4. Review the output -- proper nouns and modern slang may not translate well.

### 3. Build a Renaissance-themed page with filler content

1. Call `GET /shakespeare/generate/lorem-ipsum?type=paragraphs&limit=3` for body text.
2. Call `GET /shakespeare/generate/name?limit=5` for character placeholders.
3. Call `GET /shakespeare/quote` for a decorative pull-quote.
4. Assemble the pieces into your template.

### 4. Create a Shakespearean insult generator bot

1. Call `GET /shakespeare/generate/insult?limit=1` on each user request.
2. Cache recent insults client-side to avoid repeats.
3. If a 401 is returned, prompt the user to check API key configuration.
4. Optionally pair each insult with a quote from `GET /shakespeare/quote` for comedic contrast.

### 5. Validate API connectivity and key

1. Call `GET /shakespeare/quote` with the `X-Fungenerators-Api-Secret` header set.
2. If 200 is returned, the key is valid and the API is reachable.
3. If 401 is returned, the key is invalid -- regenerate it from the Fun Generators dashboard.
4. If the request times out or returns 5xx, the API may be temporarily down -- retry after 30 seconds.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
