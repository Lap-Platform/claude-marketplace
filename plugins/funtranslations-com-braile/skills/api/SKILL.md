---
name: funtranslations-braille-api
description: "FunTranslations Braille API skill. Use when working with FunTranslations Braille for translate. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# FunTranslations Braille API
API version: 2.3

## Auth
ApiKey X-Funtranslations-Api-Secret in header

## Base URL
https://api.funtranslations.com

## Setup
1. Set your API key in the appropriate header
2. GET /translate/braille -- verify access

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### translate
| Method | Path | Description |
|--------|------|-------------|
| GET | /translate/braille | Translate from English to Braille. This is what you use if you have a braille display. This API translates the English text into characters that a braille display understands and you can feed the translated text directly to the display. |
| GET | /translate/braille/dots | Use this to see which dots are enabled for each Braille letters. This is highly educational (to see which dots are enabled) and can potentially drive a non braille display which works on individual dots. |
| GET | /translate/braille/unicode | Translate from English to Braille Unicode characters. |
| GET | /translate/braille/image | Translate from English to Braille image characters. This is probably what you want to use if you are displaying braille in a browser. |
| GET | /translate/braille/html | Translate from English to Braille Image characters. This is probably what you want to use if you are displaying braille in a browser. |

## Enhanced Skill Content


## Question Mapping

- "How do I convert text to braille?" -> GET /translate/braille
- "Can I get braille as dot notation (like 1-2-4-5)?" -> GET /translate/braille/dots
- "How do I get braille Unicode characters for display?" -> GET /translate/braille/unicode
- "Can I generate a braille image from text?" -> GET /translate/braille/image
- "How do I render braille in a web page?" -> GET /translate/braille/html
- "What braille output formats are available?" -> GET /translate/braille (then try /dots, /unicode, /image, /html)
- "How do I translate a sentence to braille dots pattern?" -> GET /translate/braille/dots
- "Can I get an image file of braille for a given phrase?" -> GET /translate/braille/image
- "How do I embed braille output directly into HTML?" -> GET /translate/braille/html
- "What happens if I forget the API key?" -> Any endpoint returns 401
- "How do I authenticate my requests?" -> Set `X-Funtranslations-Api-Secret` header
- "Is there a way to get both Unicode braille and dot notation for the same text?" -> Call GET /translate/braille/unicode then GET /translate/braille/dots with same `text` param
- "How do I batch-translate multiple strings to braille?" -> Loop GET /translate/braille per string (no batch endpoint)

## Response Tips

- **All /translate/braille/* endpoints**: Response body contains a `contents` object with `translated` (the result) and `text` (the original input). Check `contents.translated` for output.
- **401 errors**: Missing or invalid `X-Funtranslations-Api-Secret` header. Free tier exists but is heavily rate-limited.
- **Rate limits**: Free tier allows ~5 calls/hour, ~60/day. Response headers or 429 status indicate exhaustion. Paid keys raise limits.
- **/braille/image**: Response may be binary image data or a URL to the rendered image -- inspect `Content-Type` header.

## Anomaly Flags

- **Rate limit exhaustion**: Surface immediately when a 429 response is received or response includes rate-limit headers near zero remaining. Free tier is very restrictive (5/hour).
- **401 on previously working key**: API secret may have been rotated or revoked. Prompt user to verify their key.
- **Empty `translated` field**: Input text may contain characters outside supported braille mapping. Flag to user with the original input.
- **Slow responses from /braille/image**: Image generation takes longer than text endpoints. Flag if response time exceeds 5s.
- **Deprecation headers**: If any `Deprecation` or `Sunset` header appears in responses, surface immediately -- FunTranslations has historically retired endpoints without long notice.

## Playbook

### 1. Translate Text to Braille (Quick Start)

1. Set the `X-Funtranslations-Api-Secret` header with your API key (or omit for free-tier trial).
2. Call `GET /translate/braille?text=hello world`.
3. Read `contents.translated` from the JSON response for the braille output.

### 2. Generate a Braille Image for Download or Display

1. Authenticate with `X-Funtranslations-Api-Secret`.
2. Call `GET /translate/braille/image?text=Your text here`.
3. Check the response `Content-Type` -- if binary, save directly; if JSON, extract the image URL from the response body.
4. Render or download the image as needed.

### 3. Embed Braille in a Web Page

1. Call `GET /translate/braille/html?text=Your text here` with your API key.
2. Extract the HTML fragment from `contents.translated`.
3. Inject the fragment into your page DOM. The HTML is self-contained and renderable.

### 4. Get Multiple Braille Formats for the Same Text

1. Define your input text once as a variable.
2. Call `GET /translate/braille/unicode?text=...` for display-ready Unicode characters.
3. Call `GET /translate/braille/dots?text=...` for numeric dot-pattern notation.
4. Call `GET /translate/braille?text=...` for the default representation.
5. Combine outputs as needed. Watch rate limits -- this uses 3 calls.

### 5. Handle Rate Limit Exhaustion Gracefully

1. Before calling any endpoint, check if you've tracked recent call counts (5/hour free-tier limit).
2. If a 429 response is received, parse the `Retry-After` header (if present) for wait time.
3. Queue pending translations and retry after the cooldown period.
4. If rate limits are consistently blocking work, prompt the user to upgrade to a paid API key.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
