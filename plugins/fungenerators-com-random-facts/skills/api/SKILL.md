---
name: facts-api
description: "Facts API skill. Use when working with Facts for fact. Covers 12 endpoints."
version: 1.0.0
generator: lapsh
---

# Facts API
API version: 1.5

## Auth
Bearer bearer

## Base URL
https://api.fungenerators.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /fact -- verify access

## Endpoints

12 endpoints across 1 groups. See references/api-spec.lap for full details.

### fact
| Method | Path | Description |
|--------|------|-------------|
| GET | /fact | Get a Fact belonging to the id. |
| PUT | /fact | Add a Fact entry to the database (private collection). |
| DELETE | /fact | Delete a Fact entry identified by the id. |
| GET | /fact/fod/categories | Get the list of supported fact of the day categories. |
| GET | /fact/fod | Get fact of the day for the given category. |
| GET | /fact/random | Get a random Fact for a given category(optional) and subcategory(optional). |
| GET | /fact/search | Search for random Fact which has the text in the query, for a given category(optional) and subcategory(optional). |
| GET | /fact/categories | Get a random Fact. |
| GET | /fact/numbers | Get a random fact about a number |
| GET | /fact/onthisday/born | Returns a random ( famous/ relatively famous ) person born on a given day and month |
| GET | /fact/onthisday/died | Returns a random ( famous/ relatively famous ) person died on a given day and month |
| GET | /fact/onthisday/event | Returns a random ( famous/ relatively famous ) historic event on a given day and month |

## Enhanced Skill Content
## Question Mapping

- "Give me a random fact" -> GET /fact/random
- "Get a random fact about science" -> GET /fact/random?category=science
- "What are the available fact categories?" -> GET /fact/categories
- "Search for facts about space" -> GET /fact/search?query=space
- "What is the fact of the day?" -> GET /fact/fod
- "What are the fact-of-the-day categories?" -> GET /fact/fod/categories
- "Look up a specific fact by ID" -> GET /fact?id={id}
- "Add a new fact to the database" -> PUT /fact
- "Delete a fact I created" -> DELETE /fact?id={id}
- "Tell me a number fact about 42" -> GET /fact/numbers?number=42
- "Who was born on this day?" -> GET /fact/onthisday/born
- "Who died on March 15?" -> GET /fact/onthisday/died?month=3&day=15
- "What historical events happened on July 4?" -> GET /fact/onthisday/event?month=7&day=4
- "Find facts in the history subcategory" -> GET /fact/search?category=history

## Response Tips

- **Single fact endpoints** (`/fact`, `/fact/random`, `/fact/fod`, `/fact/numbers`): Response contains a fact object with id, text, category, and tags -- extract `.fact` or `.contents` from the response body.
- **List endpoints** (`/fact/categories`, `/fact/fod/categories`): Return flat arrays; `/fact/categories` supports `start` for offset-based pagination -- increment `start` to page through results.
- **Search** (`/fact/search`): Results may be empty for narrow queries; broaden by dropping `subcategory` before dropping `category`.
- **On-this-day endpoints** (`/born`, `/died`, `/event`): Omitting `month` and `day` defaults to today's date; results are date-scoped lists.
- **Write operations** (`PUT`, `DELETE`): Return success/failure status; 401 means the Bearer token is missing or invalid.

## Anomaly Flags

- **401 on any request**: Surface immediately -- the Bearer token is expired, missing, or malformed. All 12 endpoints require auth.
- **Empty search results**: Flag when `/fact/search` returns zero hits so the user can broaden the query or try `/fact/random` with a category instead.
- **Unknown category used**: If a category passed to `/fact/random`, `/fact/search`, or `/fact/fod` yields an empty or error response, suggest calling `/fact/categories` to list valid options.
- **On-this-day with no results**: Some dates have sparse data; surface this and offer to try adjacent dates.
- **PUT missing required fields**: All four fields (fact, category, subcategory, tags) are mandatory -- flag before sending if any are absent.

## Playbook

### 1. Discover and browse facts by topic

1. Call `GET /fact/categories` to list all available categories
2. Pick a category of interest
3. Call `GET /fact/search?category={category}` to browse facts in that category
4. Optionally narrow with `subcategory` or `query` parameters

### 2. Get a daily fact for a specific topic

1. Call `GET /fact/fod/categories` to see which categories support fact-of-the-day
2. Call `GET /fact/fod?category={category}` to retrieve today's featured fact
3. If no category preference, call `GET /fact/fod` for the default pick

### 3. Add a new fact to the collection

1. Confirm the target category exists via `GET /fact/categories`
2. Call `PUT /fact` with all required fields: `fact`, `category`, `subcategory`, `tags`
3. Note the returned `id` for future reference or deletion
4. Verify by calling `GET /fact?id={id}`

### 4. Explore what happened on a specific date

1. Call `GET /fact/onthisday/event?month={m}&day={d}` for historical events
2. Call `GET /fact/onthisday/born?month={m}&day={d}` for notable births
3. Call `GET /fact/onthisday/died?month={m}&day={d}` for notable deaths
4. Omit `month` and `day` to default to today

### 5. Look up a number fact and clean up

1. Call `GET /fact/numbers?number={n}` to get a trivia fact about a specific number
2. If you previously added a custom fact and want to remove it, call `DELETE /fact?id={id}`
3. Confirm deletion by calling `GET /fact?id={id}` and verifying it no longer returns


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
