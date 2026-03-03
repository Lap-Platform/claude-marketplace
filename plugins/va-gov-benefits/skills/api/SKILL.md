---
name: benefits-intake
description: "Benefits Intake API skill. Use when working with Benefits Intake for uploads, path. Covers 6 endpoints."
version: 1.0.0
generator: lapsh
---

# Benefits Intake
API version: 1.0.0

## Auth
ApiKey apikey in header

## Base URL
https://sandbox-api.va.gov/services/vba_documents/{version}

## Setup
1. Set your API key in the appropriate header
2. GET /uploads/{id}/download -- verify access
3. POST /uploads -- create first uploads

## Endpoints

6 endpoints across 2 groups. See references/api-spec.lap for full details.

### uploads
| Method | Path | Description |
|--------|------|-------------|
| POST | /uploads | Get a location for subsequent document upload PUT request |
| GET | /uploads/{id} | Get status for a previous benefits document upload |
| GET | /uploads/{id}/download | Download zip of "what the server sees" |
| POST | /uploads/report | Get a bulk status report for a list of previous uploads |
| POST | /uploads/validate_document | Validate an individual document against system file requirements |

### path
| Method | Path | Description |
|--------|------|-------------|
| PUT | /path | Accepts document upload. |

## Enhanced Skill Content
## Question Mapping

- "How do I submit a new benefits document?" -> POST /uploads
- "How do I upload the actual file content?" -> PUT /path
- "What is the status of my submission?" -> GET /uploads/{id}
- "Can I check the status of multiple submissions at once?" -> POST /uploads/report
- "How do I download a previously uploaded document?" -> GET /uploads/{id}/download
- "Is my document valid before I submit it?" -> POST /uploads/validate_document
- "Why was my upload rejected?" -> GET /uploads/{id} (check status and error details in response data)
- "How do I submit a document with integrity verification?" -> PUT /path (use optional Content-MD5 header)
- "What happens after I create an upload?" -> POST /uploads returns a location/GUID, then PUT /path to send the file
- "How do I track a batch of submissions?" -> POST /uploads/report with array of UUIDs
- "Can I retry a failed upload?" -> POST /uploads to get a new submission, then PUT /path again
- "How do I confirm my file was received intact?" -> PUT /path with Content-MD5, then GET /uploads/{id} to verify status

## Response Tips

- **uploads (POST)**: Returns 202 Accepted, not 200 -- the upload is queued, not complete. Extract the GUID from `data` for all subsequent calls.
- **path (PUT)**: Returns 200 with no body on success. A 422 typically means the Content-MD5 did not match or the file was malformed.
- **uploads status (GET)**: The `data` object contains processing status -- poll this endpoint until the status reaches a terminal state.
- **uploads download (GET)**: Returns raw file content, not JSON. Handle the response as a binary stream.
- **uploads report (POST)**: Returns `data` as an array matching the input `ids` order. Missing or invalid UUIDs surface as 400/422.
- **validate_document (POST)**: Returns validation results in `data`. A 200 does not mean the document is valid -- check the response body for validation errors.

## Anomaly Flags

- **429 Too Many Requests**: Every endpoint can return 429. Surface rate limit headers (`X-RateLimit-Remaining`, `Retry-After`) proactively and back off before hitting the wall.
- **202 vs 200**: POST /uploads returns 202 (async processing). If an agent treats this as a failure or tries to immediately fetch results, flag the misunderstanding.
- **Stuck submissions**: If GET /uploads/{id} returns the same non-terminal status across multiple polls, flag the submission as potentially stuck and suggest contacting support.
- **MD5 mismatch on PUT**: A 422 on PUT /path when Content-MD5 was provided likely means file corruption in transit -- flag and recommend re-upload.
- **Bulk report gaps**: If POST /uploads/report returns fewer items in `data` than UUIDs sent in `ids`, flag the missing entries as potentially deleted or invalid.
- **Auth failures (401/403)**: Distinguish between missing API key (401) and insufficient permissions (403). Surface the difference clearly.

## Playbook

### 1. Submit a New Benefits Document

1. Call `POST /uploads` to create a new submission -- returns 202 with a GUID and a signed upload location.
2. Read the upload location from the response `data`.
3. Call `PUT /path` with the file content in the request body. Optionally include `Content-MD5` header for integrity verification.
4. Confirm 200 response on the PUT.
5. Call `GET /uploads/{id}` with the GUID to verify the submission entered processing.

### 2. Monitor Submission Status

1. After submitting, note the GUID from the POST /uploads response.
2. Call `GET /uploads/{id}` with the GUID.
3. Check the `data` object for the current processing status.
4. If status is non-terminal, wait and poll again (respect rate limits).
5. Once terminal, check for success or error details in the response.

### 3. Bulk Status Check

1. Collect all submission GUIDs you want to check.
2. Call `POST /uploads/report` with `{"ids": ["uuid-1", "uuid-2", ...]}`.
3. Parse the `data` array -- each entry corresponds to a submission.
4. Flag any entries with error states or missing results for follow-up.

### 4. Validate Before Submitting

1. Call `POST /uploads/validate_document` with the document payload.
2. Inspect the `data` object for validation errors or warnings.
3. If validation passes, proceed with the full submit flow (Playbook 1).
4. If validation fails, fix the document issues and re-validate before submitting.

### 5. Retrieve a Previously Uploaded Document

1. Obtain the submission GUID (from original upload or a report query).
2. Call `GET /uploads/{id}/download` with the GUID.
3. Handle the response as binary content (not JSON).
4. Verify file integrity if the original Content-MD5 is available.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
