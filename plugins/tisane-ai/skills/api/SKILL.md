---
name: tisane-api-documentation
description: "Tisane API Documentation API skill. Use when working with Tisane API Documentation for parse, languages, helper. Covers 8 endpoints."
version: 1.0.0
generator: lapsh
---

# Tisane API Documentation

## Auth
ApiKey Ocp-Apim-Subscription-Key in header

## Base URL
https://api.tisane.ai

## Setup
1. Set your API key in the appropriate header
2. GET /languages -- verify access
3. POST /parse -- create first parse

## Endpoints

8 endpoints across 8 groups. See references/api-spec.lap for full details.

### parse
| Method | Path | Description |
|--------|------|-------------|
| POST | /parse | Analyze text |

### languages
| Method | Path | Description |
|--------|------|-------------|
| GET | /languages | List available languages |

### helper
| Method | Path | Description |
|--------|------|-------------|
| POST | /helper/extract_text | Text clean up |

### compare
| Method | Path | Description |
|--------|------|-------------|
| POST | /compare/entities | Named entity comparison |

### similarity
| Method | Path | Description |
|--------|------|-------------|
| POST | /similarity | Semantic similarity |

### detectLanguage
| Method | Path | Description |
|--------|------|-------------|
| POST | /detectLanguage | Detect language |

### transform
| Method | Path | Description |
|--------|------|-------------|
| POST | /transform | Translate text |

### lm
| Method | Path | Description |
|--------|------|-------------|
| GET | /lm/inflections | List inflected forms |

## Enhanced Skill Content
## Question Mapping

- "Analyze the sentiment of this text?" -> POST /parse
- "What topics are discussed in this paragraph?" -> POST /parse
- "Is there any abusive content in this message?" -> POST /parse
- "Extract named entities from this document?" -> POST /parse
- "What languages does Tisane support?" -> GET /languages
- "Is this language written right-to-left?" -> GET /languages
- "Extract plain text from a file or HTML?" -> POST /helper/extract_text
- "Are these two entities the same person or thing?" -> POST /compare/entities
- "How similar are these two pieces of text?" -> POST /similarity
- "What language is this text written in?" -> POST /detectLanguage
- "Can you detect multiple languages in a mixed-language post?" -> POST /detectLanguage
- "Transform or rephrase this text?" -> POST /transform
- "What are all the inflected forms of this word?" -> GET /lm/inflections
- "Is this word form the lemma or a conjugation?" -> GET /lm/inflections
- "Analyze a text for topics, sentiment, and entities together?" -> POST /parse

## Response Tips

- **Parse responses** vary by requested features: check for `topics`, `abuse`, `sentiment_expressions`, `entities_summary`, and `sentence_list` fields -- absent keys mean that feature was not requested, not that results are empty.
- **Languages** returns flat objects per language; filter by `latin`, `rightToLeft`, or `nativeEncoding` to narrow results for locale-specific workflows.
- **Compare/entities** returns a `result` string (match/mismatch) plus a `differences` array; an empty array means the entities are considered equivalent.
- **Detect language** returns a `languages` array ranked by confidence; always check multiple entries for mixed-language or ambiguous input.
- **Inflections** returns an array of feature maps with `text` forms; look for `isLemma: true` to identify the base form among results.
- **Transform/similarity/extract_text** have untyped responses; inspect the raw body and adapt parsing based on the transformation or extraction requested.

## Anomaly Flags

- **Missing API key**: All endpoints accept `Ocp-Apim-Subscription-Key` as optional in the spec, but requests without it will likely fail with 401/403 -- surface auth errors immediately and prompt for key setup.
- **Empty parse arrays**: If `abuse`, `topics`, or `entities_summary` come back as empty arrays, flag that the input may be too short, ambiguous, or in an unsupported language.
- **Language detection uncertainty**: When the top result in `/detectLanguage` has low confidence or multiple languages score similarly, warn the user before proceeding with downstream parse calls.
- **Inflection misses**: If `/lm/inflections` returns no results for a valid-looking word, the language code or word family may be wrong -- suggest verifying against `/languages`.
- **Rate limiting**: Watch for 429 status codes or `Retry-After` headers; surface remaining quota if response headers include rate limit metadata.
- **Unexpected 200 with empty body**: `/similarity`, `/transform`, and `/helper/extract_text` have untyped 200 responses -- flag empty or malformed bodies rather than silently passing them through.

## Playbook

### 1. Full Text Analysis (Topics + Sentiment + Entities)

1. Call `POST /parse` with the text and settings requesting topics, sentiment, and entity extraction.
2. Read `topics` for subject classification.
3. Iterate `sentiment_expressions` for per-phrase sentiment polarity.
4. Iterate `entities_summary` for detected people, places, organizations.
5. If `abuse` is present and non-empty, surface flagged content with severity.

### 2. Language Detection then Parse

1. Call `POST /detectLanguage` with the raw text.
2. Read the top entry from the `languages` array to get the detected language code.
3. If confidence is low or multiple candidates are close, ask the user to confirm.
4. Call `POST /parse` using the detected language code in the request body.
5. Process the parse response for topics, entities, or sentiment as needed.

### 3. Entity Comparison Across Documents

1. Call `POST /parse` on Document A to extract `entities_summary`.
2. Call `POST /parse` on Document B to extract `entities_summary`.
3. For each entity pair to compare, call `POST /compare/entities` with both entity representations.
4. Check the `result` field for match status and `differences` for specific discrepancies.
5. Summarize which entities match and which diverge across documents.

### 4. Linguistic Inflection Lookup

1. Call `GET /languages` to confirm the target language is supported and get its code.
2. Call `GET /lm/inflections` with `language`, `lexeme` (the word), and `family` (part of speech).
3. Scan results for the entry where `isLemma: true` to identify the base form.
4. Present the full inflection table grouped by `features` (tense, case, number, etc.).

### 5. Content Moderation Pipeline

1. Call `POST /helper/extract_text` if input is HTML or a document format to get plain text.
2. Call `POST /detectLanguage` on the extracted text to identify the language.
3. Call `POST /parse` with abuse detection enabled for the detected language.
4. Check the `abuse` array: if non-empty, flag the content with abuse type and severity.
5. Optionally check `sentiment_expressions` for strongly negative sentiment as a secondary signal.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
