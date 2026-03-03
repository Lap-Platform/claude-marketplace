---
name: urlbox-api
description: "Urlbox API skill. Use when working with Urlbox for render. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Urlbox API
API version: v1

## Auth
Bearer bearer

## Base URL
https://api.urlbox.io

## Setup
1. Set Authorization header with your Bearer token
3. POST /v1/render/sync -- create first sync

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### render
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/render/sync | Render a URL as an image or video |

## Enhanced Skill Content
## Question Mapping

- "How do I take a screenshot of a website?" -> POST /v1/render/sync
- "Can I render a page as a PDF?" -> POST /v1/render/sync (set format to "pdf")
- "How do I capture a full-page screenshot?" -> POST /v1/render/sync (set full_page to true)
- "How do I screenshot just a specific element on the page?" -> POST /v1/render/sync (use selector param)
- "Can I render raw HTML instead of a URL?" -> POST /v1/render/sync (use html param instead of url)
- "How do I generate a thumbnail of a webpage?" -> POST /v1/render/sync (set thumb_width/thumb_height)
- "How do I block ads in my screenshot?" -> POST /v1/render/sync (set block_ads to true)
- "How do I wait for dynamic content before capturing?" -> POST /v1/render/sync (use wait_for or wait_until)
- "Can I record a video of a webpage?" -> POST /v1/render/sync (set format to "mp4" or "webm")
- "How do I get a retina/high-DPI screenshot?" -> POST /v1/render/sync (set retina to true)
- "How do I hide cookie consent banners?" -> POST /v1/render/sync (set hide_cookie_banners or click_accept to true)
- "Can I get metadata about the rendered page?" -> POST /v1/render/sync (set metadata to true)
- "How do I set a custom viewport size?" -> POST /v1/render/sync (set width and height)
- "How do I add a delay before capturing?" -> POST /v1/render/sync (use delay param)

## Response Tips

- **Successful renders (200):** Response contains `renderUrl` (a URI to the rendered asset) and `size` (file size in bytes as int64). Download the asset from `renderUrl` promptly as it may be temporary.
- **Redirects (307):** The render result is available at the redirected location. Follow the redirect to retrieve the asset directly.
- **Client errors (400):** Malformed request. Check that either `url` or `html` is provided (not both omitted), and that `format`, `wait_until`, and other enum values are valid.
- **Auth errors (401):** Bearer token is missing or invalid. Verify the Authorization header is set correctly.
- **Server errors (500):** Rendering failed upstream. Retry with exponential backoff. If persistent, simplify params (disable gpu, reduce dimensions) to isolate the issue.

## Anomaly Flags

- **Large file sizes:** Surface when `size` exceeds 10 MB, as this may indicate an unexpectedly large full-page capture or high-res retina render that could cause downstream issues.
- **307 redirects:** Flag if the client is not configured to follow redirects, as the actual asset lives at the redirect target.
- **Slow renders:** If using `wait_until: requestsfinished` with complex pages, warn the user that timeouts may occur. Suggest `mostrequestsfinished` as a faster alternative.
- **Missing url and html:** Both are optional per spec, but omitting both will produce a 400. Proactively validate before sending the request.
- **GPU mode usage:** Flag when `gpu: true` is set, as GPU rendering may have different availability or pricing implications.
- **Video format with full_page:** Warn if `format` is "mp4"/"webm" combined with `full_page: true`, as this is an unusual combination that may produce unexpected results.

## Playbook

### 1. Screenshot a Public Webpage

1. Send `POST /v1/render/sync` with `url` set to the target page and `format` set to "png".
2. Optionally set `width` and `height` for a custom viewport (defaults are typically 1280x1024).
3. Read `renderUrl` from the 200 response.
4. Download the image from `renderUrl`.

### 2. Generate a Clean PDF Without Ads or Banners

1. Send `POST /v1/render/sync` with `url`, `format: "pdf"`, `full_page: true`, `block_ads: true`, and `hide_cookie_banners: true`.
2. If the page has a cookie consent modal, also set `click_accept: true` to dismiss it.
3. Retrieve the PDF from `renderUrl` in the response.

### 3. Capture a Specific Element After Dynamic Load

1. Identify the CSS selector for the target element (e.g., `#chart-container`).
2. Send `POST /v1/render/sync` with `url`, `selector: "#chart-container"`, and `wait_for: "#chart-container"` to ensure the element exists before capture.
3. Optionally set `wait_until: "requestsfinished"` to wait for all network activity to settle.
4. Download the cropped screenshot from `renderUrl`.

### 4. Create a Thumbnail Gallery

1. For each target URL, send `POST /v1/render/sync` with `url`, `thumb_width` (e.g., 320), and `thumb_height` (e.g., 240).
2. Set `block_ads: true` and `hide_cookie_banners: true` for cleaner thumbnails.
3. Collect each `renderUrl` and `size` from the responses.
4. Use the render URLs to populate the gallery. Check `size` values to flag any unexpectedly large thumbnails.

### 5. Render Raw HTML to an Image

1. Prepare the HTML string you want to render.
2. Send `POST /v1/render/sync` with `html` set to the HTML content (omit `url`).
3. Set `format` to the desired output ("png", "jpg", "webp", etc.) and `width`/`height` for dimensions.
4. Retrieve the rendered image from `renderUrl` in the response.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
