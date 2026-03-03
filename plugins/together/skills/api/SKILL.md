---
name: together-apis
description: "Together APIs API skill. Use when working with Together APIs for deployments, voices, videos. Covers 91 endpoints."
version: 1.0.0
generator: lapsh
---

# Together APIs
API version: 2.0.0

## Auth
Bearer bearer

## Base URL
https://api.together.xyz/v1

## Setup
1. Set Authorization header with your Bearer token
2. GET /deployments -- verify access
3. POST /deployments -- create first deployments

## Endpoints

91 endpoints across 24 groups. See references/api-spec.lap for full details.

### deployments
| Method | Path | Description |
|--------|------|-------------|
| GET | /deployments | Get the list of deployments |
| POST | /deployments | Create a new deployment |
| DELETE | /deployments/{id} | Delete a deployment |
| GET | /deployments/{id} | Get a deployment by ID or name |
| PATCH | /deployments/{id} | Update a deployment |
| GET | /deployments/{id}/logs | Get logs for a deployment |
| GET | /deployments/secrets | Get the list of project secrets |
| POST | /deployments/secrets | Create a new secret |
| DELETE | /deployments/secrets/{id} | Delete a secret |
| GET | /deployments/secrets/{id} | Get a secret by ID or name |
| PATCH | /deployments/secrets/{id} | Update a secret |
| GET | /deployments/storage/{filename} | Download a file |
| GET | /deployments/storage/volumes | Get the list of project volumes |
| POST | /deployments/storage/volumes | Create a new volume |
| DELETE | /deployments/storage/volumes/{id} | Delete a volume |
| GET | /deployments/storage/volumes/{id} | Get a volume by ID or name |
| PATCH | /deployments/storage/volumes/{id} | Update a volume |

### voices
| Method | Path | Description |
|--------|------|-------------|
| GET | /voices | Fetch available voices for each model |

### videos
| Method | Path | Description |
|--------|------|-------------|
| GET | /videos/{id} | Fetch video metadata |
| POST | /videos | Create video |

### chat
| Method | Path | Description |
|--------|------|-------------|
| POST | /chat/completions | Create chat completion |

### completions
| Method | Path | Description |
|--------|------|-------------|
| POST | /completions | Create completion |

### embeddings
| Method | Path | Description |
|--------|------|-------------|
| POST | /embeddings | Create embedding |

### models
| Method | Path | Description |
|--------|------|-------------|
| GET | /models | List all models |
| POST | /models | Upload a custom model or adapter |

### jobs
| Method | Path | Description |
|--------|------|-------------|
| GET | /jobs/{jobId} | Get job status |
| GET | /jobs | List all jobs |

### images
| Method | Path | Description |
|--------|------|-------------|
| POST | /images/generations | Create image |

### files
| Method | Path | Description |
|--------|------|-------------|
| GET | /files | List all files |
| GET | /files/{id} | Retrieve file metadata |
| DELETE | /files/{id} | Delete a file |
| GET | /files/{id}/content | Get file contents |
| POST | /files/upload | Upload a file |

### fine-tunes
| Method | Path | Description |
|--------|------|-------------|
| POST | /fine-tunes | Create job |
| GET | /fine-tunes | List all jobs |
| POST | /fine-tunes/estimate-price | Estimate price |
| GET | /fine-tunes/{id} | List job |
| DELETE | /fine-tunes/{id} | Delete a fine-tune job |
| GET | /fine-tunes/{id}/events | List job events |
| GET | /fine-tunes/{id}/checkpoints | List checkpoints |
| POST | /fine-tunes/{id}/cancel | Cancel job |

### finetune
| Method | Path | Description |
|--------|------|-------------|
| GET | /finetune/download | Download model |

### rerank
| Method | Path | Description |
|--------|------|-------------|
| POST | /rerank | Create a rerank request |

### audio
| Method | Path | Description |
|--------|------|-------------|
| POST | /audio/speech | Create audio generation request |
| GET | /audio/speech/websocket | Real-time text-to-speech via WebSocket |
| POST | /audio/transcriptions | Create audio transcription request |
| POST | /audio/translations | Create audio translation request |

### compute
| Method | Path | Description |
|--------|------|-------------|
| GET | /compute/clusters | List all GPU clusters. |
| POST | /compute/clusters | Create GPU Cluster |
| GET | /compute/clusters/{cluster_id} | Get GPU cluster by cluster ID |
| PUT | /compute/clusters/{cluster_id} | Update a GPU Cluster. |
| DELETE | /compute/clusters/{cluster_id} | Delete GPU cluster by cluster ID |
| GET | /compute/regions | List regions and corresponding supported driver versions |
| GET | /compute/clusters/storage/volumes | List all shared volumes. |
| PUT | /compute/clusters/storage/volumes | Update a shared volume. |
| POST | /compute/clusters/storage/volumes | Create a shared volume. |
| GET | /compute/clusters/storage/volumes/{volume_id} | Get shared volume by volume Id. |
| DELETE | /compute/clusters/storage/volumes/{volume_id} | Delete shared volume by volume id. |

### clusters
| Method | Path | Description |
|--------|------|-------------|
| GET | /clusters/availability-zones | List all available availability zones. |

### endpoints
| Method | Path | Description |
|--------|------|-------------|
| GET | /endpoints | List all endpoints, can be filtered by type |
| POST | /endpoints | Create a dedicated endpoint, it will start automatically |
| GET | /endpoints/{endpointId} | Get endpoint by ID |
| PATCH | /endpoints/{endpointId} | Update endpoint, this can also be used to start or stop a dedicated endpoint |
| DELETE | /endpoints/{endpointId} | Delete endpoint |

### hardware
| Method | Path | Description |
|--------|------|-------------|
| GET | /hardware | List available hardware configurations |

### tci
| Method | Path | Description |
|--------|------|-------------|
| POST | /tci/execute | Executes the given code snippet and returns the output. Without a session_id, a new session will be created to run the code. If you do pass in a valid session_id, the code will be run in that session. This is useful for running multiple code snippets in the same environment, because dependencies and similar things are persisted |
| GET | /tci/sessions | Lists all your currently active sessions. |

### batches
| Method | Path | Description |
|--------|------|-------------|
| GET | /batches | List batch jobs |
| POST | /batches | Create a batch job |
| GET | /batches/{id} | Get a batch job |
| POST | /batches/{id}/cancel | Cancel a batch job |

### evaluation
| Method | Path | Description |
|--------|------|-------------|
| POST | /evaluation | Create an evaluation job |
| GET | /evaluation | Get all evaluation jobs |
| GET | /evaluation/model-list | Get model list |
| GET | /evaluation/{id} | Get evaluation job details |
| GET | /evaluation/{id}/status | Get evaluation job status and results |

### realtime
| Method | Path | Description |
|--------|------|-------------|
| GET | /realtime | Real-time audio transcription via WebSocket |

### queue
| Method | Path | Description |
|--------|------|-------------|
| POST | /queue/cancel | Cancel a queued job |
| GET | /queue/metrics | Get queue metrics |
| GET | /queue/status | Get job status |
| POST | /queue/submit | Submit a queued job |

### rl
| Method | Path | Description |
|--------|------|-------------|
| GET | /rl/training-sessions | List training sessions |
| POST | /rl/training-sessions | Create training session |
| GET | /rl/training-sessions/{session_id} | Get training session |
| GET | /rl/training-sessions/{session_id}/operations/forward-backward/{operation_id} | Get forward-backward operation |
| GET | /rl/training-sessions/{session_id}/operations/optim-step/{operation_id} | Get optim-step operation |
| GET | /rl/training-sessions/{session_id}/operations/sample/{operation_id} | Get sample operation |
| POST | /rl/training-sessions/{session_id}/operations/forward-backward | Forward-backward pass |
| POST | /rl/training-sessions/{session_id}/operations/optim-step | Optimizer step |
| POST | /rl/training-sessions/{session_id}/operations/sample | Sample |
| POST | /rl/training-sessions/{session_id}/stop | Stop training session |

## Enhanced Skill Content
## Question Mapping

- "What models are available on Together?" -> GET /models
- "Generate a chat response with GPT or Llama" -> POST /chat/completions
- "Create an image from a text prompt" -> POST /images/generations
- "How do I fine-tune a model on my dataset?" -> POST /fine-tunes
- "What's the status of my fine-tuning job?" -> GET /fine-tunes/{id}
- "How much will fine-tuning cost me?" -> POST /fine-tunes/estimate-price
- "Generate embeddings for my text" -> POST /embeddings
- "List all my deployed services" -> GET /deployments
- "How do I generate a video from a prompt?" -> POST /videos
- "What hardware options exist for a given model?" -> GET /hardware
- "Run a batch inference job on a file" -> POST /batches
- "Check the queue depth for a model" -> GET /queue/metrics
- "Convert text to speech" -> POST /audio/speech
- "Rerank search results by relevance" -> POST /rerank
- "Execute Python code in a sandbox" -> POST /tci/execute

## Response Tips

- **Chat/Completions**: `usage` may be null; always check `choices[].message` or `choices[].text` for output. Token counts live in `usage.prompt_tokens` and `usage.completion_tokens`.
- **Deployments**: `status` is an enum-like `any` field; compare against known states (e.g., "running", "pending"). `replica_events` is a map keyed by event type.
- **Fine-tunes**: `progress.seconds_remaining` is only meaningful when `progress.estimate_available` is true. `batch_size` can be the string `"max"` or an integer.
- **Files**: `Processed` (capital P) is a boolean indicating server-side processing is complete; poll before using the file in fine-tuning.
- **Batches**: `progress` is a float64 from 0.0 to 1.0; `output_file_id` and `error_file_id` are only populated after completion.
- **Images/Videos**: Async by default for video (poll GET /videos/{id}); images return inline. Video `outputs.video_url` is a temporary signed URL.
- **Queue**: `status` field on queue items indicates progression (queued -> running -> done/failed); `warnings` array may contain non-fatal issues.
- **RL Training**: Operation endpoints return `status` (pending/completed/failed); poll the GET variant with `operation_id` until status resolves.
- **Errors**: 429 means rate limited (back off), 503 means model is loading (retry after delay), 504 means generation timed out (reduce `max_tokens` or simplify prompt).

## Anomaly Flags

- **429 Too Many Requests**: Surface immediately with retry-after guidance. Appears on inference, embedding, rerank, audio, and batch endpoints.
- **503 Service Unavailable**: Model is cold-starting or overloaded. Flag to user with suggestion to retry in 30-60 seconds or check queue metrics.
- **504 Gateway Timeout**: Generation exceeded time limit. Recommend reducing `max_tokens`, prompt length, or switching to a smaller model.
- **Fine-tune `progress.estimate_available: false`**: Training time cannot be estimated yet. Surface so the user knows not to rely on `seconds_remaining`.
- **Batch job `error` field populated**: Even on 200 responses, the `error` string may be non-empty indicating partial failure. Always check.
- **Deployment `ready_replicas < desired_replicas`**: Deployment is degraded. Surface the replica gap and status field.
- **Queue `messages_waiting` spike**: If waiting messages significantly exceed running, the model is backlogged. Alert the user to expect latency.
- **File `Processed: false`**: File uploaded but not yet ready for use. Warn before attempting to reference it in fine-tuning or batch jobs.
- **Video `status: "failed"`**: Check `error.code` and `error.message` in the response. Common causes: invalid dimensions, unsupported model.
- **Evaluation `status` stuck**: If an evaluation workflow stays in a non-terminal status for an extended period, flag for user investigation.

## Playbook

### 1. Fine-tune a Model End-to-End

1. Upload your JSONL training file via `POST /files/upload`
2. Confirm the file is processed by polling `GET /files/{id}` until `Processed: true`
3. Estimate cost with `POST /fine-tunes/estimate-price` using the `training_file` id
4. If `allowed_to_proceed` is true, start fine-tuning with `POST /fine-tunes` specifying `training_file`, `model`, `n_epochs`, and optional `suffix`
5. Monitor progress via `GET /fine-tunes/{id}` checking `status` and `progress.seconds_remaining`
6. Review training events with `GET /fine-tunes/{id}/events` and checkpoints with `GET /fine-tunes/{id}/checkpoints`
7. Once complete, the fine-tuned model appears in `GET /models` and can be used in `POST /chat/completions`

### 2. Deploy a Custom Model as a Dedicated Endpoint

1. Check available hardware with `GET /hardware` filtered by your model
2. Create an endpoint via `POST /endpoints` with `model`, `hardware`, and `autoscaling` (min/max replicas)
3. Poll `GET /endpoints/{endpointId}` until `state` is "STARTED" and replicas are ready
4. Send inference requests to `POST /chat/completions` using the model name from your endpoint
5. When done, stop with `PATCH /endpoints/{endpointId}` setting `state: "STOPPED"`, or delete with `DELETE /endpoints/{endpointId}`

### 3. Run Batch Inference on a Large Dataset

1. Prepare a JSONL file with one request per line and upload via `POST /files/upload`
2. Confirm processing with `GET /files/{id}` (wait for `Processed: true`)
3. Submit the batch with `POST /batches` specifying `endpoint` (e.g., `/v1/chat/completions`), `input_file_id`, and optionally `model_id`
4. Monitor progress via `GET /batches/{id}` watching `progress` (0.0 to 1.0) and `status`
5. On completion, download results using `GET /files/{output_file_id}/content` and errors via `GET /files/{error_file_id}/content`

### 4. Generate and Iterate on Video Content

1. List available voices or reference assets if needed via `GET /voices`
2. Submit a video generation request with `POST /videos` specifying `model`, `prompt`, dimensions (`width`, `height`), and `seconds`
3. Poll `GET /videos/{id}` until `status` changes from "processing" to "completed" or "failed"
4. On success, retrieve the video from `outputs.video_url` (temporary signed URL, download promptly)
5. To iterate, adjust `prompt`, `negative_prompt`, `seed`, or `guidance_scale` and resubmit

### 5. RL Training Loop (GRPO/Custom Rewards)

1. Create a training session with `POST /rl/training-sessions` specifying `base_model` and optional `lora_config`
2. Sample completions from the model via `POST /rl/training-sessions/{session_id}/operations/sample` with your prompt
3. Poll `GET /rl/training-sessions/{session_id}/operations/sample/{operation_id}` until completed, then score the sequences externally
4. Submit scored samples for training via `POST /rl/training-sessions/{session_id}/operations/forward-backward` with loss configuration
5. Apply the gradient update with `POST /rl/training-sessions/{session_id}/operations/optim-step`
6. Repeat steps 2-5 for each training iteration, monitoring loss in the forward-backward response
7. When satisfied, stop the session with `POST /rl/training-sessions/{session_id}/stop` and use the checkpoint


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
