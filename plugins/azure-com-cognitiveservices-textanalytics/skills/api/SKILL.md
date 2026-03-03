---
name: text-analytics-client
description: "Text Analytics Client API skill. Use when working with Text Analytics Client for keyPhrases, languages, sentiment. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# Text Analytics Client
API version: v2.1-preview

## Auth
ApiKey Ocp-Apim-Subscription-Key in header

## Base URL
Not specified.

## Setup
1. Set your API key in the appropriate header
3. POST /keyPhrases -- create first keyPhrases

## Endpoints

4 endpoints across 4 groups. See references/api-spec.lap for full details.

### keyPhrases
| Method | Path | Description |
|--------|------|-------------|
| POST | /keyPhrases | The API returns a list of strings denoting the key talking points in the input text. |

### languages
| Method | Path | Description |
|--------|------|-------------|
| POST | /languages | The API returns the detected language and a numeric score between 0 and 1. |

### sentiment
| Method | Path | Description |
|--------|------|-------------|
| POST | /sentiment | The API returns a numeric score between 0 and 1. |

### entities
| Method | Path | Description |
|--------|------|-------------|
| POST | /entities | The API returns a list of recognized entities in a given document. |

## Enhanced Skill Content
## Question Mapping

- "What are the key phrases in this text?" -> POST /keyPhrases
- "Extract important topics from these documents" -> POST /keyPhrases
- "What language is this text written in?" -> POST /languages
- "Detect the language of multiple documents at once" -> POST /languages
- "Is this review positive or negative?" -> POST /sentiment
- "Analyze the sentiment of customer feedback" -> POST /sentiment
- "What entities are mentioned in this article?" -> POST /entities
- "Extract people, places, and organizations from text" -> POST /entities
- "Score the tone of these support tickets" -> POST /sentiment
- "Identify named entities and link them to knowledge bases" -> POST /entities
- "What languages are represented in this batch of documents?" -> POST /languages
- "Summarize the main themes across these documents" -> POST /keyPhrases
- "Classify the sentiment of each sentence in a document" -> POST /sentiment
- "Find all company names mentioned in this press release" -> POST /entities

## Response Tips

- **Key Phrases** (`/keyPhrases`): Returns a `documents` array; each entry contains `id` and `keyPhrases` string array. Empty arrays mean no phrases met the confidence threshold. Check `errors` array for per-document failures.
- **Languages** (`/languages`): Each document returns `detectedLanguages` ranked by `score` (0-1). The top result is the best guess; low scores indicate uncertain detection. `iso6391Name` gives the standard language code.
- **Sentiment** (`/sentiment`): Returns a `score` between 0 (negative) and 1 (positive) per document. Scores near 0.5 indicate neutral or mixed sentiment, not confident classification. Absent scores signal processing errors.
- **Entities** (`/entities`): Returns nested `entities` with `name`, `type`, `subType`, and optional `wikipediaUrl`/`bingId`. Multiple matches per entity are ranked by relevance. Missing `type` means the entity was recognized but not classified.
- **All endpoints**: Partial failures return HTTP 200 with per-document errors in the `errors` array -- always check both `documents` and `errors` in every response.

## Anomaly Flags

- **Per-document errors**: Surface any entries in the `errors` array immediately -- these indicate documents that failed processing (bad encoding, unsupported language, exceeded size limits) while the overall request succeeded.
- **Rate limit headers**: Watch for `Retry-After` headers and HTTP 429 responses. Proactively warn when batching large volumes that approach the transactions-per-second quota.
- **Truncated input**: Documents exceeding 5,120 characters are silently truncated. Flag when input text is near or over this limit.
- **Low confidence scores**: Alert when language detection scores fall below 0.5 or sentiment scores cluster near 0.5 across a batch, suggesting ambiguous or mixed-language input.
- **Empty results**: Key phrases returning empty arrays or entities returning zero matches for non-trivial text may indicate an unsupported language or malformed input -- surface this rather than silently passing through.
- **API version deprecation**: This spec targets `v2.1-preview`. Flag if responses include deprecation warnings or if the user should consider migrating to a newer API version (v3.x+).

## Playbook

### 1. Analyze Customer Feedback (Sentiment + Key Phrases)

1. Prepare a `documents` array with each feedback entry as `{"id": "1", "language": "en", "text": "..."}`
2. Call `POST /sentiment` with `{"documents": [...]}` to score each entry
3. Call `POST /keyPhrases` with the same payload to extract themes
4. Correlate results by `id` -- pair sentiment scores with their key phrases
5. Group by score ranges (0-0.3 negative, 0.3-0.7 neutral, 0.7-1.0 positive) and surface top phrases per group

### 2. Process Multilingual Documents

1. Call `POST /languages` with `{"documents": [{"id": "1", "text": "..."}]}` (no `language` field needed)
2. Read `detectedLanguages[0].iso6391Name` for each document
3. Group documents by detected language
4. Call `POST /keyPhrases` or `POST /sentiment` per language group, setting the `language` field to the detected code
5. Merge results back by document `id`

### 3. Entity Extraction and Enrichment

1. Prepare documents with `id`, `language`, and `text` fields
2. Call `POST /entities` with the document batch
3. Filter results by `entity.type` (e.g., `Organization`, `Person`, `Location`) for targeted extraction
4. Use `wikipediaUrl` or `bingId` fields to enrich entities with external context
5. Deduplicate entities across documents by matching on `name` and `type`

### 4. Batch Processing Large Document Sets

1. Split documents into batches of up to 1,000 documents (API limit per request)
2. Ensure each document is under 5,120 characters; split longer documents into chunks sharing the same base `id`
3. Send each batch to the desired endpoint with a brief pause between calls to respect rate limits
4. Collect all responses and check every batch's `errors` array for partial failures
5. Retry failed documents from the `errors` array in a separate batch before merging final results

### 5. Real-Time Text Triage Pipeline

1. Receive incoming text (e.g., support ticket, social post)
2. Call `POST /languages` to detect language -- reject or route unsupported languages
3. Call `POST /sentiment` to classify urgency (low scores may indicate frustrated users)
4. Call `POST /entities` to extract mentioned products, people, or locations for routing
5. Combine all three results to auto-tag, prioritize, and assign the incoming text


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
