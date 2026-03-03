---
name: form-recognizer-client
description: "Form Recognizer Client API skill. Use when working with Form Recognizer Client for custom, prebuilt, layout. Covers 12 endpoints."
version: 1.0.0
generator: lapsh
---

# Form Recognizer Client
API version: 2.0-preview

## Auth
ApiKey Ocp-Apim-Subscription-Key in header

## Base URL
Not specified.

## Setup
1. Set your API key in the appropriate header
2. GET /custom/models/{modelId} -- verify access
3. POST /custom/models -- create first models

## Endpoints

12 endpoints across 3 groups. See references/api-spec.lap for full details.

### custom
| Method | Path | Description |
|--------|------|-------------|
| POST | /custom/models | Train Custom Model |
| GET | /custom/models/{modelId} | Get Custom Model |
| DELETE | /custom/models/{modelId} | Delete Custom Model |
| POST | /custom/models/{modelId}/analyze | Analyze Form |
| GET | /custom/models/{modelId}/analyzeResults/{resultId} | Get Analyze Form Result |
| POST | /custom/models/{modelId}/copy | Copy Custom Model |
| GET | /custom/models/{modelId}/copyResults/{resultId} | Get Custom Model Copy Result |
| POST | /custom/models/copyAuthorization | Generate Copy Authorization |

### prebuilt
| Method | Path | Description |
|--------|------|-------------|
| POST | /prebuilt/receipt/analyze | Analyze Receipt |
| GET | /prebuilt/receipt/analyzeResults/{resultId} | Get Analyze Receipt Result |

### layout
| Method | Path | Description |
|--------|------|-------------|
| POST | /layout/analyze | Analyze Layout |
| GET | /layout/analyzeResults/{resultId} | Get Analyze Layout Result |

## Enhanced Skill Content
## Question Mapping

- "How do I train a custom form recognition model?" -> POST /custom/models
- "What are the details of my custom model?" -> GET /custom/models/{modelId}
- "How do I delete a custom model I no longer need?" -> DELETE /custom/models/{modelId}
- "How do I analyze a document using my custom model?" -> POST /custom/models/{modelId}/analyze
- "What's the status of my custom model analysis?" -> GET /custom/models/{modelId}/analyzeResults/{resultId}
- "How do I copy a model to another resource?" -> POST /custom/models/{modelId}/copy
- "Did my model copy complete successfully?" -> GET /custom/models/{modelId}/copyResults/{resultId}
- "How do I authorize a target resource to receive a copied model?" -> POST /custom/models/copyAuthorization
- "How do I extract data from a receipt?" -> POST /prebuilt/receipt/analyze
- "What are the results of my receipt analysis?" -> GET /prebuilt/receipt/analyzeResults/{resultId}
- "How do I extract layout information (tables, text) from a document?" -> POST /layout/analyze
- "What are the results of my layout analysis?" -> GET /layout/analyzeResults/{resultId}
- "How do I train a model and then immediately analyze a document with it?" -> POST /custom/models then POST /custom/models/{modelId}/analyze
- "How do I move a model from a dev environment to production?" -> POST /custom/models/copyAuthorization then POST /custom/models/{modelId}/copy
- "Does my custom model include key-value pair extraction?" -> GET /custom/models/{modelId} with includeKeys

## Response Tips

- **Custom model training/copy auth (201):** Response body contains the new model ID or authorization payload; check `Location` header for the resource URI.
- **Async analysis & copy operations (202):** No result in the body -- poll the corresponding `GET .../Results/{resultId}` endpoint using the `Operation-Location` header value until status is `succeeded` or `failed`.
- **Model details (200):** Nested objects include model status, training document info, and optionally extracted keys; always check the `status` field before using the model.
- **Analysis results (200):** Results contain deeply nested `pageResults`, `documentResults`, and `readResults` arrays -- iterate pages first, then fields within each page.
- **Delete (204):** Empty response body; a 204 confirms successful deletion, any other code means the model was not removed.

## Anomaly Flags

- **Operation stuck in `running`:** If polling an analyzeResults or copyResults endpoint returns `running` for more than 60 seconds, surface a warning -- the operation may be stalled or the document may be unusually large.
- **Model status `invalid`:** When GET /custom/models/{modelId} returns a model with status `invalid`, proactively flag that the training data was insufficient or malformed.
- **Rate limit headers:** Surface `Retry-After` or `429 Too Many Requests` responses immediately -- the Cognitive Services tier may be throttling.
- **Partial success in analysis:** If analysis results contain `errors` array entries alongside `pageResults`, flag which pages failed so the user can resubmit or inspect those documents.
- **Deprecated API version:** This spec targets `2.0-preview` -- flag if the service returns a header indicating a newer stable version is available.
- **Copy authorization expiry:** Copy authorization tokens are time-limited; flag if a copy operation fails with 401/403 after authorization was obtained more than a few minutes prior.

## Playbook

### Train and Use a Custom Model

1. Prepare labeled training data and host it in an accessible Azure Blob container.
2. Call `POST /custom/models` with a `trainRequest` body pointing to your training data source.
3. Note the `modelId` from the 201 response.
4. Poll `GET /custom/models/{modelId}` until `status` is `ready`.
5. Submit a document via `POST /custom/models/{modelId}/analyze` with the file stream.
6. Extract the `resultId` from the `Operation-Location` header.
7. Poll `GET /custom/models/{modelId}/analyzeResults/{resultId}` until `status` is `succeeded`, then read the extracted fields.

### Extract Receipt Data (Prebuilt)

1. Call `POST /prebuilt/receipt/analyze` with the receipt image or PDF as the file stream.
2. Capture the `resultId` from the `Operation-Location` response header.
3. Poll `GET /prebuilt/receipt/analyzeResults/{resultId}` until `status` is `succeeded`.
4. Parse `documentResults` for merchant name, transaction date, totals, and line items.

### Extract Document Layout

1. Call `POST /layout/analyze` with the document file stream.
2. Capture the `resultId` from the `Operation-Location` header.
3. Poll `GET /layout/analyzeResults/{resultId}` until complete.
4. Read `readResults` for OCR text and bounding boxes, and `pageResults` for detected tables and their cell contents.

### Copy a Model Across Resources

1. On the **target** resource, call `POST /custom/models/copyAuthorization` to get an authorization payload.
2. On the **source** resource, call `POST /custom/models/{modelId}/copy` passing the authorization payload as `copyRequest`.
3. Capture the `resultId` from the `Operation-Location` header.
4. Poll `GET /custom/models/{modelId}/copyResults/{resultId}` on the source until `status` is `succeeded`.
5. Verify the model exists on the target by calling `GET /custom/models/{modelId}` against the target endpoint.

### Clean Up Unused Models

1. Identify the model to remove by listing or noting its `modelId`.
2. Optionally call `GET /custom/models/{modelId}` to confirm it is the correct model.
3. Call `DELETE /custom/models/{modelId}` and confirm a 204 response.
4. Verify deletion by calling `GET /custom/models/{modelId}` -- expect a 404.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
