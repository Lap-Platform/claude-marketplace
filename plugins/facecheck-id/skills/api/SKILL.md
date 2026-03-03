---
name: facial-recognition-reverse-image-face-search-api
description: "Facial Recognition Reverse Image Face Search API skill. Use when working with Facial Recognition Reverse Image Face Search for api. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# Facial Recognition Reverse Image Face Search API
API version: v1.02

## Auth
ApiKey Authorization in header

## Base URL
Not specified.

## Setup
1. Set your API key in the appropriate header
3. POST /api/upload_pic -- create first upload_pic

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### api
| Method | Path | Description |
|--------|------|-------------|
| POST | /api/upload_pic |  |
| POST | /api/delete_pic | Remove an image from a search request |
| POST | /api/info | Returns remaining search credits, search engine online status, and number of indexed faces |
| POST | /api/search |  |

## Enhanced Skill Content
## Question Mapping

- "How do I search for a face in an image?" -> POST /api/upload_pic
- "How do I check the status of my face search?" -> POST /api/search (with `status_only: true`)
- "How do I get the results of a previous search?" -> POST /api/search (with `id_search`)
- "How many credits do I have left?" -> POST /api/info
- "Is the facial recognition service online?" -> POST /api/info
- "How do I delete a specific image from my search results?" -> POST /api/delete_pic
- "How do I run a demo search without using credits?" -> POST /api/search (with `demo: true`)
- "How do I track search progress in real time?" -> POST /api/search (with `with_progress: true`)
- "How many faces are in the database?" -> POST /api/info
- "Can I filter results to show only flagged/shady matches?" -> POST /api/search (with `shady_only: true`)
- "How do I remove an entire search session?" -> POST /api/delete_pic (with `id_search`)
- "What was the highest confidence score in my search?" -> POST /api/search (check `output.max_score`)
- "How do I solve a captcha challenge during search?" -> POST /api/search (with `id_captcha`)

## Response Tips

- **Upload/Search/Delete responses** all share the same envelope: check `error` and `code` first, then read `output.items` for match results and `output.max_score` for the best confidence value.
- **Progress tracking**: `progress` is an integer 0-100; poll with `status_only: true` until it reaches 100 before reading final `output`.
- **Info endpoint**: returns a flat object; `has_credits_to_search` is the quick boolean gate -- if false, stop before attempting a search.
- **Nested output object**: `output.items` is the array of matched faces; `output.searchedFaces` and `output.scaned_till_index` indicate how much of the database was covered.
- **Performance fields**: `tookSeconds`, `tookSecondsDownload`, `tookSecondsQueue` break down latency; `face_per_sec` and `performance` summarize throughput.

## Anomaly Flags

- **Credits exhausted**: Surface immediately when `has_credits_to_search` is `false` or `remaining_credits` drops below 5.
- **Service offline**: Alert when `is_online` returns `false` from `/api/info`.
- **Error codes**: Surface any non-null `error` or `code` field in responses -- these indicate server-side failures or validation issues.
- **Low confidence results**: Flag when `output.max_score` is below 50, indicating no strong matches were found.
- **Demo mode active**: Warn the user when `output.demo` is `true` since results may be limited or synthetic.
- **Incomplete scans**: Flag when `output.scaned_till_index` is significantly less than `output.searchedFaces`, suggesting the search was truncated.
- **Empty results with items flag**: Surface when `output.hasItems` is `false` or `hasEmptyImages` is `true` -- the search completed but found nothing.
- **Face monitoring status**: Surface `facemon_status` and `facemon_last_scann` when monitoring appears stale or in an unexpected state.

## Playbook

### 1. Upload an Image and Get Face Matches

1. Call `POST /api/info` to confirm `is_online` is `true` and `has_credits_to_search` is `true`.
2. Call `POST /api/upload_pic` with the image data. Capture `id_search` from the response.
3. Poll `POST /api/search` with `id_search` and `status_only: true` until `progress` reaches 100.
4. Call `POST /api/search` with `id_search` (without `status_only`) to retrieve full results from `output.items`.
5. Check `output.max_score` to gauge match confidence.

### 2. Monitor Search Progress in Real Time

1. After uploading via `POST /api/upload_pic`, save the returned `id_search`.
2. Call `POST /api/search` with `id_search` and `with_progress: true`.
3. Read the `progress` field (0-100) from each response.
4. Continue polling until `progress` is 100 and `output.hasItems` indicates results are ready.
5. Parse `output.items` for the final matched faces.

### 3. Clean Up Unwanted Results

1. Retrieve search results via `POST /api/search` with `id_search`.
2. Identify the unwanted image's `id_pic` from `output.items`.
3. Call `POST /api/delete_pic` with both `id_search` and `id_pic`.
4. Verify deletion by re-calling `POST /api/search` with the same `id_search` and confirming the item is removed.

### 4. Run a Demo Search Before Committing Credits

1. Call `POST /api/info` to check current `remaining_credits`.
2. Call `POST /api/search` with `demo: true` to run a test search without consuming credits.
3. Review `output.items` and `output.max_score` to evaluate result quality.
4. If satisfied, repeat the search without the `demo` flag to get full production results.

### 5. Filter for Flagged Matches Only

1. Upload an image via `POST /api/upload_pic` and capture `id_search`.
2. Wait for the search to complete (poll with `status_only: true`).
3. Call `POST /api/search` with `id_search` and `shady_only: true`.
4. Review the filtered `output.items` -- only flagged/suspicious matches are returned.
5. Use `output.images_in_bundle` and `output.scaned_till_index` to understand scan coverage.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
