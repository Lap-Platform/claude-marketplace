---
name: replicate-http-api
description: "Replicate HTTP API skill. Use when working with Replicate HTTP for account, collections, deployments. Covers 36 endpoints."
version: 1.0.0
generator: lapsh
---

# Replicate HTTP API
API version: 1.0.0-a1

## Auth
Bearer bearer

## Base URL
https://api.replicate.com/v1

## Setup
1. Set Authorization header with your Bearer token
2. GET /account -- verify access
3. POST /deployments -- create first deployments

## Endpoints

36 endpoints across 10 groups. See references/api-spec.lap for full details.

### account
| Method | Path | Description |
|--------|------|-------------|
| GET | /account | Get the authenticated account |

### collections
| Method | Path | Description |
|--------|------|-------------|
| GET | /collections | List collections of models |
| GET | /collections/{collection_slug} | Get a collection of models |

### deployments
| Method | Path | Description |
|--------|------|-------------|
| GET | /deployments | List deployments |
| POST | /deployments | Create a deployment |
| DELETE | /deployments/{deployment_owner}/{deployment_name} | Delete a deployment |
| GET | /deployments/{deployment_owner}/{deployment_name} | Get a deployment |
| PATCH | /deployments/{deployment_owner}/{deployment_name} | Update a deployment |
| POST | /deployments/{deployment_owner}/{deployment_name}/predictions | Create a prediction using a deployment |

### files
| Method | Path | Description |
|--------|------|-------------|
| GET | /files | List files |
| POST | /files | Create a file |
| DELETE | /files/{file_id} | Delete a file |
| GET | /files/{file_id} | Get a file |
| GET | /files/{file_id}/download | Download a file |

### hardware
| Method | Path | Description |
|--------|------|-------------|
| GET | /hardware | List available hardware for models |

### models
| Method | Path | Description |
|--------|------|-------------|
| GET | /models | List public models |
| POST | /models | Create a model |
| DELETE | /models/{model_owner}/{model_name} | Delete a model |
| GET | /models/{model_owner}/{model_name} | Get a model |
| PATCH | /models/{model_owner}/{model_name} | Update metadata for a model |
| GET | /models/{model_owner}/{model_name}/examples | List examples for a model |
| POST | /models/{model_owner}/{model_name}/predictions | Create a prediction using an official model |
| GET | /models/{model_owner}/{model_name}/readme | Get a model's README |
| GET | /models/{model_owner}/{model_name}/versions | List model versions |
| DELETE | /models/{model_owner}/{model_name}/versions/{version_id} | Delete a model version |
| GET | /models/{model_owner}/{model_name}/versions/{version_id} | Get a model version |
| POST | /models/{model_owner}/{model_name}/versions/{version_id}/trainings | Create a training |

### predictions
| Method | Path | Description |
|--------|------|-------------|
| GET | /predictions | List predictions |
| POST | /predictions | Create a prediction |
| GET | /predictions/{prediction_id} | Get a prediction |
| POST | /predictions/{prediction_id}/cancel | Cancel a prediction |

### search
| Method | Path | Description |
|--------|------|-------------|
| GET | /search | Search models, collections, and docs (beta) |

### trainings
| Method | Path | Description |
|--------|------|-------------|
| GET | /trainings | List trainings |
| GET | /trainings/{training_id} | Get a training |
| POST | /trainings/{training_id}/cancel | Cancel a training |

### webhooks
| Method | Path | Description |
|--------|------|-------------|
| GET | /webhooks/default/secret | Get the signing secret for the default webhook |

## Enhanced Skill Content
## Question Mapping

- "What account am I logged in as?" -> GET /account
- "Search for a model that does image generation" -> GET /search
- "List all my predictions" -> GET /predictions
- "What happened to prediction abc123?" -> GET /predictions/{prediction_id}
- "Run a prediction using model stability-ai/sdxl" -> POST /models/{model_owner}/{model_name}/predictions
- "Cancel a running prediction" -> POST /predictions/{prediction_id}/cancel
- "What hardware options are available?" -> GET /hardware
- "Create a new private model called my-model" -> POST /models
- "List all versions of a model" -> GET /models/{model_owner}/{model_name}/versions
- "Start a training job on a model version" -> POST /models/{model_owner}/{model_name}/versions/{version_id}/trainings
- "Upload a file to use as prediction input" -> POST /files
- "Create a new deployment with autoscaling" -> POST /deployments
- "Scale down my deployment to zero instances" -> PATCH /deployments/{deployment_owner}/{deployment_name}
- "Run a prediction on my deployment" -> POST /deployments/{deployment_owner}/{deployment_name}/predictions
- "Get my webhook signing secret" -> GET /webhooks/default/secret

## Response Tips

- **List endpoints** (models, predictions, deployments, files, collections, trainings, versions, examples): All return `{next, previous, results}` cursor pagination. Follow `next` URL until null to fetch all pages.
- **Predictions & trainings**: Poll `status` field (`starting` -> `processing` -> `succeeded`/`failed`/`canceled`). Use `urls.get` to re-fetch, `urls.cancel` to abort, `urls.stream` for SSE streaming. `output` is `any` type (varies per model -- could be a string URL, array of URLs, or structured object).
- **Async predictions** (201 vs 202): 201 means the prediction completed synchronously; 202 means it is still processing and requires polling. Use `Prefer: wait` header to request synchronous completion up to a timeout.
- **Deployments & models**: Nested `current_release.configuration` holds hardware/scaling config; `current_release.created_by` holds the user who triggered it.
- **Files**: `urls.get` contains the download URL. `expires_at` indicates when the file will be auto-deleted. 413 means the file is too large.
- **Search**: Returns three result arrays (`models`, `collections`, `pages`) -- check all three for comprehensive results.
- **DELETE endpoints**: Return 204 with no body on success.

## Anomaly Flags

- **Prediction errors**: Surface `error` field (nullable) whenever `status` is `failed` -- include the full error string, it often contains actionable model-specific messages.
- **Data removal**: Flag `data_removed: true` on predictions -- means input/output have been scrubbed and are no longer retrievable.
- **Deadline approaching**: If `deadline` is set on a prediction and current time is close, warn the user the prediction may be auto-canceled.
- **File expiration**: Surface `expires_at` on uploaded files -- alert if a file will expire within the next hour.
- **Model visibility**: Flag when a newly created model is `private` in case the user intended public access, or vice versa.
- **Empty pagination**: If `results` is empty on a list call, explicitly note "no results found" rather than silently returning nothing.
- **413 on file upload**: Proactively suggest checking file size limits before retrying.
- **Deprecated version deletion (202)**: Model version DELETE returns 202 (async) -- warn that deletion may not be immediate and dependent predictions could still be running.
- **Missing latest_version**: If `GET /models/{owner}/{name}` returns `latest_version: null`, flag that the model has no pushed versions and cannot run predictions.

## Playbook

### 1. Run a Prediction on a Public Model

1. `GET /search?query=stable diffusion` to find the model (note `owner` and `name` from results).
2. `GET /models/{owner}/{name}` to inspect the model, check `latest_version` for the current version ID and `default_example` for sample inputs.
3. `POST /predictions` with `version` (from latest_version.id) and `input` matching the model schema. Optionally set `stream: true` for SSE output.
4. Poll `GET /predictions/{id}` using the returned `urls.get` until `status` is `succeeded` or `failed`.
5. Read `output` from the final response (usually a URL or array of URLs for media models).

### 2. Create and Use a Deployment

1. `GET /hardware` to list available hardware SKUs (e.g., `gpu-a40-large`).
2. `GET /models/{owner}/{name}/versions` to pick the version ID you want to deploy.
3. `POST /deployments` with `name`, `model`, `version`, `hardware`, `min_instances`, and `max_instances`.
4. `POST /deployments/{owner}/{name}/predictions` with `input` to run predictions on the deployment.
5. `PATCH /deployments/{owner}/{name}` to scale instances or update the version later.

### 3. Fine-tune a Model (Training)

1. `GET /models/{owner}/{name}/versions` to find the trainable base model version.
2. Upload training data via `POST /files`, note the returned `id` and `urls.get`.
3. `POST /models/{owner}/{name}/versions/{version_id}/trainings` with `input` (including file reference), `destination` (e.g., `your-username/my-fine-tune`), and optionally a `webhook` URL.
4. Poll `GET /trainings/{training_id}` until `status` is `succeeded`. Check `output.weights` for the resulting weights URL and `output.version` for the new version ID.
5. Run predictions using the new version from `output.version`.

### 4. Manage Files for Large Inputs

1. `POST /files` to upload the file (image, audio, etc.). Note the `id`, `checksums.sha256`, and `expires_at`.
2. Use the `urls.get` URL as input to a prediction (e.g., `"image": "https://..."`).
3. `GET /files` to list all uploaded files and check expiration dates.
4. `DELETE /files/{file_id}` to clean up files you no longer need.

### 5. Monitor and Cancel Long-Running Work

1. `GET /predictions?created_after=2025-01-01T00:00:00Z` to list recent predictions, optionally filtering by date range.
2. For each prediction with `status` of `starting` or `processing`, decide whether to keep or cancel.
3. `POST /predictions/{id}/cancel` to abort unwanted predictions.
4. `GET /trainings` to review active training jobs similarly.
5. `POST /trainings/{id}/cancel` to abort unwanted training runs.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
