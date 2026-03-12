---
name: api-reference
description: "API Reference API skill. Use when working with API Reference for chat, generate, embed. Covers 40 endpoints."
version: 1.0.0
generator: lapsh
---

# API Reference
API version: 1.0

## Auth
Bearer bearer

## Base URL
https://api.cohere.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /v2/batches -- verify access
3. POST /v1/chat -- create first chat

## Endpoints

40 endpoints across 15 groups. See references/api-spec.lap for full details.

### chat
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/chat | Chat API (v1) |
| POST | /v2/chat | Chat API (v2) |

### generate
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/generate | Generate |

### embed
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/embed | Embed API (v1) |
| POST | /v2/embed | Embed API (v2) |

### batches
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/batches | List batches |
| POST | /v2/batches | Create a batch |
| GET | /v2/batches/{id} | Retrieve a batch |
| POST | /v2/batches/{id}:cancel | Cancel a batch |

### embed-jobs
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/embed-jobs | Create an Embed Job |
| GET | /v1/embed-jobs | List Embed Jobs |
| GET | /v1/embed-jobs/{id} | Fetch an Embed Job |
| POST | /v1/embed-jobs/{id}/cancel | Cancel an Embed Job |

### rerank
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/rerank | Rerank API (v1) |
| POST | /v2/rerank | Rerank API (v2) |

### classify
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/classify | Classify |

### datasets
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/datasets | Create a Dataset |
| GET | /v1/datasets | List Datasets |
| GET | /v1/datasets/usage | Get Dataset Usage |
| GET | /v1/datasets/{id} | Get a Dataset |
| DELETE | /v1/datasets/{id} | Delete a Dataset |

### summarize
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/summarize | Summarize |

### tokenize
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/tokenize | Tokenize |

### detokenize
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/detokenize | Detokenize |

### connectors
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/connectors | List Connectors |
| POST | /v1/connectors | Create a Connector |
| GET | /v1/connectors/{id} | Get a Connector |
| PATCH | /v1/connectors/{id} | Update a Connector |
| DELETE | /v1/connectors/{id} | Delete a Connector |
| POST | /v1/connectors/{id}/oauth/authorize | Authorize with oAuth |

### models
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/models/{model} | Get a Model |
| GET | /v1/models | List Models |

### check-api-key
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/check-api-key | Check API key |

### finetuning
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/finetuning/finetuned-models | Lists fine-tuned models. |
| POST | /v1/finetuning/finetuned-models | Trains and deploys a fine-tuned model. |
| PATCH | /v1/finetuning/finetuned-models/{id} | Updates a fine-tuned model. |
| GET | /v1/finetuning/finetuned-models/{id} | Returns a fine-tuned model by ID. |
| DELETE | /v1/finetuning/finetuned-models/{id} | Deletes a fine-tuned model. |
| GET | /v1/finetuning/finetuned-models/{finetuned_model_id}/events | Fetch history of statuses for a fine-tuned model. |
| GET | /v1/finetuning/finetuned-models/{finetuned_model_id}/training-step-metrics | Retrieve training metrics for fine-tuned models. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Create a chat?" -> POST /v1/chat
- "Create a chat?" -> POST /v2/chat
- "Create a generate?" -> POST /v1/generate
- "Create a embed?" -> POST /v1/embed
- "Create a embed?" -> POST /v2/embed
- "List all batches?" -> GET /v2/batches
- "Create a batche?" -> POST /v2/batches
- "Get batche details?" -> GET /v2/batches/{id}
- "Create a embed-job?" -> POST /v1/embed-jobs
- "List all embed-jobs?" -> GET /v1/embed-jobs
- "Get embed-job details?" -> GET /v1/embed-jobs/{id}
- "Create a cancel?" -> POST /v1/embed-jobs/{id}/cancel
- "Create a rerank?" -> POST /v1/rerank
- "Create a rerank?" -> POST /v2/rerank
- "Create a classify?" -> POST /v1/classify
- "Create a dataset?" -> POST /v1/datasets
- "List all datasets?" -> GET /v1/datasets
- "List all usage?" -> GET /v1/datasets/usage
- "Get dataset details?" -> GET /v1/datasets/{id}
- "Delete a dataset?" -> DELETE /v1/datasets/{id}
- "Create a summarize?" -> POST /v1/summarize
- "Create a tokenize?" -> POST /v1/tokenize
- "Create a detokenize?" -> POST /v1/detokenize
- "List all connectors?" -> GET /v1/connectors
- "Create a connector?" -> POST /v1/connectors
- "Get connector details?" -> GET /v1/connectors/{id}
- "Partially update a connector?" -> PATCH /v1/connectors/{id}
- "Delete a connector?" -> DELETE /v1/connectors/{id}
- "Create a authorize?" -> POST /v1/connectors/{id}/oauth/authorize
- "Get model details?" -> GET /v1/models/{model}
- "List all models?" -> GET /v1/models
- "Create a check-api-key?" -> POST /v1/check-api-key
- "List all finetuned-models?" -> GET /v1/finetuning/finetuned-models
- "Create a finetuned-model?" -> POST /v1/finetuning/finetuned-models
- "Partially update a finetuned-model?" -> PATCH /v1/finetuning/finetuned-models/{id}
- "Get finetuned-model details?" -> GET /v1/finetuning/finetuned-models/{id}
- "Delete a finetuned-model?" -> DELETE /v1/finetuning/finetuned-models/{id}
- "List all events?" -> GET /v1/finetuning/finetuned-models/{finetuned_model_id}/events
- "List all training-step-metrics?" -> GET /v1/finetuning/finetuned-models/{finetuned_model_id}/training-step-metrics
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
