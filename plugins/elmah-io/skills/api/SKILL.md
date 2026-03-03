---
name: elmahio-api
description: "elmah.io API skill. Use when working with elmah.io for deployments, heartbeats, installations. Covers 24 endpoints."
version: 1.0.0
generator: lapsh
---

# elmah.io API
API version: v3

## Auth
ApiKey api_key in query

## Base URL
Not specified.

## Setup
1. Set your API key in the appropriate header
2. GET /v3/deployments -- verify access
3. POST /v3/deployments -- create first deployments

## Endpoints

24 endpoints across 7 groups. See references/api-spec.lap for full details.

### deployments
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/deployments | Fetch a list of deployments. |
| POST | /v3/deployments | Create a new deployment. |
| GET | /v3/deployments/{id} | Fetch a deployment by its ID. |
| DELETE | /v3/deployments/{id} | Delete a deployment by its ID. |

### heartbeats
| Method | Path | Description |
|--------|------|-------------|
| POST | /v3/heartbeats/{logId}/{id} | Create a new heartbeat. |

### installations
| Method | Path | Description |
|--------|------|-------------|
| POST | /v3/installations/{logId} | Create a new installation. |

### logs
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/logs | Fetch a list of logs. |
| POST | /v3/logs | Create a new log. |
| GET | /v3/logs/{id} | Fetch a log by its ID. |
| DELETE | /v3/logs/{id} | Delete a log by its ID. |
| POST | /v3/logs/{id}/_disable | Disable a log by its ID. |
| POST | /v3/logs/{id}/_enable | Enable a log by its ID. |
| GET | /v3/logs/{id}/_diagnose | Help diagnose logging problems. |

### messages
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/messages/{logId} | Fetch messages from a log. |
| DELETE | /v3/messages/{logId} | Deletes a list of messages by logid and query. |
| POST | /v3/messages/{logId} | Create a new message. |
| GET | /v3/messages/{logId}/{id} | Fetch a message by its ID. |
| DELETE | /v3/messages/{logId}/{id} | Delete a message by its ID. |
| POST | /v3/messages/{logId}/_fix | Mark a list of messages as fixed by logid and query. |
| POST | /v3/messages/{logId}/{id}/_hide | Hide a message by its ID. |
| POST | /v3/messages/{logId}/{id}/_fix | Fix a message by its ID. |
| POST | /v3/messages/{logId}/_bulk | Create one or more new messages. |

### sourcemaps
| Method | Path | Description |
|--------|------|-------------|
| POST | /v3/sourcemaps/{logId} | Create or update a translation between a minified JavaScript path to the minified JavaScript and source map files. |

### uptimechecks
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/uptimechecks | Fetch a list of uptime checks. Currently in closed beta. Get in contact to get access to this endpoint. |

## Enhanced Skill Content
## Question Mapping

- "How do I list all my logs?" -> GET /v3/logs
- "How do I create a new log?" -> POST /v3/logs
- "How do I delete a log?" -> DELETE /v3/logs/{id}
- "How do I search for error messages in a specific log?" -> GET /v3/messages/{logId}
- "How do I get details of a specific message?" -> GET /v3/messages/{logId}/{id}
- "How do I mark a message as fixed?" -> POST /v3/messages/{logId}/{id}/_fix
- "How do I hide a message from the dashboard?" -> POST /v3/messages/{logId}/{id}/_hide
- "How do I bulk-create multiple messages at once?" -> POST /v3/messages/{logId}/_bulk
- "How do I record a deployment?" -> POST /v3/deployments
- "How do I list all deployments?" -> GET /v3/deployments
- "How do I send a heartbeat to confirm my service is alive?" -> POST /v3/heartbeats/{logId}/{id}
- "How do I disable a log temporarily without deleting it?" -> POST /v3/logs/{id}/_disable
- "How do I re-enable a disabled log?" -> POST /v3/logs/{id}/_enable
- "How do I diagnose issues with a log configuration?" -> GET /v3/logs/{id}/_diagnose
- "How do I upload a source map for JavaScript error deobfuscation?" -> POST /v3/sourcemaps/{logId}

## Response Tips

- **Logs & Messages**: Message listing (GET /v3/messages/{logId}) supports pagination via `pageIndex`, `pageSize`, and cursor-based `searchAfter` -- prefer `searchAfter` for deep pagination. A 200 on POST /v3/messages can mean update while 201 means created.
- **Deployments**: POST returns 201 on success; GET returns flat arrays -- no envelope object.
- **Heartbeats & Installations**: POST returns 200 with status confirmation; 404 means the logId or heartbeat id does not exist.
- **Errors**: 401 = missing or invalid API key, 402 = subscription/payment issue, 429 = rate limited, 409 (DELETE log only) = conflict due to active references.
- **Source Maps**: Requires multipart upload with `Path`, `SourceMap`, and `MinifiedJavaScript` fields; 413 is not listed but watch payload size on message creation (where it is).

## Anomaly Flags

- **429 Too Many Requests**: Surface immediately with retry guidance. All endpoints can return this -- back off exponentially.
- **402 Payment Required**: Indicates the subscription tier has been exceeded or expired. Flag to user as an account-level issue, not a code bug.
- **409 Conflict on log deletion**: The log has active dependencies. Surface the conflict and suggest disabling (POST /_disable) instead of deleting.
- **413 Payload Too Large on message creation**: The message body exceeds the allowed size. Flag the payload size and suggest using `_bulk` with smaller batches or trimming content.
- **404 on heartbeat or installation POST**: The referenced logId or id does not exist. Suggest verifying log existence with GET /v3/logs/{id} first.
- **Disabled log writes**: If a user posts messages to a log that was disabled, proactively suggest checking log status via GET /v3/logs/{id} or running /_diagnose.

## Playbook

### 1. Set Up Error Monitoring for a New App

1. Create a new log: POST /v3/logs with a descriptive name in the body
2. Note the returned log `id`
3. Configure your app to send errors: POST /v3/messages/{logId} with error details in the body
4. Upload source maps for JS apps: POST /v3/sourcemaps/{logId} with Path, SourceMap, and MinifiedJavaScript
5. Verify setup: GET /v3/logs/{id}/_diagnose to check configuration health

### 2. Investigate and Resolve an Error Spike

1. Search recent messages: GET /v3/messages/{logId}?query=severity:Error&from={timestamp}&to={timestamp}
2. Page through results using `searchAfter` from the previous response for deep result sets
3. Inspect a specific error: GET /v3/messages/{logId}/{id} with `includeHeaders=true` for full context
4. Mark resolved errors as fixed: POST /v3/messages/{logId}/{id}/_fix
5. Bulk-fix a class of errors: POST /v3/messages/{logId}/_fix with a query filter in the body

### 3. Track Deployments and Correlate with Errors

1. Record the deployment: POST /v3/deployments with version, description, and timestamp in the body
2. List all deployments: GET /v3/deployments to see the timeline
3. After deploying, query messages for the period: GET /v3/messages/{logId}?from={deployTime}
4. Compare error rates before and after by adjusting the `from`/`to` window
5. Clean up old deployment records: DELETE /v3/deployments/{id}

### 4. Set Up and Monitor Heartbeats

1. Identify the target log: GET /v3/logs to find or create the log
2. Send periodic heartbeats from your service: POST /v3/heartbeats/{logId}/{id} on a schedule (e.g., every 5 minutes)
3. Include health metadata in the request body (e.g., memory usage, queue depth)
4. If a heartbeat POST returns 404, verify the log still exists: GET /v3/logs/{id}
5. Check uptime status across all monitors: GET /v3/uptimechecks

### 5. Clean Up and Manage Logs

1. List all logs: GET /v3/logs
2. Disable inactive logs instead of deleting: POST /v3/logs/{id}/_disable
3. Purge messages from a log: DELETE /v3/messages/{logId} with optional query filter in body
4. Re-enable a log when needed: POST /v3/logs/{id}/_enable
5. Permanently remove a log only after disabling: DELETE /v3/logs/{id} (watch for 409 conflicts)


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
