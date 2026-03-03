---
name: apiwordnikcom
description: "api.wordnik.com API skill. Use when working with api.wordnik.com for word.json, words.json. Covers 16 endpoints."
version: 1.0.0
generator: lapsh
---

# api.wordnik.com
API version: 4.0

## Auth
ApiKey api_key in query

## Base URL
https://api.wordnik.com/v4

## Setup
1. Set your API key in the appropriate header
2. GET /words.json/randomWord -- verify access

## Endpoints

16 endpoints across 2 groups. See references/api-spec.lap for full details.

### word.json
| Method | Path | Description |
|--------|------|-------------|
| GET | /word.json/{word}/audio | Fetches audio metadata for a word. |
| GET | /word.json/{word}/definitions | Return definitions for a word |
| GET | /word.json/{word}/etymologies | Fetches etymology data |
| GET | /word.json/{word}/examples | Returns examples for a word |
| GET | /word.json/{word}/frequency | Returns word usage over time |
| GET | /word.json/{word}/hyphenation | Returns syllable information for a word |
| GET | /word.json/{word}/phrases | Fetches bi-gram phrases for a word |
| GET | /word.json/{word}/pronunciations | Returns text pronunciations for a given word |
| GET | /word.json/{word}/relatedWords | Given a word as a string, returns relationships from the Word Graph |
| GET | /word.json/{word}/scrabbleScore | Returns the Scrabble score for a word |
| GET | /word.json/{word}/topExample | Returns a top example for a word |

### words.json
| Method | Path | Description |
|--------|------|-------------|
| GET | /words.json/randomWord | Returns a single random WordObject |
| GET | /words.json/randomWords | Returns an array of random WordObjects |
| GET | /words.json/reverseDictionary | Reverse dictionary search |
| GET | /words.json/search/{query} | Searches words |
| GET | /words.json/wordOfTheDay | Returns a specific WordOfTheDay |

## Enhanced Skill Content
## Question Mapping

- "What does the word 'ephemeral' mean?" -> GET /word.json/{word}/definitions
- "How do you pronounce 'quinoa'?" -> GET /word.json/{word}/pronunciations
- "Where does the word 'algorithm' come from?" -> GET /word.json/{word}/etymologies
- "Can you use 'serendipity' in a sentence?" -> GET /word.json/{word}/examples
- "What is the Scrabble score for 'quixotic'?" -> GET /word.json/{word}/scrabbleScore
- "Give me a random word" -> GET /words.json/randomWord
- "Give me 10 random nouns" -> GET /words.json/randomWords
- "What's the word of the day?" -> GET /words.json/wordOfTheDay
- "What words are related to 'happy'?" -> GET /word.json/{word}/relatedWords
- "How is 'onomatopoeia' hyphenated?" -> GET /word.json/{word}/hyphenation
- "How often was 'internet' used between 1990 and 2020?" -> GET /word.json/{word}/frequency
- "What phrases include the word 'break'?" -> GET /word.json/{word}/phrases
- "Find words that mean 'a feeling of intense joy'" -> GET /words.json/reverseDictionary
- "Search for words starting with 'astro'" -> GET /words.json/search/{query}
- "Is there audio for the word 'schadenfreude'?" -> GET /word.json/{word}/audio

## Response Tips

- **Definitions** (`/definitions`): Returns an array of definition objects; filter by `partOfSpeech` to narrow results. Use `sourceDictionaries` to prefer specific lexicons. Empty arrays mean no definitions found, not an error.
- **Examples** (`/examples`, `/topExample`): `topExample` returns a single best-match object; `examples` returns a paginated list -- use `skip` and `limit` for paging.
- **Random words** (`/randomWord`, `/randomWords`): `randomWord` returns one object; `randomWords` returns an array. Use `limit` on `randomWords` to control count. Results vary per call by design.
- **Search & reverse dictionary** (`/search`, `/reverseDictionary`): Both support `skip`/`limit` pagination and part-of-speech filtering. `reverseDictionary` matches concept descriptions to words; `search` matches word patterns.
- **Related words** (`/relatedWords`): Returns grouped arrays keyed by relationship type (synonym, antonym, etc.). Use `relationshipTypes` to request specific groups and `limitPerRelationshipType` to cap each.
- **Frequency** (`/frequency`): Returns year-bucketed counts. Specify `startYear`/`endYear` to constrain the range.

## Anomaly Flags

- **Rate limit headers**: Monitor `X-RateLimit-Remaining` and `X-RateLimit-Limit` in response headers. Surface a warning when remaining calls drop below 10% of the limit.
- **Empty results for common words**: If definitions or examples return empty for a well-known word, flag that `useCanonical=true` may resolve the lookup (handles inflected forms).
- **403 or 401 responses**: Indicates missing or invalid `api_key`. Prompt the user to verify their API key is set and valid.
- **Unusual 404s**: The API returns 404 when a word is not in the corpus. Distinguish this from a malformed URL -- surface it as "word not found" rather than an error.
- **Large result sets without pagination**: If `limit` is not set on endpoints like `/examples` or `/randomWords`, warn that defaults may return fewer results than expected or that pagination is available.
- **Deprecated source dictionaries**: If a `sourceDictionaries` value returns empty results where it previously worked, flag possible deprecation of that source.

## Playbook

### 1. Build a Complete Word Profile

1. Call `GET /word.json/{word}/definitions` to get meanings across parts of speech
2. Call `GET /word.json/{word}/pronunciations` to get phonetic representations
3. Call `GET /word.json/{word}/etymologies` to get word origin
4. Call `GET /word.json/{word}/relatedWords` to get synonyms, antonyms, and other relations
5. Call `GET /word.json/{word}/topExample` to get a usage sentence
6. Combine all results into a structured word card

### 2. Find the Right Word (Reverse Lookup)

1. Call `GET /words.json/reverseDictionary?query={description}` with a plain-language concept description
2. Filter candidates by `includePartOfSpeech` if a specific word type is needed
3. For each top candidate, call `GET /word.json/{word}/definitions` to confirm the meaning fits
4. Optionally call `GET /word.json/{word}/examples` to verify real-world usage

### 3. Generate a Vocabulary Quiz

1. Call `GET /words.json/randomWords?limit=5&hasDictionaryDef=true&minCorpusCount=1000` to get quiz words
2. For each word, call `GET /word.json/{word}/definitions?limit=1` to get the correct answer
3. For each word, call `GET /word.json/{word}/relatedWords?relationshipTypes=synonym` to generate distractor options
4. Present each word with its correct definition and plausible alternatives

### 4. Explore Word Frequency Over Time

1. Call `GET /word.json/{word}/frequency?startYear=1800&endYear=2020` to get historical usage data
2. Call `GET /word.json/{word}/etymologies` to correlate frequency changes with word origin events
3. Compare multiple words by repeating step 1 for each term
4. Summarize trends (rising, declining, stable) and notable inflection points

### 5. Scrabble Word Validation and Strategy

1. Call `GET /words.json/search/{pattern}?allowRegex=true&minLength=2&maxLength=7` to find words matching available tiles
2. For each candidate, call `GET /word.json/{word}/scrabbleScore` to rank by point value
3. Call `GET /word.json/{word}/definitions?limit=1` to verify each word has a valid definition (challenge-proof)
4. Sort results by score descending and present the top plays


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
