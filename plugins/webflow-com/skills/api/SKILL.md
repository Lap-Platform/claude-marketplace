---
name: lucidtech-api
description: "Lucidtech API skill. Use when working with Lucidtech for appClients, assets, datasets. Covers 133 endpoints."
version: 1.0.0
generator: lapsh
---

# Lucidtech API
API version: 2024-11-29T08:05:46Z

## Auth
OAuth2

## Base URL
https://api.lucidtech.ai/{basePath}

## Setup
1. Configure auth: OAuth2
2. GET /appClients -- verify access
3. POST /appClients -- create first appClients

## Endpoints

133 endpoints across 17 groups. See references/api-spec.lap for full details.

### appClients
| Method | Path | Description |
|--------|------|-------------|
| GET | /appClients |  |
| OPTIONS | /appClients |  |
| POST | /appClients |  |
| DELETE | /appClients/{appClientId} |  |
| GET | /appClients/{appClientId} |  |
| OPTIONS | /appClients/{appClientId} |  |
| PATCH | /appClients/{appClientId} |  |

### assets
| Method | Path | Description |
|--------|------|-------------|
| GET | /assets |  |
| OPTIONS | /assets |  |
| POST | /assets |  |
| DELETE | /assets/{assetId} |  |
| GET | /assets/{assetId} |  |
| OPTIONS | /assets/{assetId} |  |
| PATCH | /assets/{assetId} |  |

### datasets
| Method | Path | Description |
|--------|------|-------------|
| GET | /datasets |  |
| OPTIONS | /datasets |  |
| POST | /datasets |  |
| DELETE | /datasets/{datasetId} |  |
| GET | /datasets/{datasetId} |  |
| OPTIONS | /datasets/{datasetId} |  |
| PATCH | /datasets/{datasetId} |  |
| GET | /datasets/{datasetId}/transformations |  |
| OPTIONS | /datasets/{datasetId}/transformations |  |
| POST | /datasets/{datasetId}/transformations |  |
| DELETE | /datasets/{datasetId}/transformations/{transformationId} |  |
| OPTIONS | /datasets/{datasetId}/transformations/{transformationId} |  |

### deploymentEnvironments
| Method | Path | Description |
|--------|------|-------------|
| GET | /deploymentEnvironments |  |
| OPTIONS | /deploymentEnvironments |  |
| GET | /deploymentEnvironments/{deploymentEnvironmentId} |  |
| OPTIONS | /deploymentEnvironments/{deploymentEnvironmentId} |  |

### documents
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /documents |  |
| GET | /documents |  |
| OPTIONS | /documents |  |
| POST | /documents |  |
| DELETE | /documents/{documentId} |  |
| GET | /documents/{documentId} |  |
| OPTIONS | /documents/{documentId} |  |
| PATCH | /documents/{documentId} |  |

### logs
| Method | Path | Description |
|--------|------|-------------|
| GET | /logs |  |
| OPTIONS | /logs |  |
| GET | /logs/{logId} |  |
| OPTIONS | /logs/{logId} |  |

### models
| Method | Path | Description |
|--------|------|-------------|
| GET | /models |  |
| OPTIONS | /models |  |
| POST | /models |  |
| DELETE | /models/{modelId} |  |
| GET | /models/{modelId} |  |
| OPTIONS | /models/{modelId} |  |
| PATCH | /models/{modelId} |  |
| GET | /models/{modelId}/dataBundles |  |
| OPTIONS | /models/{modelId}/dataBundles |  |
| POST | /models/{modelId}/dataBundles |  |
| DELETE | /models/{modelId}/dataBundles/{dataBundleId} |  |
| GET | /models/{modelId}/dataBundles/{dataBundleId} |  |
| OPTIONS | /models/{modelId}/dataBundles/{dataBundleId} |  |
| PATCH | /models/{modelId}/dataBundles/{dataBundleId} |  |
| GET | /models/{modelId}/trainings |  |
| OPTIONS | /models/{modelId}/trainings |  |
| POST | /models/{modelId}/trainings |  |
| GET | /models/{modelId}/trainings/{trainingId} |  |
| OPTIONS | /models/{modelId}/trainings/{trainingId} |  |
| PATCH | /models/{modelId}/trainings/{trainingId} |  |

### organizations
| Method | Path | Description |
|--------|------|-------------|
| GET | /organizations |  |
| OPTIONS | /organizations |  |
| POST | /organizations |  |
| GET | /organizations/{organizationId} |  |
| OPTIONS | /organizations/{organizationId} |  |
| PATCH | /organizations/{organizationId} |  |

### paymentMethods
| Method | Path | Description |
|--------|------|-------------|
| GET | /paymentMethods |  |
| OPTIONS | /paymentMethods |  |
| POST | /paymentMethods |  |
| DELETE | /paymentMethods/{paymentMethodId} |  |
| GET | /paymentMethods/{paymentMethodId} |  |
| OPTIONS | /paymentMethods/{paymentMethodId} |  |
| PATCH | /paymentMethods/{paymentMethodId} |  |

### plans
| Method | Path | Description |
|--------|------|-------------|
| GET | /plans |  |
| OPTIONS | /plans |  |
| GET | /plans/{planId} |  |
| OPTIONS | /plans/{planId} |  |

### predictions
| Method | Path | Description |
|--------|------|-------------|
| GET | /predictions |  |
| OPTIONS | /predictions |  |
| POST | /predictions |  |
| GET | /predictions/{predictionId} |  |
| OPTIONS | /predictions/{predictionId} |  |

### profiles
| Method | Path | Description |
|--------|------|-------------|
| GET | /profiles/{profileId} |  |
| OPTIONS | /profiles/{profileId} |  |
| PATCH | /profiles/{profileId} |  |

### roles
| Method | Path | Description |
|--------|------|-------------|
| GET | /roles |  |
| OPTIONS | /roles |  |
| GET | /roles/{roleId} |  |
| OPTIONS | /roles/{roleId} |  |

### secrets
| Method | Path | Description |
|--------|------|-------------|
| GET | /secrets |  |
| OPTIONS | /secrets |  |
| POST | /secrets |  |
| DELETE | /secrets/{secretId} |  |
| OPTIONS | /secrets/{secretId} |  |
| PATCH | /secrets/{secretId} |  |

### transitions
| Method | Path | Description |
|--------|------|-------------|
| GET | /transitions |  |
| OPTIONS | /transitions |  |
| POST | /transitions |  |
| DELETE | /transitions/{transitionId} |  |
| GET | /transitions/{transitionId} |  |
| OPTIONS | /transitions/{transitionId} |  |
| PATCH | /transitions/{transitionId} |  |
| GET | /transitions/{transitionId}/executions |  |
| OPTIONS | /transitions/{transitionId}/executions |  |
| POST | /transitions/{transitionId}/executions |  |
| GET | /transitions/{transitionId}/executions/{executionId} |  |
| OPTIONS | /transitions/{transitionId}/executions/{executionId} |  |
| PATCH | /transitions/{transitionId}/executions/{executionId} |  |
| OPTIONS | /transitions/{transitionId}/executions/{executionId}/heartbeats |  |
| POST | /transitions/{transitionId}/executions/{executionId}/heartbeats |  |

### users
| Method | Path | Description |
|--------|------|-------------|
| GET | /users |  |
| OPTIONS | /users |  |
| POST | /users |  |
| DELETE | /users/{userId} |  |
| GET | /users/{userId} |  |
| OPTIONS | /users/{userId} |  |
| PATCH | /users/{userId} |  |

### workflows
| Method | Path | Description |
|--------|------|-------------|
| GET | /workflows |  |
| OPTIONS | /workflows |  |
| POST | /workflows |  |
| DELETE | /workflows/{workflowId} |  |
| GET | /workflows/{workflowId} |  |
| OPTIONS | /workflows/{workflowId} |  |
| PATCH | /workflows/{workflowId} |  |
| GET | /workflows/{workflowId}/executions |  |
| OPTIONS | /workflows/{workflowId}/executions |  |
| POST | /workflows/{workflowId}/executions |  |
| DELETE | /workflows/{workflowId}/executions/{executionId} |  |
| GET | /workflows/{workflowId}/executions/{executionId} |  |
| OPTIONS | /workflows/{workflowId}/executions/{executionId} |  |
| PATCH | /workflows/{workflowId}/executions/{executionId} |  |

## Enhanced Skill Content
## Question Mapping

- "How do I upload a document for processing?" -> POST /documents
- "How do I run a prediction on a document?" -> POST /predictions
- "What models are available in my organization?" -> GET /models
- "How do I check the status of a prediction?" -> GET /predictions/{predictionId}
- "How do I create a workflow and execute it?" -> POST /workflows, then POST /workflows/{workflowId}/executions
- "What is my organization's current usage and quota?" -> GET /organizations/{organizationId}
- "How do I train a model on my data?" -> POST /models/{modelId}/dataBundles, then POST /models/{modelId}/trainings
- "How do I check the logs for a failed workflow execution?" -> GET /logs with workflowId and workflowExecutionId filters
- "How do I add a user and assign them a role?" -> POST /users with email and roleIds
- "How do I set up a payment method for my organization?" -> POST /paymentMethods, then PATCH /organizations/{organizationId} with paymentMethodId
- "What transitions are configured and what type are they?" -> GET /transitions with optional transitionType filter
- "How do I update ground truth labels on a document?" -> PATCH /documents/{documentId} with groundTruth array
- "How do I create an app client for OAuth integration?" -> POST /appClients with callbackUrls and loginUrls
- "How do I check if a training job is still running?" -> GET /models/{modelId}/trainings/{trainingId} and inspect status field

## Response Tips

- **List endpoints** (GET /models, /documents, /workflows, etc.): All return a top-level array field (e.g., `models`, `documents`) plus an optional `nextToken` -- always check `nextToken` and paginate with it in subsequent requests using `maxResults` to control page size.
- **Resource detail endpoints** (GET by ID): Return flat objects with many optional (`?`) fields; missing fields mean unset, not errors -- do not treat null/absent values as failures.
- **Predictions**: The `predictions` field in POST /predictions response is typed as `any` -- its structure depends on the model's `fieldConfig`; also check `status` (may be async) and `nextPage` for multi-page documents.
- **Workflow executions**: Contain nested `transitionExecutions` map and `events` array -- drill into these for per-step status; `completedBy` is an array of `any` so inspect carefully.
- **Organization responses**: Extremely wide objects with dozens of `monthlyNumberOf*` quota/usage fields -- extract only what you need rather than displaying everything.
- **Error responses**: All endpoints share the same error code set (400, 403, 404, 415, 500) -- 415 indicates a missing or wrong `Content-Type` header, which is a required field on all POST/PATCH calls.

## Anomaly Flags

- **Quota nearing limits**: When `monthlyNumberOf*Created` approaches `monthlyNumberOf*Allowed` on organization responses (predictions, trainings, workflow executions, transitions, documents, transformations), warn the user before they hit hard limits.
- **Training stuck or failed**: If GET /models/{modelId}/trainings/{trainingId} shows a `status` other than a completed state for an extended period, surface it -- GPU hours are being consumed (`gpuHours` field).
- **Prediction errors**: If `error` field is non-null or `status` is not a success state on a prediction response, flag immediately -- the document may need reprocessing or the model may be misconfigured.
- **Missing Content-Type header**: All write operations require `Content-Type: str` as a required parameter -- omitting it will return 415 errors that can be confusing; proactively remind users.
- **Workflow in development vs production**: The `status` field on workflows accepts `development` or `production` -- flag if a workflow is being executed while still in `development` status, as behavior may differ.
- **App client secret exposure**: POST /appClients returns `clientSecret` in the response -- warn the user to store it securely since it may not be retrievable again (the object has `hasSecret` boolean but the secret itself is only in creation/delete responses).
- **Document retention expiry risk**: Documents and datasets have `retentionInDays` -- flag when documents are approaching their retention window to prevent data loss.

## Playbook

### 1. Process a Document with an Existing Model

1. Upload the document: `POST /documents` with `content` (base64), `contentType` (e.g., `application/pdf`), and optionally assign it to a `datasetId`.
2. Note the `documentId` from the response.
3. Run a prediction: `POST /predictions` with `documentId` and `modelId`. Set `async: true` for large documents.
4. If async, poll `GET /predictions/{predictionId}` until `status` indicates completion.
5. Read the `predictions` field for extracted field values. If `nextPage` is present, re-run with adjusted `preprocessConfig.startPage`.
6. Optionally update the document with corrected ground truth: `PATCH /documents/{documentId}` with `groundTruth` array for training feedback.

### 2. Train a Custom Model

1. Create a dataset: `POST /datasets` with a name and PII flag.
2. Upload labeled documents to the dataset: `POST /documents` with `datasetId`, `content`, and `groundTruth` array containing `label` and `value` pairs.
3. Create a model with field configuration: `POST /models` with `fieldConfig` defining expected extraction fields.
4. Create a data bundle linking the dataset: `POST /models/{modelId}/dataBundles` with `datasetIds` array.
5. Wait for data bundle status to be ready: poll `GET /models/{modelId}/dataBundles/{dataBundleId}`.
6. Start training: `POST /models/{modelId}/trainings` with `dataBundleIds` and desired `instanceType` (small-gpu, medium-gpu, or large-gpu).
7. Monitor training: poll `GET /models/{modelId}/trainings/{trainingId}` and check `status` and `evaluation` metrics.
8. Activate the trained model: `PATCH /models/{modelId}` with `trainingId` set to the completed training.

### 3. Build and Run a Document Processing Workflow

1. Define transitions for each processing step: `POST /transitions` with `transitionType` (docker, manual, or lambda) and configuration `parameters`.
2. Create secrets for any credentials needed: `POST /secrets` with `data` map containing key-value pairs.
3. Create the workflow: `POST /workflows` with a `specification` containing the `definition` (state machine connecting transitions), and optionally `errorConfig` for failure notifications.
4. Set workflow to production: `PATCH /workflows/{workflowId}` with `status: "production"`.
5. Execute the workflow: `POST /workflows/{workflowId}/executions` with the required `input` map.
6. Monitor execution: `GET /workflows/{workflowId}/executions/{executionId}` -- inspect `status`, `events`, and `transitionExecutions`.
7. Debug failures: `GET /logs` filtered by `workflowId` and `workflowExecutionId` to see detailed event logs.

### 4. Set Up Organization Billing and User Access

1. Create a payment method: `POST /paymentMethods` with a name/description.
2. Use the returned `stripeSetupIntentSecret` and `stripePublishableKey` to complete Stripe payment setup on the client side.
3. Attach payment to organization: `PATCH /organizations/{organizationId}` with `paymentMethodId`.
4. Select a plan: browse available plans with `GET /plans`, then `PATCH /organizations/{organizationId}` with `planId`.
5. Create users: `POST /users` with `email` and `roleIds` for access control.
6. Optionally create an app client for programmatic access: `POST /appClients` with callback URLs and role assignments.

### 5. Monitor and Debug Transition Executions

1. List all transitions: `GET /transitions` to find the target `transitionId`.
2. View executions: `GET /transitions/{transitionId}/executions` with optional `status` filter (e.g., filter for failed).
3. Inspect a specific execution: `GET /transitions/{transitionId}/executions/{executionId}` -- check `input`, `output`, and `status`.
4. For long-running executions, send heartbeats: `POST /transitions/{transitionId}/executions/{executionId}/heartbeats` to prevent timeout.
5. Complete or fail the execution: `PATCH /transitions/{transitionId}/executions/{executionId}` with `status` and either `output` (success) or `error` with a `message` (failure).
6. Review logs: `GET /logs` filtered by `transitionId` and `transitionExecutionId` for detailed event traces.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
