---
name: starwars-translations-api
description: "Starwars Translations API skill. Use when working with Starwars Translations for translate. Covers 6 endpoints."
version: 1.0.0
generator: lapsh
---

# Starwars Translations API
API version: 2.3

## Auth
ApiKey X-Funtranslations-Api-Secret in header

## Base URL
https://api.funtranslations.com

## Setup
1. Set your API key in the appropriate header
2. GET /translate/yoda -- verify access

## Endpoints

6 endpoints across 1 groups. See references/api-spec.lap for full details.

### translate
| Method | Path | Description |
|--------|------|-------------|
| GET | /translate/yoda | Translate from English to Yoda Speak. |
| GET | /translate/sith | Translate from English to Sith Speak. |
| GET | /translate/cheunh | Translate from English to Starwars cheunh. |
| GET | /translate/gungan | Translate from English to Starwars Gungan Language. |
| GET | /translate/mandalorian | Translate from English to Starwars Mandalorian Language. |
| GET | /translate/huttese | Translate from English to Starwars Huttese Language. |

## Enhanced Skill Content
## Question Mapping

- "How do I translate text to Yoda speak?" -> GET /translate/yoda
- "Can you convert this sentence into Sith language?" -> GET /translate/sith
- "Translate this phrase into Cheunh (Chiss language)?" -> GET /translate/cheunh
- "How would a Gungan say this?" -> GET /translate/gungan
- "What does this sound like in Mandalorian?" -> GET /translate/mandalorian
- "Translate this text into Huttese?" -> GET /translate/huttese
- "What Star Wars languages are available for translation?" -> GET /translate/yoda (list all 6 endpoints)
- "Can I translate without an API key?" -> GET /translate/yoda (will return 401)
- "How do I batch-translate a paragraph into multiple Star Wars languages?" -> GET /translate/yoda + GET /translate/sith + ...
- "What happens if I send an empty text to the Yoda translator?" -> GET /translate/yoda
- "Is there a Wookiee translation endpoint?" -> None (not available; only yoda, sith, cheunh, gungan, mandalorian, huttese)
- "How do I check if my API key is valid?" -> GET /translate/yoda (test with minimal input)
- "Translate a movie quote into every available Star Wars language?" -> GET /translate/yoda, sith, cheunh, gungan, mandalorian, huttese (fan-out)

## Response Tips

- **Translation endpoints** (`/translate/*`): Response contains `success.total` (result count) and `contents.translated` (the translated text), `contents.text` (original input), and `contents.translation` (language name). Always read `contents.translated` for the result.
- **Auth errors (401)**: Returned when `X-Funtranslations-Api-Secret` header is missing or invalid. The body includes an `error.message` field describing the issue. Free-tier keys have a rate limit of 5 calls/hour and 60 calls/day.
- **Rate limit errors (429)**: Treated as a soft 401 on the free tier. Check `error.message` for "Too Many Requests" wording. No `Retry-After` header is provided; back off for at least 60 seconds.

## Anomaly Flags

- **Rate limit approaching**: The free tier allows only 5 requests/hour. After 3-4 calls in quick succession, warn the user that the hourly cap is nearly exhausted.
- **401 on previously working key**: May indicate the daily limit (60/day) has been hit rather than an invalid key. Surface the distinction to the user.
- **Empty or identical translation**: Some phrases pass through unchanged (especially short words or proper nouns). Flag when `contents.translated` equals `contents.text` exactly, as the translation may not have applied.
- **Unexpected language in response**: If `contents.translation` does not match the requested endpoint (e.g., calling `/translate/sith` but getting `"yoda"`), flag as a potential API anomaly.
- **Missing `text` parameter**: All endpoints require the `text` query parameter. If omitted, the API may return a 200 with empty or null translated content rather than an error. Flag when the response contains no meaningful translation.

## Playbook

### 1. Translate Text into a Single Star Wars Language

1. Choose the target language endpoint (e.g., `/translate/yoda`).
2. Set the `X-Funtranslations-Api-Secret` header with your API key.
3. Send a GET request with `?text=Your sentence here` (URL-encode the text).
4. Read `contents.translated` from the response for the result.

### 2. Compare a Phrase Across All Star Wars Languages

1. Prepare the source text and URL-encode it.
2. Send parallel GET requests to all 6 endpoints: `/translate/yoda`, `/translate/sith`, `/translate/cheunh`, `/translate/gungan`, `/translate/mandalorian`, `/translate/huttese`.
3. Collect `contents.translated` from each response.
4. Present results side-by-side, noting any that returned the original text unchanged.
5. Be mindful of rate limits: on the free tier, this single fan-out uses 6 of your 5/hour quota. Use a paid key or space calls across hours.

### 3. Validate Your API Key

1. Send a minimal test request: `GET /translate/yoda?text=hello` with your API key header.
2. If 200 with `contents.translated` populated, the key is valid and active.
3. If 401, check `error.message` to distinguish between invalid key vs. rate limit exhaustion.
4. If rate-limited, wait at least 60 seconds before retrying.

### 4. Handle Rate Limit Exhaustion Gracefully

1. Track the number of requests made in the current hour (client-side counter).
2. When the counter reaches 4 (free tier), warn the user before the next call.
3. On a 401 with rate-limit wording, stop sending requests and surface the wait time.
4. Suggest upgrading to a paid plan if the user needs higher throughput.
5. Reset the counter each clock hour.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
