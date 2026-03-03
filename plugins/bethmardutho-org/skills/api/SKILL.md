---
name: sedra-iv-api
description: "SEDRA IV API skill. Use when working with SEDRA IV for word, lexeme. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# SEDRA IV API
API version: 1.0.0

## Auth
No authentication required.

## Base URL
http://sedra.bethmardutho.org/api

## Setup
1. No auth setup needed
2. GET /word/{id} -- verify access

## Endpoints

2 endpoints across 2 groups. See references/api-spec.lap for full details.

### word
| Method | Path | Description |
|--------|------|-------------|
| GET | /word/{id} | Get Syriac word. |

### lexeme
| Method | Path | Description |
|--------|------|-------------|
| GET | /lexeme/{id} | Get Syriac lexeme. |

## Enhanced Skill Content
## Question Mapping

- "Look up a Syriac word by its ID?" -> GET /word/{id}
- "Get details for word 500?" -> GET /word/{id}
- "What does SEDRA word entry 1234 contain?" -> GET /word/{id}
- "Fetch morphological data for a specific word?" -> GET /word/{id}
- "Retrieve a lexeme by ID?" -> GET /lexeme/{id}
- "Get the dictionary entry for lexeme 42?" -> GET /lexeme/{id}
- "What root does lexeme 100 belong to?" -> GET /lexeme/{id}
- "Find the lemma form for a given lexeme?" -> GET /lexeme/{id}
- "Look up a word and then find its parent lexeme?" -> GET /word/{id}, then GET /lexeme/{id}
- "Get the base form for word 750?" -> GET /word/{id}, then GET /lexeme/{id} using the lexeme reference from the word response
- "What grammatical features does word 300 have?" -> GET /word/{id}
- "Does this word ID exist in SEDRA?" -> GET /word/{id}

## Response Tips

- **word**: Responses include morphological attributes (person, gender, number, state) and a reference to the parent lexeme. Extract the lexeme ID from the response to chain lookups.
- **lexeme**: Responses contain the root/lemma form and lexical category. These are dictionary-level entries that group related word forms.
- **General**: Both endpoints return 200 on success. Non-existent IDs may return empty results or error objects rather than 404 -- check the response body, not just the status code.

## Anomaly Flags

- **Non-existent ID**: Surface immediately if the API returns an empty or null result for a requested ID -- the user likely has a wrong reference.
- **Server unavailability**: The SEDRA API is an academic resource (`bethmardutho.org`) and may have limited uptime. Flag connection failures with a note that this is a third-party academic server.
- **No pagination**: This API serves single records by ID. If a user expects list/search functionality, proactively inform them that SEDRA IV only supports direct ID lookups.
- **HTTP (not HTTPS)**: The base URL uses plain HTTP. Flag this if the user is transmitting or processing sensitive data alongside API calls.
- **Unexpected response shape**: If a response lacks expected fields (e.g., missing morphological data on a word), surface it -- the record may be incomplete in the database.

## Playbook

### 1. Look Up a Word and Its Dictionary Entry

1. Call `GET /word/{id}` with the known word ID
2. Parse the response for morphological features and the lexeme reference
3. Extract the lexeme ID from the word response
4. Call `GET /lexeme/{id}` with the extracted lexeme ID
5. Combine both responses to present the full picture: word form + dictionary entry

### 2. Verify a SEDRA ID Exists

1. Call `GET /word/{id}` or `GET /lexeme/{id}` depending on the ID type
2. Check if the response contains valid data or is empty/error
3. Report back whether the entry exists and summarize its contents if found

### 3. Compare Two Word Forms

1. Call `GET /word/{id}` for the first word ID
2. Call `GET /word/{id}` for the second word ID (run in parallel)
3. Compare morphological attributes (person, gender, number, state)
4. If both reference the same lexeme ID, note they share a dictionary entry
5. Summarize the grammatical differences between the two forms

### 4. Explore a Lexeme's Details

1. Start with `GET /lexeme/{id}` using the known lexeme ID
2. Review the root form, lexical category, and any semantic metadata
3. If the user wants related word forms, note that reverse lookup (lexeme -> words) is not available via this API -- only forward lookup (word -> lexeme) is supported


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
