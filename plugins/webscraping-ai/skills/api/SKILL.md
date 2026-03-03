---
name: webscrapingai
description: "WebScraping.AI API skill. Use when working with WebScraping.AI for ai, html, text. Covers 7 endpoints."
version: 1.0.0
generator: lapsh
---

# WebScraping.AI
API version: 3.2.0

## Auth
ApiKey api_key in query

## Base URL
https://api.webscraping.ai

## Setup
1. Set your API key in the appropriate header
2. GET /ai/question -- verify access

## Endpoints

7 endpoints across 6 groups. See references/api-spec.lap for full details.

### ai
| Method | Path | Description |
|--------|------|-------------|
| GET | /ai/question | Get an answer to a question about a given web page |
| GET | /ai/fields | Extract structured data fields from a web page |

### html
| Method | Path | Description |
|--------|------|-------------|
| GET | /html | Page HTML by URL |

### text
| Method | Path | Description |
|--------|------|-------------|
| GET | /text | Page text by URL |

### selected
| Method | Path | Description |
|--------|------|-------------|
| GET | /selected | HTML of a selected page area by URL and CSS selector |

### selected-multiple
| Method | Path | Description |
|--------|------|-------------|
| GET | /selected-multiple | HTML of multiple page areas by URL and CSS selectors |

### account
| Method | Path | Description |
|--------|------|-------------|
| GET | /account | Information about your account calls quota |

## Enhanced Skill Content
## Question Mapping

- "How do I scrape a webpage and get its HTML?" -> GET /html
- "What is the main topic of this webpage?" -> GET /ai/question
- "Extract the price and title from this product page" -> GET /ai/fields
- "Get the plain text content of a URL" -> GET /text
- "How many API calls do I have left?" -> GET /account
- "Select a specific element from a page using a CSS selector" -> GET /selected
- "Extract multiple CSS selectors from a page at once" -> GET /selected-multiple
- "Scrape a page as it appears on a mobile device" -> GET /html with device=mobile
- "Fetch a page through a residential proxy in Germany" -> GET /html with proxy=residential, country=de
- "Run custom JavaScript on a page before scraping it" -> GET /html with js_script
- "Get all links from a webpage" -> GET /text with return_links=True
- "Ask a question about a JavaScript-heavy SPA page" -> GET /ai/question with js=True, wait_for selector
- "Get structured JSON fields from multiple product pages" -> GET /ai/fields (loop per URL)
- "Scrape a page but fail if it redirects" -> GET /html with error_on_redirect=True

## Response Tips

- **AI endpoints** (`/ai/question`, `/ai/fields`): Return AI-generated answers; `/ai/question` returns plain text or JSON depending on `format`; `/ai/fields` returns a JSON object keyed by your requested field names.
- **Content endpoints** (`/html`, `/text`, `/selected`): Return raw page content; format varies by endpoint and `format`/`text_format` param; no pagination -- one page per request.
- **Selection endpoints** (`/selected`, `/selected-multiple`): `/selected` returns the first matching element; `/selected-multiple` returns a JSON object keyed by each selector string.
- **Account** (`/account`): Returns `remaining_api_calls`, `resets_at` (Unix timestamp), and `remaining_concurrency` -- use these to throttle your requests.
- **Errors**: 402 means quota exhausted; 429 means concurrency limit hit (back off and retry); 504 means the target page timed out (increase `timeout` or `js_timeout`).

## Anomaly Flags

- **Quota depletion**: Surface a warning when `remaining_api_calls` from `/account` drops below 10% of the typical cycle budget or hits zero (402 errors).
- **Concurrency ceiling**: Flag when `remaining_concurrency` is 0 -- subsequent requests will return 429 until a slot frees up.
- **Timeout failures**: Repeated 504 errors on the same URL suggest the target is slow or blocking; recommend increasing `timeout`/`js_timeout` or switching to `residential` proxy.
- **Unexpected redirects**: If a scrape silently follows redirects and returns unrelated content, suggest enabling `error_on_redirect=True` to catch this.
- **402 Payment Required**: Immediately halt batch operations and notify the user their plan quota is exhausted; continuing will waste retries.
- **Proxy/geo mismatch**: If results look region-gated or empty, flag that the `country` param may need changing or `residential` proxy may be required.

## Playbook

### 1. Extract Structured Data from a Product Page

1. Call `GET /account` to verify you have sufficient `remaining_api_calls`.
2. Call `GET /ai/fields` with the product URL and `fields` set to the data you need (e.g., `{"title": "product name", "price": "current price", "rating": "star rating"}`).
3. Parse the JSON response -- each key maps to the AI-extracted value.
4. If a field returns empty, retry with `GET /ai/question` asking specifically about that field for a more targeted answer.

### 2. Scrape a JavaScript-Heavy SPA

1. Call `GET /html` with `js=True` (default), and set `wait_for` to a CSS selector that appears only after the SPA renders (e.g., `wait_for=.product-list`).
2. If content is still missing, increase `js_timeout` (e.g., 5000) and optionally add a `js_script` to trigger interactions (scroll, click).
3. Validate the response contains expected elements by following up with `GET /selected` using a known selector.
4. If the site blocks datacenter IPs, switch to `proxy=residential`.

### 3. Batch-Scrape Text Content with Link Extraction

1. Call `GET /account` to check quota and concurrency limits.
2. For each URL, call `GET /text` with `return_links=True` and `text_format=json` to get structured text plus all hyperlinks.
3. Respect `remaining_concurrency` -- run that many requests in parallel, then wait for slots to free.
4. Collect the links from each response to build a crawl frontier for deeper scraping.
5. Periodically re-check `GET /account` to avoid hitting 402 mid-batch.

### 4. Geo-Targeted Scraping with Device Emulation

1. Determine the target country code (e.g., `de` for Germany) and device type (`mobile`, `desktop`, or `tablet`).
2. Call `GET /html` with `country=de`, `device=mobile`, and `proxy=residential` for the most authentic geo-targeted result.
3. Compare with a `device=desktop` request if you need to verify responsive layout differences.
4. If the site returns a CAPTCHA or block page, flag it and consider adjusting `headers` with a realistic `User-Agent`.

### 5. Ask AI Questions About a Page

1. Call `GET /ai/question` with the target `url` and your `question` in natural language (e.g., "What are the return policy terms?").
2. Set `format=json` if you need structured output, or `format=text` for a plain answer.
3. If the answer seems incomplete, check whether the page requires JavaScript rendering (`js=True` with adequate `js_timeout`).
4. For multi-field extraction from the same page, switch to `GET /ai/fields` to reduce API calls -- one request extracts all fields at once.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
