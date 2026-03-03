---
name: word-associations-api
description: "Word Associations API skill. Use when working with Word Associations for json. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# Word Associations API
API version: 1.0

## Auth
ApiKey apikey in query

## Base URL
https://api.wordassociations.net/associations/v1.0

## Setup
1. Set your API key in the appropriate header
2. GET /json/search -- verify access
3. POST /json/search -- create first search

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### json
| Method | Path | Description |
|--------|------|-------------|
| GET | /json/search | Gets associations with the given word or phrase. |
| POST | /json/search | Gets associations with the given word or phrase. |

## Enhanced Skill Content
## Question Mapping

- "What words are associated with 'love'?" -> GET /json/search
- "Find associations for a word in Russian?" -> GET /json/search (with lang=ru)
- "Get stimulus-response associations for 'computer'?" -> GET /json/search (with type=stimulus or type=response)
- "How do I limit results to 10 associations?" -> GET /json/search (with limit=10)
- "What nouns are associated with 'ocean'?" -> GET /json/search (with pos=noun)
- "Can I search for associations of multiple words at once?" -> POST /json/search (text accepts multiple words)
- "How do I authenticate my requests?" -> GET /json/search (apikey query parameter required)
- "What languages are supported for word associations?" -> GET /json/search (lang parameter determines language)
- "How do I get pretty-printed JSON output?" -> GET /json/search (with indent=yes)
- "Find verb associations for 'run' in English?" -> GET /json/search (with lang=en, pos=verb)
- "What's the difference between GET and POST search?" -> Both hit /json/search; POST suits bulk or long text payloads
- "How do I get both stimulus and response associations?" -> GET /json/search (omit type or set type=all)
- "Why am I getting a 429 error?" -> Rate limit exceeded; back off and retry with delay
- "Can I filter associations by part of speech?" -> GET /json/search (pos parameter: noun, verb, adjective, etc.)

## Response Tips

- **Search results**: Response contains an array of association sets keyed by input word; each entry includes the stimulus word, part of speech, and a ranked list of associated words with their scores.
- **Errors 401/429/501**: 401 means missing or invalid apikey; 429 means rate limit hit (check response headers for reset timing); 501 means the requested language or feature is not supported.
- **Formatting**: When indent is set, response JSON is human-readable; omit for compact payloads in production use.

## Anomaly Flags

- **Rate limit approaching**: Surface 429 errors immediately and recommend backing off; watch for repeated 429s indicating the key is near its quota ceiling.
- **Empty association sets**: If a valid word returns zero associations, flag that the word may be too rare, misspelled, or unsupported in the requested language.
- **501 Not Implemented**: Proactively warn when a user attempts a language or feature combination the API does not support.
- **Authentication failures**: Flag repeated 401 errors - the API key may be expired, missing, or incorrectly passed (must be in query, not header).
- **Unexpected response shape**: If the response lacks the expected association array structure, flag a possible API version change or service degradation.

## Playbook

### 1. Basic Word Association Lookup

1. Set your `apikey` query parameter with a valid API key.
2. Send `GET /json/search?text=happy&lang=en&apikey=YOUR_KEY`.
3. Parse the response array for associated words and their scores.
4. Sort by score descending if not already ranked.

### 2. Bulk Association Lookup via POST

1. Prepare a list of words to look up (e.g., "sun", "moon", "star").
2. Send `POST /json/search` with `text`, `lang`, and `apikey` in the request body.
3. Iterate over the response; each input word maps to its own association set.
4. Handle any words that return empty results separately.

### 3. Filtered Part-of-Speech Exploration

1. Choose a seed word and target part of speech (e.g., `text=water&pos=verb`).
2. Send `GET /json/search?text=water&lang=en&pos=verb&apikey=YOUR_KEY`.
3. Review returned verbs associated with "water" (e.g., "flow", "drink", "pour").
4. Repeat with different `pos` values (noun, adjective) to build a word map.

### 4. Building a Word Association Graph

1. Start with a seed word: `GET /json/search?text=music&lang=en&limit=5&apikey=YOUR_KEY`.
2. Collect the top 5 associated words from the response.
3. For each associated word, repeat step 1 to get second-degree associations.
4. Deduplicate and map connections between words to form a graph structure.
5. Stop after 2-3 degrees to avoid exponential growth and rate limits.

### 5. Handling Errors and Rate Limits Gracefully

1. Wrap every request in error handling; check the HTTP status code first.
2. On 401: verify the `apikey` parameter is present and valid; re-authenticate if needed.
3. On 429: pause requests, wait for the rate limit window to reset, then retry.
4. On 501: log the unsupported language/feature and fall back to a supported alternative.
5. On network timeouts: retry once with exponential backoff before surfacing the failure.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
