---
name: docspring-api
description: "DocSpring API skill. Use when working with DocSpring for authentication, combined_submissions, custom_files. Covers 40 endpoints."
version: 1.0.0
generator: lapsh
---

# DocSpring API
API version: v1

## Auth
basic

## Base URL
https://sync.api.docspring.com/api/v1

## Setup
1. Configure auth: basic
2. GET /authentication -- verify access
3. POST /combined_submissions -- create first combined_submissions

## Endpoints

40 endpoints across 10 groups. See references/api-spec.lap for full details.

### authentication
| Method | Path | Description |
|--------|------|-------------|
| GET | /authentication | Test authentication |

### combined_submissions
| Method | Path | Description |
|--------|------|-------------|
| GET | /combined_submissions | Get a list of all combined submissions |
| POST | /combined_submissions | Merge submission PDFs, template PDFs, or custom files |
| GET | /combined_submissions/{combined_submission_id} | Check the status of a combined submission (merged PDFs) |
| DELETE | /combined_submissions/{combined_submission_id} | Expire a combined submission |

### custom_files
| Method | Path | Description |
|--------|------|-------------|
| POST | /custom_files | Create a new custom file from a cached S3 upload |

### uploads
| Method | Path | Description |
|--------|------|-------------|
| GET | /uploads/presign | Get a presigned S3 URL for direct file upload |

### folders
| Method | Path | Description |
|--------|------|-------------|
| GET | /folders/ | Get a list of all folders |
| POST | /folders/ | Create a folder |
| POST | /folders/{folder_id}/move | Move a folder |
| POST | /folders/{folder_id}/rename | Rename a folder |
| DELETE | /folders/{folder_id} | Delete a folder |

### data_requests
| Method | Path | Description |
|--------|------|-------------|
| POST | /data_requests/{data_request_id}/events | Create a new event for emailing a signee a request for signature |
| POST | /data_requests/{data_request_id}/tokens | Create a new data request token for form authentication |
| GET | /data_requests/{data_request_id} | Look up a submission data request |
| PUT | /data_requests/{data_request_id} | Update a submission data request |

### submissions
| Method | Path | Description |
|--------|------|-------------|
| POST | /submissions/batches | Generate multiple PDFs |
| GET | /submissions/batches/{submission_batch_id} | Check the status of a submission batch job |
| GET | /submissions/{submission_id} | Check the status of a PDF |
| DELETE | /submissions/{submission_id} | Expire a PDF submission |
| POST | /submissions/{submission_id}/generate_preview | Generate a preview PDF for partially completed data requests |
| GET | /submissions | List all submissions |

### templates
| Method | Path | Description |
|--------|------|-------------|
| POST | /templates/{template_id}/submissions | Generate a PDF |
| GET | /templates/{template_id}/submissions | List all submissions for a given template |
| GET | /templates | Get a list of all templates |
| POST | /templates | Create a new PDF template with a form POST file upload |
| GET | /templates/{template_id} | Check the status of an uploaded template |
| PUT | /templates/{template_id} | Update a Template |
| DELETE | /templates/{template_id} | Delete a template |
| POST | /templates/{template_id}/publish_version | Publish a template version |
| POST | /templates/{template_id}/restore_version | Restore a template version |
| GET | /templates/{template_id}?full=true | Fetch the full attributes for a PDF template |
| PUT | /templates/{template_id}?endpoint_variant=update_template_pdf_with_form_post | Update a template's document with a form POST file upload |
| PUT | /templates/{template_id}?endpoint_variant=update_template_pdf_with_cached_upload | Update a template's document with a cached S3 file upload |
| PUT | /templates/{template_id}/add_fields | Add new fields to a Template |
| POST | /templates/{template_id}/move | Move Template to folder |
| POST | /templates/{template_id}/copy | Copy a template |
| GET | /templates/{template_id}/schema | Fetch the JSON schema for a template |

### templates?endpoint_variant=create_html_template
| Method | Path | Description |
|--------|------|-------------|
| POST | /templates?endpoint_variant=create_html_template | Create a new HTML template |

### templates?endpoint_variant=create_template_from_cached_upload
| Method | Path | Description |
|--------|------|-------------|
| POST | /templates?endpoint_variant=create_template_from_cached_upload | Create a new PDF template from a cached S3 file upload |

## Enhanced Skill Content
## Question Mapping

- "How do I verify my API credentials are working?" -> GET /authentication
- "Show me all my combined submissions" -> GET /combined_submissions
- "How do I merge multiple PDFs into one?" -> POST /combined_submissions
- "What's the status of my combined submission?" -> GET /combined_submissions/{combined_submission_id}
- "How do I upload a file to use as a template?" -> GET /uploads/presign
- "List all templates in a specific folder" -> GET /templates with parent_folder_id
- "How do I generate a PDF from a template?" -> POST /templates/{template_id}/submissions
- "Where is my submission? Is it done processing?" -> GET /submissions/{submission_id}
- "How do I submit data for multiple templates at once?" -> POST /submissions/batches
- "How do I create a template from raw HTML?" -> POST /templates?endpoint_variant=create_html_template
- "How do I roll back a template to a previous version?" -> POST /templates/{template_id}/restore_version
- "What fields does a template expect?" -> GET /templates/{template_id}/schema
- "How do I organize templates into folders?" -> POST /folders/ then POST /templates/{template_id}/move
- "How do I let an external user fill in a data request?" -> POST /data_requests/{data_request_id}/tokens
- "How do I get a preview of a submission without finalizing?" -> POST /submissions/{submission_id}/generate_preview

## Response Tips

- **Authentication:** 200 means credentials are valid; 401 on any endpoint means your basic auth header is missing or wrong.
- **Combined submissions:** Response includes processing status -- poll the GET endpoint until state indicates completion.
- **Submissions:** Both list endpoints (global and per-template) use cursor-based pagination via `cursor` and `limit` params; check for a next cursor in the response to know if more pages exist.
- **Combined submissions list:** Uses page-based pagination via `page` and `per_page` params instead of cursors.
- **Templates:** List response is paginated with `page`/`per_page`; the `?full=true` variant on GET returns expanded field definitions and document details.
- **Batch submissions:** Returns 201 when queued asynchronously, 200 when `wait=true` and processing completes synchronously -- check which you received.
- **Folders:** Responses are hierarchical; use `parent_folder_id` to traverse the tree.
- **Data requests:** Token creation (POST tokens) returns a short-lived URL or token for external users to submit data without API credentials.
- **Errors:** 422 consistently indicates validation failure with field-level detail in the response body; 403 means you lack permission on that specific resource.

## Anomaly Flags

- **401 on any endpoint:** Surface immediately -- credentials are invalid or expired. Do not retry; prompt the user to check their API key.
- **422 with field errors:** Parse and display the specific validation failures rather than the raw response -- these contain actionable fix instructions.
- **Submission stuck in processing:** If polling GET /submissions/{id} returns the same non-terminal state across multiple checks, flag that the submission may be stalled.
- **Combined submission partial failure:** When a combined submission completes but individual component submissions have errors, surface which ones failed.
- **Template version conflicts:** If PUT /templates/{id} or publish_version returns 422, flag that someone else may have modified the template concurrently.
- **Presign URL expiry:** The upload presign URL from GET /uploads/presign is time-limited. If a subsequent upload fails with 403, flag that the presign likely expired and a new one is needed.
- **Batch submission mixed results:** When POST /submissions/batches returns 200 (sync mode), check each submission's individual status in the response -- some may have succeeded while others failed.
- **Delete with version param:** Deleting a template with `version` param only removes that version, not the whole template. Flag this distinction when the user says "delete template."

## Playbook

### Generate a PDF from a Template

1. List available templates: `GET /templates` (optionally filter with `query` param)
2. Get the template schema to see required fields: `GET /templates/{template_id}/schema`
3. Submit data to generate the PDF: `POST /templates/{template_id}/submissions` with the `submission` map containing field values
4. If you need synchronous result, include `wait=true`; otherwise poll `GET /submissions/{submission_id}` until the state is terminal
5. Download the PDF from the URL in the completed submission response

### Create and Configure a Template from HTML

1. Create the HTML template: `POST /templates?endpoint_variant=create_html_template` with your HTML content in the `data` map
2. Add form fields to the template: `PUT /templates/{template_id}/add_fields` with field definitions
3. Optionally organize it: `POST /templates/{template_id}/move` to place it in a folder
4. Publish a version: `POST /templates/{template_id}/publish_version`
5. Verify the schema: `GET /templates/{template_id}/schema`

### Bulk Generate PDFs Across Templates

1. Prepare your batch payload mapping template IDs to their submission data
2. Submit the batch: `POST /submissions/batches` with the `data` map (add `wait=true` for synchronous processing)
3. If async, poll the batch status: `GET /submissions/batches/{submission_batch_id}` with `include_submissions=true`
4. Check each individual submission's status in the response for errors or completion
5. Collect download URLs from completed submissions

### Organize Templates into Folders

1. List existing folders: `GET /folders/` (use `parent_folder_id` to browse sub-folders)
2. Create a new folder if needed: `POST /folders/` with folder name in `data`
3. Move templates into the folder: `POST /templates/{template_id}/move` for each template
4. To reorganize later, rename with `POST /folders/{folder_id}/rename` or move with `POST /folders/{folder_id}/move`

### Collect Data from External Users via Data Requests

1. Create a submission with a data request (via template submission with appropriate options)
2. Generate an access token for the external user: `POST /data_requests/{data_request_id}/tokens`
3. Share the token/URL with the external user
4. Monitor progress: `GET /data_requests/{data_request_id}` to check if data has been submitted
5. Track events: `POST /data_requests/{data_request_id}/events` to log custom milestones or send reminders


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
