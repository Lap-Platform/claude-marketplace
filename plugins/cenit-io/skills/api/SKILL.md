---
name: cenit-io-rest-api-specification
description: "Cenit IO - REST API Specification API skill. Use when working with Cenit IO - REST API Specification for setup. Covers 40 endpoints."
version: 1.0.0
generator: lapsh
---

# Cenit IO - REST API Specification
API version: v1

## Auth
ApiKey X-User-Access-Key in header | ApiKey X-User-Access-Token in header

## Base URL
https://cenit.io/api/v1

## Setup
1. Set your API key in the appropriate header
2. GET /setup/connection -- verify access
3. POST /setup/connection -- create first connection

## Endpoints

40 endpoints across 1 groups. See references/api-spec.lap for full details.

### setup
| Method | Path | Description |
|--------|------|-------------|
| GET | /setup/connection/{id} | Retrieve an existing connection |
| DELETE | /setup/connection/{id} | Delete a connection |
| GET | /setup/connection | Returns a list of connections |
| POST | /setup/connection | Create or update a connection |
| GET | /setup/connection_role/{id} | Return a connection role |
| DELETE | /setup/connection_role/{id} | Delete a connection role. |
| GET | /setup/connection_role | Returns a list of connection roles |
| POST | /setup/connection_role | Create or update a connection role |
| GET | /setup/data_type/ | Returns a list of data types |
| POST | /setup/data_type/ | Create or update a data type |
| GET | /setup/data_type/{id} | Retrieve a data type |
| DELETE | /setup/data_type/{id} | Delete a data type |
| GET | /setup/observer/ | Returns a list of events |
| POST | /setup/observer/ | Create or update an event |
| GET | /setup/observer/{id} | Retrieve an existing event |
| DELETE | /setup/observer/{id} | Delete an event |
| GET | /setup/scheduler/ | Returns a list of schedulers |
| POST | /setup/scheduler/ | Create or update an scheduler |
| GET | /setup/scheduler/{id} | Retrieve an existing schedule |
| DELETE | /setup/scheduler/{id} | Delete an schedule |
| GET | /setup/flow/ | Returns a list of flows |
| POST | /setup/flow/ | Create or update a flow |
| GET | /setup/flow/{id} | Retrieve an existing flow |
| DELETE | /setup/flow/{id} | Delete a flow. |
| GET | /setup/schema/ | Returns a list of schemas |
| POST | /setup/schema/ | Create or update an schema |
| GET | /setup/schema/{id} | Retrieve an existing schema |
| DELETE | /setup/schema/{id} | Delete an schema. |
| GET | /setup/translator/ | Returns a list of translators |
| POST | /setup/translator/ | Create or update a translator |
| GET | /setup/translator/{id} | Retrieve an existing translator |
| DELETE | /setup/translator/{id} | Delete a translator |
| GET | /setup/webhook/ | Returns a list of webhooks |
| POST | /setup/webhook/ | Create or update a webhook |
| GET | /setup/webhook/{id} | Retrieve an existing webhook |
| DELETE | /setup/webhook/{id} | Delete a webhook |
| GET | /setup/namespace/ | Returns a list of namespaces |
| POST | /setup/namespace/ | Create or update a namespace |
| GET | /setup/namespace/{id} | Retrieve an existing namespace |
| DELETE | /setup/namespace/{id} | Delete a namespace |

## Enhanced Skill Content
## Question Mapping

- "How do I list all connections?" -> GET /setup/connection
- "Show me the details of a specific flow" -> GET /setup/flow/{id}
- "How do I create a new webhook?" -> POST /setup/webhook
- "Delete a data type by ID" -> DELETE /setup/data_type/{id}
- "What schedulers are configured?" -> GET /setup/scheduler/
- "How do I set up a new connection role?" -> POST /setup/connection_role
- "Which translators exist in my account?" -> GET /setup/translator/
- "How do I remove an observer?" -> DELETE /setup/observer/{id}
- "Create a new namespace for organizing resources" -> POST /setup/namespace/
- "Get the schema definition for a specific ID" -> GET /setup/schema/{id}
- "What namespaces are available?" -> GET /setup/namespace/
- "How do I wire a connection to a webhook?" -> POST /setup/flow (flows bind connections, webhooks, and translators together)
- "How do I register a new data type?" -> POST /setup/data_type/
- "Remove a connection I no longer need" -> DELETE /setup/connection/{id}
- "What observers are watching for data changes?" -> GET /setup/observer/

## Response Tips

- **All list endpoints** (GET without ID): Return arrays of resource objects. Expect pagination parameters in the response; check for `total_pages` or similar fields and iterate if results are truncated.
- **All detail endpoints** (GET with ID): Return a single resource object. A 404 means the ID does not exist -- verify the ID value before retrying.
- **All create endpoints** (POST): Send JSON body with resource properties. The response includes the created object with its assigned `id` field.
- **All delete endpoints** (DELETE with ID): Return 200 on success with no meaningful body. A 404 means the resource was already removed or never existed.
- **Auth errors**: Missing or invalid `X-User-Access-Key` / `X-User-Access-Token` headers will return 401 or 403 before reaching business logic.

## Anomaly Flags

- **404 on DELETE**: Surface when a delete returns 404 -- the resource may have been removed by another process or the ID is stale.
- **Auth header mismatch**: Both `X-User-Access-Key` and `X-User-Access-Token` are required simultaneously. Flag if only one is provided -- the request will fail silently or with an unclear error.
- **Orphaned resources**: After deleting a connection or webhook, flag that flows referencing them may break. Suggest listing flows to check for dangling references.
- **Empty list responses**: If a list endpoint returns zero results for a resource type the user expects to exist (e.g., translators, schemas), surface this as a potential configuration issue.
- **Unexpected 200 on POST**: Cenit may return 200 instead of 201 for creation. Do not treat this as an error -- confirm by checking for an `id` in the response body.

## Playbook

### 1. Set Up a Complete Integration Flow

1. POST /setup/namespace -- create a namespace to organize your resources
2. POST /setup/connection -- create a connection with the target system URL and credentials
3. POST /setup/webhook -- define the webhook (HTTP method, path, headers)
4. POST /setup/translator -- create a translator to map data between formats
5. POST /setup/flow -- create a flow that ties the connection, webhook, and translator together
6. GET /setup/flow/{id} -- verify the flow was created correctly

### 2. Audit All Configured Resources

1. GET /setup/namespace/ -- list all namespaces
2. GET /setup/connection -- list all connections
3. GET /setup/webhook/ -- list all webhooks
4. GET /setup/flow/ -- list all flows
5. GET /setup/scheduler/ -- list all schedulers
6. Cross-reference flow details (GET /setup/flow/{id}) to confirm each flow references valid connections and webhooks

### 3. Clean Up Unused Resources

1. GET /setup/flow/ -- list flows and identify unused ones
2. DELETE /setup/flow/{id} -- remove unused flows first (they reference other resources)
3. GET /setup/connection -- identify connections no longer referenced by any flow
4. DELETE /setup/connection/{id} -- remove orphaned connections
5. Repeat for webhooks, translators, and schemas as needed

### 4. Set Up Event-Driven Processing

1. POST /setup/data_type/ -- register the data type you want to monitor
2. POST /setup/observer/ -- create an observer that watches for changes on that data type
3. POST /setup/translator -- create a translator for the outbound data format
4. POST /setup/connection -- set up the target connection
5. POST /setup/webhook -- define the outbound webhook
6. POST /setup/flow -- wire everything together: observer triggers the flow, which uses the connection, webhook, and translator

### 5. Schedule Recurring Data Sync

1. POST /setup/connection -- configure source and destination connections
2. POST /setup/translator -- define data transformation rules
3. POST /setup/webhook -- set up the API call details
4. POST /setup/scheduler/ -- create a scheduler with the desired cron expression
5. POST /setup/flow -- create a flow triggered by the scheduler instead of an observer
6. GET /setup/scheduler/{id} -- verify the scheduler configuration and next run time


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
