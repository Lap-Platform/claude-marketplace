---
name: wealthreader-api-legacy-placeholder-not-official-documentation
description: "Wealthreader API — Legacy Placeholder (Not Official Documentation) API skill. Use when working with Wealthreader API — Legacy Placeholder (Not Official Documentation) for root, docs. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# Wealthreader API — Legacy Placeholder (Not Official Documentation)
API version: 1.0.0

## Auth
No authentication required.

## Base URL
https://virtserver.swaggerhub.com/Wealth-Reader/api/1.0.0

## Setup
1. No auth setup needed
2. GET / -- verify access

## Endpoints

3 endpoints across 2 groups. See references/api-spec.lap for full details.

### root
| Method | Path | Description |
|--------|------|-------------|
| GET | / | Landing (not official docs) |

### docs
| Method | Path | Description |
|--------|------|-------------|
| GET | /docs | List supported language branches |
| GET | /docs/{lang} | Documentation notice by language (legacy placeholder) |

## Enhanced Skill Content
## Question Mapping

- "Is the Wealthreader API running?" -> GET /
- "What languages does the Wealthreader API support?" -> GET /docs
- "Get the documentation in English" -> GET /docs/{lang}
- "Show me the API root info" -> GET /
- "What SEO metadata does the API expose?" -> GET /
- "Is this the official Wealthreader documentation?" -> GET /
- "List all available documentation languages" -> GET /docs
- "Fetch Spanish documentation" -> GET /docs/{lang}
- "What is the API headline for SEO?" -> GET /
- "Get docs in French and check if they are official" -> GET /docs/{lang}
- "Which languages can I request docs in?" -> GET /docs
- "Check API health and supported languages" -> GET /
- "Get localized documentation and its SEO keywords" -> GET /docs/{lang}

## Response Tips

- **Root (GET /)**: Response includes optional fields (`language`, `languages_supported`, `seo`) that may be null. Always check `is_official_documentation` -- this is a legacy placeholder, not the official source.
- **Docs listing (GET /docs)**: Returns a flat `languages` array of string codes. Use these values directly as the `{lang}` path parameter.
- **Docs by language (GET /docs/{lang})**: Same shape as root response. The `seo` object is optional; when present it contains `headline` (string) and `keywords` (array). Validate `ok` before consuming other fields.

## Anomaly Flags

- **`is_official_documentation: false`**: Surface immediately. This API is a legacy placeholder and responses should not be treated as authoritative Wealthreader documentation.
- **Missing optional fields**: If `seo`, `languages_supported`, or `language` come back null, flag this as incomplete metadata worth noting to the user.
- **Unknown language code**: If GET /docs/{lang} returns an error or unexpected shape, flag that the language may not be supported and suggest calling GET /docs first.
- **Base URL is SwaggerHub virtual server**: The base URL points to `virtserver.swaggerhub.com`, meaning responses are mocked. Surface this if the user expects live data.

## Playbook

### 1. Check API availability and capabilities

1. Call GET / to confirm the API is reachable (`ok: true`).
2. Note `is_official_documentation` -- if false, inform the user this is a placeholder.
3. Read `languages_supported` from the response for a quick overview.

### 2. Retrieve documentation in a specific language

1. Call GET /docs to list all available language codes.
2. Confirm the desired language code exists in the `languages` array.
3. Call GET /docs/{lang} with the matching code.
4. Check `ok` in the response, then extract `title`, `message`, and `seo` fields.

### 3. Extract SEO metadata

1. Call GET / to retrieve root-level SEO data.
2. If `seo` is present, read `headline` and `keywords`.
3. Optionally call GET /docs/{lang} for language-specific SEO metadata.
4. Compare keywords across languages to identify localization gaps.

### 4. Enumerate all localized documentation

1. Call GET /docs to get the full list of language codes.
2. For each code in the `languages` array, call GET /docs/{lang}.
3. Collect `title`, `message`, and `seo` from each response.
4. Flag any language where `ok` is false or optional fields are missing.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
