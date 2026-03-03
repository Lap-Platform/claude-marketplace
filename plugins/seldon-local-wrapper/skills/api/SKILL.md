---
name: seldon-external-api
description: "Seldon External API skill. Use when working with Seldon External for aggregate, predict, route. Covers 12 endpoints."
version: 1.0.0
generator: lapsh
---

# Seldon External API
API version: 0.1

## Auth
No authentication required.

## Base URL
http://{host}:{port}

## Setup
1. No auth setup needed
2. GET /aggregate -- verify access
3. POST /aggregate -- create first aggregate

## Endpoints

12 endpoints across 6 groups. See references/api-spec.lap for full details.

### aggregate
| Method | Path | Description |
|--------|------|-------------|
| POST | /aggregate |  |
| GET | /aggregate |  |

### predict
| Method | Path | Description |
|--------|------|-------------|
| GET | /predict |  |
| POST | /predict |  |

### route
| Method | Path | Description |
|--------|------|-------------|
| GET | /route |  |
| POST | /route |  |

### send-feedback
| Method | Path | Description |
|--------|------|-------------|
| GET | /send-feedback |  |
| POST | /send-feedback |  |

### transform-input
| Method | Path | Description |
|--------|------|-------------|
| GET | /transform-input |  |
| POST | /transform-input |  |

### transform-output
| Method | Path | Description |
|--------|------|-------------|
| GET | /transform-output |  |
| POST | /transform-output |  |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Create a aggregate?" -> POST /aggregate
- "List all aggregate?" -> GET /aggregate
- "List all predict?" -> GET /predict
- "Create a predict?" -> POST /predict
- "List all route?" -> GET /route
- "Create a route?" -> POST /route
- "List all send-feedback?" -> GET /send-feedback
- "Create a send-feedback?" -> POST /send-feedback
- "List all transform-input?" -> GET /transform-input
- "Create a transform-input?" -> POST /transform-input
- "List all transform-output?" -> GET /transform-output
- "Create a transform-output?" -> POST /transform-output

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
