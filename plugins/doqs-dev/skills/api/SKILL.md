---
name: doqsdev-pdf-filling-api
description: "doqs.dev | PDF filling API skill. Use when working with doqs.dev | PDF filling for pdf-filling, pdf-generator. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# doqs.dev | PDF filling API
API version: 1.0

## Auth
ApiKey x-api-key in header

## Base URL
https://api.doqs.dev/v1

## Setup
1. Set your API key in the appropriate header
2. GET /pdf-filling/templates -- verify access
3. POST /pdf-filling/templates/{id}/fill -- create first fill

## Endpoints

4 endpoints across 2 groups. See references/api-spec.lap for full details.

### pdf-filling
| Method | Path | Description |
|--------|------|-------------|
| POST | /pdf-filling/templates/{id}/fill | Fill |
| GET | /pdf-filling/templates | List |

### pdf-generator
| Method | Path | Description |
|--------|------|-------------|
| POST | /pdf-generator/render | Render Pdf |
| GET | /pdf-generator/submissions | Get Submissions |

## Enhanced Skill Content
## Question Mapping

- "How do I fill a PDF template with data?" -> POST /pdf-filling/templates/{id}/fill
- "List all my PDF templates" -> GET /pdf-filling/templates
- "What templates do I have available?" -> GET /pdf-filling/templates
- "Generate a PDF from HTML" -> POST /pdf-generator/render
- "Convert HTML to PDF" -> POST /pdf-generator/render
- "Render a PDF in landscape orientation" -> POST /pdf-generator/render (set `pdf.orientation` to `landscape`)
- "Show my recent PDF render submissions" -> GET /pdf-generator/submissions
- "How do I paginate through templates?" -> GET /pdf-filling/templates (use `limit` and `offset`)
- "Fill a template and upload the result to my own storage" -> POST /pdf-generator/render (use `presigned_upload`)
- "How do I add a header and footer to a generated PDF?" -> POST /pdf-generator/render (use `header_template` and `footer_template`)
- "What paper sizes can I use for PDF generation?" -> POST /pdf-generator/render (set `pdf.format`, default is `a4`)
- "Scale down a rendered PDF to 75%?" -> POST /pdf-generator/render (set `pdf.scale` to `0.75`)
- "Check if a specific template exists before filling it" -> GET /pdf-filling/templates then POST /pdf-filling/templates/{id}/fill

## Response Tips

- **pdf-filling**: `/templates` returns `{ results: [map] }` -- iterate `results` for template objects. `/templates/{id}/fill` returns the filled PDF directly (200 with binary or URL).
- **pdf-generator**: `/render` returns the generated PDF on 200; watch for 408 (timeout on complex renders) and 426 (upgrade required, likely plan limits). `/submissions` returns `{ results: [map] }` -- paginate with `limit`/`offset`.
- **Pagination**: Both list endpoints default to `limit=100, offset=0`. Increment `offset` by `limit` to page through results. No cursor-based pagination.
- **Errors**: All endpoints return 4XX errors. Parse the response body for error details rather than relying solely on status codes.

## Anomaly Flags

- **408 on /pdf-generator/render**: Render timed out -- the HTML template may be too complex or contain external resources that are slow to load. Surface this immediately and suggest simplifying the template.
- **426 on /pdf-generator/render**: Upgrade required -- the user has hit a plan limitation. Alert them to check their doqs.dev subscription tier.
- **Empty results arrays**: If `/templates` or `/submissions` return empty `results`, confirm the API key has access to the expected workspace.
- **Repeated 4XX errors**: If multiple calls fail with 401/403, the `x-api-key` header is likely missing, expired, or scoped incorrectly. Surface the auth issue proactively.
- **Large offset values**: If a user is paginating beyond a few hundred results, suggest filtering or archiving to avoid performance degradation.

## Playbook

### 1. Fill a PDF Template with Dynamic Data

1. Call `GET /pdf-filling/templates` to list available templates and find the target template `id`.
2. Prepare a `data` map with key-value pairs matching the template's fill fields.
3. Call `POST /pdf-filling/templates/{id}/fill` with the `data` payload.
4. Handle the 200 response (filled PDF). On 4XX, check that the `id` is valid and `data` keys match expected field names.

### 2. Generate a Custom PDF from HTML

1. Prepare your HTML string in `template_html` (inline styles recommended for consistency).
2. Optionally set `header_template` and `footer_template` for repeating headers/footers.
3. Configure `pdf` options: `format` (e.g., `a4`, `letter`), `orientation` (`portrait`/`landscape`), `scale` (0.1-2.0).
4. Call `POST /pdf-generator/render` with the payload.
5. On 200, retrieve the generated PDF. On 408, simplify the template. On 426, check plan limits.

### 3. Generate and Upload a PDF to External Storage

1. Obtain a presigned upload URL from your storage provider (e.g., S3, GCS).
2. Call `POST /pdf-generator/render` with `template_html` and `presigned_upload` set to your upload URL/config.
3. The service renders the PDF and uploads it directly to your storage.
4. Verify the upload succeeded by checking your storage bucket.

### 4. Audit Recent PDF Generation Activity

1. Call `GET /pdf-generator/submissions?limit=100&offset=0` to retrieve the latest submissions.
2. Inspect each entry in `results` for status, timestamps, and render metadata.
3. Increment `offset` by 100 and repeat until `results` is empty to get the full history.
4. Cross-reference submission records with your application logs for troubleshooting.

### 5. Batch-Fill Multiple Templates

1. Call `GET /pdf-filling/templates` to retrieve all available templates.
2. For each template in `results`, extract the `id` and determine the appropriate `data` mapping.
3. Loop through your data source, calling `POST /pdf-filling/templates/{id}/fill` for each record.
4. Collect responses and handle any 4XX errors per-record rather than aborting the entire batch.
5. Log successes and failures for reconciliation.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
