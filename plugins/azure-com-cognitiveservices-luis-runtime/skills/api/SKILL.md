---
name: luis-runtime-client
description: "LUIS Runtime Client API skill. Use when working with LUIS Runtime Client for apps. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# LUIS Runtime Client
API version: 2.0

## Auth
ApiKey Ocp-Apim-Subscription-Key in header

## Base URL
Not specified.

## Setup
1. Set your API key in the appropriate header
2. GET /apps/{appId} -- verify access
3. POST /apps/{appId} -- create first apps

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### apps
| Method | Path | Description |
|--------|------|-------------|
| GET | /apps/{appId} | Gets predictions for a given utterance, in the form of intents and entities. The current maximum query size is 500 characters. |
| POST | /apps/{appId} | Gets predictions for a given utterance, in the form of intents and entities. The current maximum query size is 500 characters. |

## Enhanced Skill Content
## Question Mapping

- "How do I get a prediction from my LUIS app?" -> GET /apps/{appId}
- "How do I send an utterance to LUIS for intent recognition?" -> POST /apps/{appId}
- "Can I test my LUIS model with a query string parameter?" -> GET /apps/{appId}
- "How do I send a batch utterance via request body?" -> POST /apps/{appId}
- "How do I get predictions from my staging slot instead of production?" -> GET /apps/{appId} (set staging=true)
- "Can LUIS spell-check my query before prediction?" -> GET /apps/{appId} (set spellCheck=true + bing-spell-check-subscription-key)
- "How do I get entity details and all intents back from LUIS?" -> GET /apps/{appId} (set verbose=true)
- "How do I query LUIS without logging the request for active learning?" -> GET /apps/{appId} (set log=false)
- "How do I adjust timezone for datetimeV2 entity resolution?" -> POST /apps/{appId} (set timezoneOffset)
- "What auth do I need to call the LUIS runtime?" -> Requires `Ocp-Apim-Subscription-Key` header with your prediction key
- "Which endpoint should I use -- GET or POST -- for long utterances?" -> POST /apps/{appId} (GET has URL length limits)
- "How do I compare staging vs production predictions for the same query?" -> Call GET /apps/{appId} twice: once with staging=true, once without

## Response Tips

- **Prediction responses (200):** Top-level contains `query`, `topScoringIntent` (with `intent` and `score`), and `entities` array. When `verbose=true`, includes full `intents` array ranked by score. Entity objects vary by type -- prebuilt entities include `resolution` sub-objects.
- **Error responses:** Expect `error` object with `statusCode` and `message`. Common codes: 401 (bad/missing subscription key), 404 (invalid appId), 414 (query too long on GET -- switch to POST), 429 (rate limited).
- **Spell-check enrichment:** When enabled, response includes `alteredQuery` alongside original `query` showing the corrected text that was actually scored.

## Anomaly Flags

- **429 status code**: Rate limit hit. Surface the `Retry-After` header value and recommend backing off before retrying.
- **401 with valid-looking key**: The subscription key may be an authoring key instead of a prediction key, or assigned to the wrong region. Flag the mismatch.
- **Low top intent score**: If `topScoringIntent.score` falls below 0.5, flag that the model is uncertain and the utterance may need to be added to training data.
- **`None` intent winning**: If the top intent is `None`, the model found no match. Surface this as a coverage gap.
- **`alteredQuery` differs significantly from `query`**: Spell-check rewrote the input substantially. Flag so the user can verify the correction did not change meaning.
- **Staging and production returning different top intents for the same query**: Model drift between slots. Flag before publishing staging to production.
- **Deprecated v2.0 API**: LUIS v2.0 runtime is legacy. Surface a note recommending migration to v3.0 prediction endpoint when appropriate.

## Playbook

### 1. Get a Quick Prediction for a Single Utterance

1. Set the `Ocp-Apim-Subscription-Key` header to your LUIS prediction key.
2. Send `GET /apps/{appId}?q=book+a+flight+to+seattle`.
3. Read `topScoringIntent.intent` for the matched intent and `topScoringIntent.score` for confidence.
4. Iterate `entities` array to extract any recognized entities (e.g., destination = "seattle").

### 2. Send a Long or Complex Utterance via POST

1. Set the `Ocp-Apim-Subscription-Key` header.
2. Send `POST /apps/{appId}` with JSON body: `{"q": "your long utterance here"}`.
3. Optionally set `verbose=true` in the query string to get all scored intents, not just the top one.
4. Parse the response the same way as GET -- `topScoringIntent` and `entities`.

### 3. Compare Staging vs Production Before Publishing

1. Send `GET /apps/{appId}?q=test+utterance&staging=true` to get the staging prediction.
2. Send `GET /apps/{appId}?q=test+utterance` (no staging flag) to get the production prediction.
3. Compare `topScoringIntent` between both responses.
4. If intents or scores differ significantly, review training changes before publishing the staging model.

### 4. Enable Spell Check for Noisy User Input

1. Obtain a Bing Spell Check v7 subscription key from Azure.
2. Send `GET /apps/{appId}?q=boook+a+fliight&spellCheck=true&bing-spell-check-subscription-key=YOUR_BING_KEY`.
3. Check `alteredQuery` in the response to see the corrected text LUIS actually scored.
4. Use `topScoringIntent` from the corrected query for your application logic.

### 5. Query with Timezone-Aware Entity Resolution

1. Determine the user's UTC offset in minutes (e.g., US Pacific = -480).
2. Send `POST /apps/{appId}?timezoneOffset=-480` with body `{"q": "remind me tomorrow at 9am"}`.
3. Read the `entities` array for datetimeV2 types -- the `resolution` will reflect the correct local time.
4. If the offset is omitted, LUIS defaults to UTC, which may produce incorrect date/time values for the user.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
