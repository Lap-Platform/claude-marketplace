---
name: random-riddles-api
description: "Random Riddles API skill. Use when working with Random Riddles for riddle. Covers 6 endpoints."
version: 1.0.0
generator: lapsh
---

# Random Riddles API
API version: 1.5

## Auth
ApiKey X-Fungenerators-Api-Secret in header

## Base URL
https://api.fungenerators.com

## Setup
1. Set your API key in the appropriate header
2. GET /riddle -- verify access
3. POST /riddle -- create first riddle

## Endpoints

6 endpoints across 1 groups. See references/api-spec.lap for full details.

### riddle
| Method | Path | Description |
|--------|------|-------------|
| GET | /riddle | Get a Riddle entry for a given id. Retrieves a riddle question and answer based on the id. |
| POST | /riddle | Create a random Riddle entry. Same as 'PUT' but can be used when some of the client libraries don't support 'PUT'. |
| PUT | /riddle | Create a random Riddle entry. |
| DELETE | /riddle | Create a random Riddle entry. |
| GET | /riddle/random | Get a random riddle for a given category(optional) |
| GET | /riddle/search | Search for random riddle which has the text in the query, for a given category(optional). |

## Enhanced Skill Content


## Question Mapping

- "Get me a random riddle" -> GET /riddle/random
- "Give me a random riddle about animals" -> GET /riddle/random?category=animals
- "Search for riddles about math" -> GET /riddle/search?query=math
- "Find riddles in the science category" -> GET /riddle/search?category=science
- "Search riddles matching 'what has legs'" -> GET /riddle/search?query=what+has+legs
- "Look up riddle by ID abc123" -> GET /riddle?id=abc123
- "Add a new riddle to the collection" -> POST /riddle
- "Submit a riddle with question, answer, and category" -> POST /riddle
- "Update an existing riddle's text" -> PUT /riddle
- "Change the category of a riddle" -> PUT /riddle
- "Delete riddle abc123" -> DELETE /riddle?id=abc123
- "Remove a riddle I created" -> DELETE /riddle
- "Browse riddles without any filter" -> GET /riddle
- "What categories of riddles are available?" -> GET /riddle/search (inspect returned category fields)
- "Create a riddle, then verify it was saved" -> POST /riddle, then GET /riddle?id={returned_id}

## Response Tips

- **GET /riddle, /riddle/random, /riddle/search**: Expect a wrapper object with a `contents` or `data` array; random endpoint returns a single riddle object. Check for empty results when filters match nothing.
- **POST /riddle**: Returns the created riddle with its assigned `id`. Capture this ID for subsequent updates or deletes.
- **PUT /riddle**: Returns the updated riddle object. Confirm changed fields match your request.
- **DELETE /riddle**: Returns a success confirmation. A subsequent GET with the same ID should 404 or return empty.
- **All endpoints**: 401 errors mean the `X-Fungenerators-Api-Secret` header is missing or invalid. No pagination parameters are documented, so large result sets may be truncated server-side.

## Anomaly Flags

- **401 on every call**: API key is missing or expired. Surface immediately and prompt the user to check `X-Fungenerators-Api-Secret`.
- **Empty search results**: If `/riddle/search` returns no matches, suggest broadening the query or trying `/riddle/random` as a fallback.
- **Missing ID on create**: If POST /riddle response lacks an `id` field, flag this as the riddle may not be retrievable or deletable.
- **Undocumented status codes**: Any 403, 429, or 5xx response should be surfaced. 429 likely indicates rate limiting not described in the spec.
- **PUT without ID context**: The PUT endpoint requires question/category/answer but the spec shows no `id` parameter. Flag if updates seem to create duplicates instead of modifying.
- **Category drift**: If a riddle's category changes unexpectedly between GET calls, surface as possible data integrity issue.

## Playbook

### 1. Get a Random Riddle for Fun

1. Call `GET /riddle/random` with no parameters for any category.
2. Optionally pass `?category=funny` to narrow the theme.
3. Display the `question` field to the user, wait, then reveal the `answer`.

### 2. Add a New Riddle to the Collection

1. Prepare `question`, `answer`, and `category` values.
2. Call `POST /riddle` with all three fields in the request body.
3. Capture the returned `id` from the response.
4. Verify with `GET /riddle?id={id}` to confirm it was stored correctly.

### 3. Search, Review, and Clean Up Riddles

1. Call `GET /riddle/search?query=your+topic` to find matching riddles.
2. Review each result's `id`, `question`, and `answer`.
3. For any unwanted riddle, call `DELETE /riddle?id={id}`.
4. Re-run the search to confirm deletions took effect.

### 4. Update an Existing Riddle

1. Retrieve the riddle with `GET /riddle?id={id}` to get current values.
2. Modify the desired fields (`question`, `category`, or `answer`).
3. Call `PUT /riddle` with all three required fields (include unchanged ones too).
4. Verify with `GET /riddle?id={id}` that updates persisted.

### 5. Explore Available Categories

1. Call `GET /riddle/search` with no parameters to get a broad result set.
2. Collect unique `category` values from all returned riddles.
3. Use a specific category with `GET /riddle/random?category={name}` to explore that theme.
4. If a category returns few results, try `GET /riddle/search?category={name}` to see the full set.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
