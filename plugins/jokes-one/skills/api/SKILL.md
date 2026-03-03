---
name: jokes-one-api
description: "Jokes One API skill. Use when working with Jokes One for jod, joke. Covers 12 endpoints."
version: 1.0.0
generator: lapsh
---

# Jokes One API
API version: 1.1

## Auth
ApiKey X-JokesOne-Api-Secret in header

## Base URL
https://api.jokes.one

## Setup
1. Set your API key in the appropriate header
2. GET /jod -- verify access
3. POST /joke/tags/add -- create first add

## Endpoints

12 endpoints across 2 groups. See references/api-spec.lap for full details.

### jod
| Method | Path | Description |
|--------|------|-------------|
| GET | /jod | Gets `Joke of the Day`. |
| GET | /jod/categories | Gets a list of `Joke of the Day` Categories. |

### joke
| Method | Path | Description |
|--------|------|-------------|
| PUT | /joke | Add a new joke to your private collection. |
| PATCH | /joke | Update a joke |
| GET | /joke | Gets a `Joke` with a given `id`. |
| DELETE | /joke | Delete a joke. The user needs to be the owner of the joke to be able to delete it. |
| GET | /joke/random | Gets a `Random Joke`. When you are in a hurry this is what you call to get a random famous joke. |
| GET | /joke/search | Search for a `Joke` in Jokes One platform. Optional `category` , `author`, `minlength`, `maxlength` params determines the filters applied while searching for the joke. |
| GET | /joke/categories/search | Gets a list of `Joke` Categories, based on a query term. |
| GET | /joke/list | Get the list of jokes in your private collection. |
| POST | /joke/tags/add | Add a tag to a given Joke. |
| POST | /joke/tags/remove | Remove a tag from a given joke. |

## Enhanced Skill Content
## Question Mapping

- "Get me the joke of the day" -> GET /jod
- "What joke categories are available for joke of the day?" -> GET /jod/categories
- "Show me a joke of the day in the programming category" -> GET /jod?category=programming
- "Give me a random joke" -> GET /joke/random
- "Find jokes about dogs" -> GET /joke/search?query=dogs
- "Search for short jokes under 100 characters" -> GET /joke/search?maxlength=100
- "List all my jokes" -> GET /joke/list
- "Get a specific joke by ID" -> GET /joke?id={id}
- "Submit a new joke" -> PUT /joke
- "Update the text of one of my jokes" -> PATCH /joke
- "Delete a joke I submitted" -> DELETE /joke
- "Add tags to a joke" -> POST /joke/tags/add
- "Remove tags from a joke" -> POST /joke/tags/remove
- "Search for joke categories matching 'animal'" -> GET /joke/categories/search?query=animal
- "Find private jokes by a specific author" -> GET /joke/search?author={name}&private=true

## Response Tips

- **Joke of the Day (jod)**: Returns a single joke object; no auth required. Category is optional -- omit it for the default pick.
- **Joke CRUD (joke)**: All mutating endpoints return 401 if the `X-JokesOne-Api-Secret` header is missing or invalid. DELETE also returns 404 if the joke ID does not exist.
- **Search & List (joke/search, joke/list, joke/categories/search)**: Support `start` parameter for offset-based pagination. Check if fewer results than expected are returned to detect the last page.
- **Tags (joke/tags/add, joke/tags/remove)**: Return 404 when the joke ID is not found. Tags parameter likely accepts a comma-separated string.

## Anomaly Flags

- **401 on any joke endpoint**: API key is missing, expired, or incorrect. Surface immediately and prompt the user to verify `X-JokesOne-Api-Secret`.
- **404 on DELETE or tag operations**: The joke ID does not exist or was already deleted. Confirm the ID before retrying.
- **Empty search results**: If `/joke/search` returns zero results, suggest broadening the query, removing filters, or checking spelling.
- **Pagination exhaustion**: If `/joke/list` or `/joke/categories/search` returns fewer results than a typical page size, the user has reached the end. Note this proactively.
- **Missing optional fields on PUT**: If `author` or `tags` are omitted when creating a joke, flag that the joke will lack attribution and discoverability.

## Playbook

### 1. Browse and pick a joke of the day

1. Call `GET /jod/categories` to list available categories.
2. Pick a category from the results.
3. Call `GET /jod?category={chosen}` to get today's joke in that category.

### 2. Submit and tag a new joke

1. Call `PUT /joke` with `title`, `text`, and optionally `author`.
2. Note the returned joke `id`.
3. Call `POST /joke/tags/add` with the `id` and desired `tags`.
4. Call `GET /joke?id={id}` to verify the joke and its tags are saved correctly.

### 3. Search, filter, and curate jokes

1. Call `GET /joke/search?query={topic}` to find jokes on a topic.
2. Narrow results with `minlength`, `maxlength`, `category`, or `author` as needed.
3. For each joke worth keeping, call `POST /joke/tags/add` to tag it for later retrieval.
4. Use `GET /joke/search?category={tag}` to retrieve curated collections.

### 4. Edit or retire an existing joke

1. Call `GET /joke/list` to browse your jokes (paginate with `start` if needed).
2. Identify the joke `id` to modify.
3. Call `PATCH /joke` with the `id` and the fields to update (`title`, `text`, `author`, or `tags`).
4. To remove the joke entirely, call `DELETE /joke` with the `id`.
5. Confirm deletion by calling `GET /joke?id={id}` and expecting an error or empty response.

### 5. Explore joke categories

1. Call `GET /joke/categories/search?query={partial}` to find categories matching a keyword.
2. Paginate results using the `start` parameter if the list is long.
3. Use a discovered category in `GET /jod?category={name}` or `GET /joke/search?category={name}` to browse jokes within it.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
