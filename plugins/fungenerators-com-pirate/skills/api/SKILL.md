---
name: pirates-api
description: "Pirates API skill. Use when working with Pirates for pirate. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# Pirates API
API version: 1.5

## Auth
ApiKey X-Fungenerators-Api-Secret in header

## Base URL
https://api.fungenerators.com

## Setup
1. Set your API key in the appropriate header
2. GET /pirate/generate/name -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### pirate
| Method | Path | Description |
|--------|------|-------------|
| GET | /pirate/generate/name | Generate random pirate names. |
| GET | /pirate/generate/insult | Generate random pirate insults. |
| GET | /pirate/generate/lorem-ipsum | Generate pirate lorem ipsum. |
| GET | /pirate/translate | Translate from English to pirate. |

## Enhanced Skill Content
## Question Mapping

- "Generate a pirate name for me?" -> GET /pirate/generate/name
- "Give me 5 random pirate names?" -> GET /pirate/generate/name (limit=5)
- "Generate a pirate name with a specific variation?" -> GET /pirate/generate/name (variation=...)
- "Insult me like a pirate?" -> GET /pirate/generate/insult
- "Give me 3 pirate insults?" -> GET /pirate/generate/insult (limit=3)
- "Generate pirate-themed lorem ipsum text?" -> GET /pirate/generate/lorem-ipsum
- "Give me pirate filler text for a paragraph?" -> GET /pirate/generate/lorem-ipsum (type=paragraph)
- "Generate 2 sentences of pirate lorem ipsum?" -> GET /pirate/generate/lorem-ipsum (type=sentence&limit=2)
- "Translate this sentence into pirate speak?" -> GET /pirate/translate (text=...)
- "How would a pirate say 'hello friend'?" -> GET /pirate/translate (text=hello friend)
- "Convert my email draft to pirate language?" -> GET /pirate/translate (text=...)
- "Generate a pirate name and then insult that pirate?" -> GET /pirate/generate/name then GET /pirate/generate/insult
- "Create a pirate-themed page with a name, insult, and filler text?" -> GET /pirate/generate/name + GET /pirate/generate/insult + GET /pirate/generate/lorem-ipsum

## Response Tips

- **Name/Insult/Lorem-ipsum generation endpoints**: Results are returned in the response body; when `limit` > 1, expect an array of strings rather than a single value.
- **Translation endpoint**: Returns the pirate-translated version of the input text as a single string result.
- **All endpoints**: A 401 error means the API key is missing or invalid -- check the `X-Fungenerators-Api-Secret` header.

## Anomaly Flags

- **401 on every call**: API key is not set or has expired -- surface immediately and prompt the user to check their `X-Fungenerators-Api-Secret` header value.
- **Empty or truncated results**: If `limit` is set high but fewer results return, the API may be silently capping output -- flag the discrepancy.
- **Unusual latency on translate**: Long input text may cause slow responses -- warn if the text parameter exceeds ~500 characters.
- **Non-200 status codes other than 401**: The spec only documents 401 errors; any 403, 429, or 5xx response is unexpected and should be surfaced with the full status and body.

## Playbook

### 1. Generate a Pirate Identity

1. Call `GET /pirate/generate/name` to get a pirate name.
2. Call `GET /pirate/generate/insult` to get a signature insult for the character.
3. Combine the name and insult into a character profile for the user.

### 2. Translate Text to Pirate Speak

1. Collect the text the user wants translated.
2. Call `GET /pirate/translate?text={user_text}` with the input URL-encoded.
3. Return the translated pirate text to the user.

### 3. Generate Pirate-Themed Placeholder Content

1. Call `GET /pirate/generate/lorem-ipsum?type=paragraph&limit=3` for body filler.
2. Call `GET /pirate/generate/name?limit=5` to populate character placeholders.
3. Assemble the names and lorem ipsum into a themed mock page or document.

### 4. Bulk Pirate Content for a Party Invitation

1. Call `GET /pirate/generate/name?limit=1` to generate the host's pirate alias.
2. Call `GET /pirate/translate?text={invitation_text}` to convert the invite copy to pirate speak.
3. Call `GET /pirate/generate/insult?limit=3` to add humorous pirate insults as flavor text.
4. Combine all outputs into a formatted invitation.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
