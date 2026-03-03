---
name: trivia-api
description: "Trivia API skill. Use when working with Trivia for trivia. Covers 6 endpoints."
version: 1.0.0
generator: lapsh
---

# Trivia API
API version: 1.5

## Auth
ApiKey X-Fungenerators-Api-Secret in header

## Base URL
https://api.fungenerators.com/

## Setup
1. Set your API key in the appropriate header
2. GET /trivia -- verify access

## Endpoints

6 endpoints across 1 groups. See references/api-spec.lap for full details.

### trivia
| Method | Path | Description |
|--------|------|-------------|
| GET | /trivia | Get a Trivia entry for a given id. Retrieves a trivia question and answer based on the id. |
| PUT | /trivia | Create a random Trivia entry. |
| DELETE | /trivia | Create a random Trivia entry. |
| GET | /trivia/random | Get a random trivia for a given category(optional) |
| GET | /trivia/search | Search for random trivia which has the text in the query, for a given category(optional). |
| GET | /trivia/categories | Get a random Trivia. |

## Enhanced Skill Content
## Question Mapping

- "Get me a random trivia question" -> GET /trivia/random
- "Give me a random trivia question about science" -> GET /trivia/random?category=science
- "Search for trivia about space" -> GET /trivia/search?query=space
- "Find trivia questions in the history category" -> GET /trivia/search?category=history
- "What categories of trivia are available?" -> GET /trivia/categories
- "List more trivia categories starting from the 10th result" -> GET /trivia/categories?start=10
- "Look up a specific trivia question by ID" -> GET /trivia?id={id}
- "Add a new trivia question to the database" -> PUT /trivia
- "Delete a trivia question" -> DELETE /trivia?id={id}
- "Create a trivia question about geography" -> PUT /trivia (with category=geography)
- "Search trivia matching 'moon landing' in the science category" -> GET /trivia/search?query=moon+landing&category=science
- "Browse all trivia without filtering" -> GET /trivia
- "Remove the trivia entry I just created" -> DELETE /trivia?id={id} (requires the id from a prior PUT response)

## Response Tips

- **Single trivia (GET /trivia, GET /trivia/random):** Response contains a trivia object with question, answer, category, and id fields. Always extract the `id` if you plan to update or delete later.
- **Search results (GET /trivia/search):** Returns a list of matching trivia entries. Results may be empty for obscure queries -- suggest broadening the search term or trying a different category.
- **Categories (GET /trivia/categories):** Returns a paginated list. Use the `start` parameter to page through results incrementally. No explicit total count -- keep requesting until results come back empty.
- **Write operations (PUT, DELETE):** Expect a success/confirmation object on 200. A 401 means the API key is missing or invalid -- do not retry without fixing auth.

## Anomaly Flags

- **401 on any endpoint:** Surface immediately. The API key (`X-Fungenerators-Api-Secret` header) is missing, expired, or invalid. Prompt the user to verify their key before retrying.
- **Empty search results:** Flag when a search returns zero matches. Suggest alternative search terms or checking available categories first via GET /trivia/categories.
- **Missing id after creation:** If a PUT /trivia response does not include an `id`, warn the user that subsequent delete or lookup operations will not be possible for that entry.
- **Pagination exhaustion:** When GET /trivia/categories returns fewer results than expected or an empty list, notify the user that all categories have been listed.
- **Unexpected response structure:** If any endpoint returns a non-200 status not documented (e.g., 403, 429, 500), surface the raw status and body -- the API may have undocumented rate limits or maintenance windows.

## Playbook

### 1. Explore Available Trivia

1. Call GET /trivia/categories to see what topics exist
2. Pick an interesting category from the results
3. Call GET /trivia/random?category={chosen_category} to get a question
4. Present the question to the user, then reveal the answer on request

### 2. Search and Browse Trivia

1. Call GET /trivia/search?query={user_query} to find relevant questions
2. If results are too broad, narrow with GET /trivia/search?query={query}&category={category}
3. If no results, call GET /trivia/categories to suggest valid categories
4. Use GET /trivia?id={id} to fetch full details on any interesting result

### 3. Add a Custom Trivia Question

1. Call GET /trivia/categories to review existing categories for consistency
2. Call PUT /trivia with `question`, `answer`, and `category` fields
3. Save the returned `id` from the response
4. Verify the entry by calling GET /trivia?id={id}

### 4. Clean Up a Trivia Entry

1. Identify the target entry's `id` (from a prior search or creation)
2. Confirm with the user before proceeding -- deletion is not reversible
3. Call DELETE /trivia?id={id}
4. Verify removal by calling GET /trivia?id={id} and confirming it returns empty or an error

### 5. Run a Trivia Quiz Session

1. Call GET /trivia/categories and let the user pick a category
2. Call GET /trivia/random?category={category} to fetch a question
3. Present only the question; wait for the user's answer
4. Reveal the correct answer and compare
5. Repeat from step 2 for additional rounds, tracking score across turns


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
