---
name: dlx
description: "DLx API skill. Use when working with DLx for languages, lexemes. Covers 18 endpoints."
version: 1.0.0
generator: lapsh
---

# DLx
API version: 0.3.1

## Auth
ApiKey Authorization in header

## Base URL
https://api.digitallinguistics.io/v0

## Setup
1. Set your API key in the appropriate header
2. GET /languages -- verify access
3. POST /languages -- create first languages

## Endpoints

18 endpoints across 2 groups. See references/api-spec.lap for full details.

### languages
| Method | Path | Description |
|--------|------|-------------|
| GET | /languages | Get all Languages |
| POST | /languages | Add a new Language |
| PUT | /languages | Upsert (create or replace) a Language |
| GET | /languages/{languageID} | Retrieve a Language by ID |
| DELETE | /languages/{languageID} | Delete a Language by ID |
| PATCH | /languages/{languageID} | Perform a partial update on a Language |
| GET | /languages/{languageID}/lexemes | Get all Lexemes for a Language |
| POST | /languages/{languageID}/lexemes | Add a new Lexeme to a Language |
| PUT | /languages/{languageID}/lexemes | Upsert (add or replace) a Lexeme |
| GET | /languages/{languageID}/lexemes/{lexemeID} | Get a Lexeme by ID |
| DELETE | /languages/{languageID}/lexemes/{lexemeID} | Delete a Lexeme by ID |
| PATCH | /languages/{languageID}/lexemes/{lexemeID} | Perform a partial update on a Lexeme |

### lexemes
| Method | Path | Description |
|--------|------|-------------|
| GET | /lexemes | Get all Lexemes |
| POST | /lexemes | Add a new Lexeme |
| PUT | /lexemes | Upsert (add or replace) a Lexeme |
| GET | /lexemes/{lexemeID} | Get a Lexeme by ID |
| DELETE | /lexemes/{lexemeID} | Delete a Lexeme by ID |
| PATCH | /lexemes/{lexemeID} | Perform a partial update on a Lexeme |

## Enhanced Skill Content
## Question Mapping

- "What languages are available?" -> GET /languages
- "Show me all public languages" -> GET /languages (with `public` param)
- "Create a new language entry" -> POST /languages
- "Get details for a specific language" -> GET /languages/{languageID}
- "Delete a language" -> DELETE /languages/{languageID}
- "Update a field on an existing language" -> PATCH /languages/{languageID}
- "Replace an entire language record" -> PUT /languages
- "List all lexemes for a given language" -> GET /languages/{languageID}/lexemes
- "Add a word to a language's lexicon" -> POST /languages/{languageID}/lexemes
- "Look up a specific lexeme by ID" -> GET /lexemes/{lexemeID}
- "Search lexemes across all languages" -> GET /lexemes (with `languageID` filter)
- "Delete a lexeme from a language" -> DELETE /languages/{languageID}/lexemes/{lexemeID}
- "What lexemes were added or changed since last week?" -> GET /lexemes (with `ifModifiedSince`)
- "Get the next page of results" -> GET /languages or GET /lexemes (with `continuation` token)
- "Update a lexeme's definition without replacing the whole record" -> PATCH /lexemes/{lexemeID}

## Response Tips

- **Language/Lexeme lists (GET collections):** Responses use cursor-based pagination; check for a `continuation` token in the response and pass it back to fetch the next page. Use `maxItemCount` to control page size.
- **Single resource GETs:** Support conditional fetching via `ifNoneMatch`; a 304 means the resource has not changed since your last fetch -- reuse your cached copy.
- **Create/Replace (POST/PUT):** Return 201 on success; the response body contains the created or replaced resource. PUT is a full replace, POST is a create.
- **Partial updates (PATCH):** Return 200 with the updated resource. Use `ifMatch` for optimistic concurrency to avoid overwriting concurrent edits.
- **Deletes:** Return 204 with no body. Use `deleted` param on subsequent GETs to include soft-deleted resources.

## Anomaly Flags

- **304 Not Modified on GETs:** Surface when conditional requests return unchanged data so the agent avoids redundant processing.
- **Missing continuation token:** If a large collection returns no `continuation` value, flag that all results fit in a single page (or pagination may be misconfigured).
- **Optimistic concurrency conflicts:** If a PUT/PATCH/DELETE with `ifMatch` returns a 412 Precondition Failed, alert the user that the resource was modified by someone else since it was last fetched.
- **Soft-deleted resources:** When `deleted` param is used and results include deleted items, flag these clearly so the agent does not treat them as active records.
- **Empty lexeme lists:** When GET /languages/{languageID}/lexemes returns zero results, proactively note the language may be newly created or the languageID may be incorrect.
- **Public vs private visibility:** Flag when queries omit the `public` parameter, as results may default to only the user's own resources.

## Playbook

### 1. Add a New Language with Initial Lexemes

1. POST /languages with the language object in the body
2. Capture the `languageID` from the 201 response
3. POST /languages/{languageID}/lexemes for each word, passing the language ID in the path
4. GET /languages/{languageID}/lexemes to verify all lexemes were created

### 2. Paginate Through All Lexemes for a Language

1. GET /languages/{languageID}/lexemes with a desired `maxItemCount`
2. Read the `continuation` token from the response
3. Repeat GET /languages/{languageID}/lexemes with the `continuation` value until no token is returned
4. Merge all pages into a single result set

### 3. Sync Changes Since Last Fetch

1. Store the timestamp of your last successful sync
2. GET /languages with `ifModifiedSince` set to that timestamp
3. GET /lexemes with `ifModifiedSince` set to the same timestamp
4. Include `deleted=true` to also capture soft-deleted records
5. Update your local store and save the new sync timestamp

### 4. Safely Update a Lexeme (Optimistic Concurrency)

1. GET /lexemes/{lexemeID} and capture the `ETag` from the response headers
2. PATCH /lexemes/{lexemeID} with the changes in the body and `ifMatch` set to the captured ETag
3. If 200, the update succeeded -- use the response as the new current version
4. If 412, re-fetch the lexeme (step 1), merge changes, and retry

### 5. Remove a Language and Its Lexemes

1. GET /languages/{languageID}/lexemes to list all lexemes (paginate if needed)
2. DELETE /languages/{languageID}/lexemes/{lexemeID} for each lexeme
3. Confirm each returns 204
4. DELETE /languages/{languageID} to remove the language itself
5. GET /languages/{languageID} with `deleted=true` to verify it appears as soft-deleted


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object
- Error responses use types: 304

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
