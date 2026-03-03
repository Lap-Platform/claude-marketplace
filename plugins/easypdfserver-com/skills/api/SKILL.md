---
name: easypdfserver
description: "EasyPDFServer API skill. Use when working with EasyPDFServer for make-pdf. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# EasyPDFServer
API version: 1.0

## Auth
Requires API key (key parameter)

## Base URL
https://api.easypdfserver.com

## Setup
1. Include your API key via the key parameter
3. POST /make-pdf -- create first make-pdf

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### make-pdf
| Method | Path | Description |
|--------|------|-------------|
| POST | /make-pdf | Generate a PDF from HTML or URL. |

## Enhanced Skill Content
## Question Mapping

- "How do I convert HTML to PDF?" -> POST /make-pdf
- "Can I generate a PDF from a webpage URL?" -> POST /make-pdf
- "What authentication does the PDF API need?" -> POST /make-pdf (requires `key` parameter)
- "How do I pass raw HTML for PDF generation?" -> POST /make-pdf with `html` param
- "Can I convert a live website to PDF?" -> POST /make-pdf with `url` param
- "What happens if I send both html and url?" -> POST /make-pdf (check which takes priority)
- "How do I test my API key is valid?" -> POST /make-pdf with minimal html payload
- "What format does the response come back in?" -> POST /make-pdf returns binary PDF on 200
- "Can I batch convert multiple pages to PDF?" -> POST /make-pdf (call once per document)
- "Why is my PDF generation failing silently?" -> POST /make-pdf (check key validity and that either html or url is provided)
- "How do I render a dynamic report as PDF?" -> POST /make-pdf with `html` containing rendered template
- "What's the base URL for the API?" -> All endpoints use https://api.easypdfserver.com

## Response Tips

- **POST /make-pdf (200)**: Response is likely binary PDF data. Set `Accept` headers accordingly and handle the response as a blob/stream, not JSON. Non-200 responses indicate auth failure (invalid key), bad input (missing both html and url), or upstream rendering errors.

## Anomaly Flags

- **Missing required field**: Surface immediately if `key` is omitted -- the request will fail auth.
- **Empty input**: Flag if neither `html` nor `url` is provided -- at least one is needed for PDF generation.
- **Large HTML payloads**: Warn if HTML content exceeds reasonable size thresholds, as request may timeout or be rejected.
- **Non-200 responses**: Surface any error status codes with full response body -- this single-endpoint API has no retry/pagination complexity, so errors need direct attention.
- **Unreachable URLs**: If using `url` param, flag connection failures or non-HTML content types at the target URL.

## Playbook

### 1. Generate a PDF from raw HTML

1. Prepare your HTML string (full document or fragment).
2. Send `POST /make-pdf` with `key` and `html` parameters.
3. Check for 200 status.
4. Save the response body as a `.pdf` file.

### 2. Convert a live webpage to PDF

1. Confirm the target URL is publicly accessible.
2. Send `POST /make-pdf` with `key` and `url` set to the target page.
3. Check for 200 status.
4. Save the response body as a `.pdf` file.

### 3. Validate your API key

1. Send `POST /make-pdf` with `key` and a minimal `html` value (e.g., `<p>test</p>`).
2. A 200 response confirms the key is valid.
3. Any auth error response means the key is invalid or expired.

### 4. Generate PDFs from templated reports

1. Render your report template to an HTML string (server-side or client-side).
2. Inject dynamic data (tables, charts as inline SVG, styles as inline CSS).
3. Send `POST /make-pdf` with `key` and the full `html` string.
4. Check for 200 and save the resulting PDF.
5. Repeat per report instance -- each call produces one PDF.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
