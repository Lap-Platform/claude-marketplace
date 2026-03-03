---
name: subscriptiondefinitionsclient
description: "SubscriptionDefinitionsClient API skill. Use when working with SubscriptionDefinitionsClient for providers. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# SubscriptionDefinitionsClient
API version: 2017-11-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.Subscription/operations -- verify access

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Subscription/operations | Lists all of the available Microsoft.Subscription API operations. |
| PUT | /providers/Microsoft.Subscription/subscriptionDefinitions/{subscriptionDefinitionName} | Create an Azure subscription definition. |
| GET | /providers/Microsoft.Subscription/subscriptionDefinitions/{subscriptionDefinitionName} | Get an Azure subscription definition. |
| GET | /providers/Microsoft.Subscription/subscriptionDefinitions | List an Azure subscription definition by subscriptionId. |
| GET | /providers/Microsoft.Subscription/subscriptionOperations/{operationId} | Retrieves the status of the subscription definition PUT operation. The URI of this API is returned in the Location field of the response header. |

## Enhanced Skill Content
## Question Mapping

- "What operations are available for subscription management?" -> GET /providers/Microsoft.Subscription/operations
- "How do I create a new subscription definition?" -> PUT /providers/Microsoft.Subscription/subscriptionDefinitions/{subscriptionDefinitionName}
- "How do I update an existing subscription definition?" -> PUT /providers/Microsoft.Subscription/subscriptionDefinitions/{subscriptionDefinitionName}
- "What are the details of a specific subscription definition?" -> GET /providers/Microsoft.Subscription/subscriptionDefinitions/{subscriptionDefinitionName}
- "Does a subscription definition with this name already exist?" -> GET /providers/Microsoft.Subscription/subscriptionDefinitions/{subscriptionDefinitionName}
- "List all subscription definitions in my tenant." -> GET /providers/Microsoft.Subscription/subscriptionDefinitions
- "How many subscription definitions do I have?" -> GET /providers/Microsoft.Subscription/subscriptionDefinitions
- "What is the status of my subscription creation operation?" -> GET /providers/Microsoft.Subscription/subscriptionOperations/{operationId}
- "Is my subscription provisioning complete yet?" -> GET /providers/Microsoft.Subscription/subscriptionOperations/{operationId}
- "How do I create a subscription and track its progress?" -> PUT /providers/Microsoft.Subscription/subscriptionDefinitions/{subscriptionDefinitionName} then GET /providers/Microsoft.Subscription/subscriptionOperations/{operationId}
- "What API version should I use for subscription definitions?" -> GET /providers/Microsoft.Subscription/operations
- "How do I rename or reconfigure a subscription definition?" -> GET /providers/Microsoft.Subscription/subscriptionDefinitions/{subscriptionDefinitionName} then PUT /providers/Microsoft.Subscription/subscriptionDefinitions/{subscriptionDefinitionName}
- "Why did my subscription creation return 202 instead of 200?" -> GET /providers/Microsoft.Subscription/subscriptionOperations/{operationId}

## Response Tips

- **Operations** (GET .../operations): Returns a list of available provider operations; look for `value[]` array with `name`, `display` fields.
- **Subscription Definition CRUD** (PUT/GET .../subscriptionDefinitions/{name}): 200 means immediate success; 202 on PUT means async provisioning -- extract `operationId` from the response headers (`Location` or `Azure-AsyncOperation`) for polling.
- **List Definitions** (GET .../subscriptionDefinitions): Response may include `nextLink` for pagination; follow it until absent to retrieve all results.
- **Operation Status** (GET .../subscriptionOperations/{operationId}): 202 means still in progress, 200 means completed; check `status` field for `Succeeded`, `Failed`, or `InProgress`.

## Anomaly Flags

- **202 without Location header**: If a PUT returns 202 but no `Location` or `Azure-AsyncOperation` header, the operation cannot be polled -- surface this immediately.
- **Operation stuck in progress**: If polling an operationId returns 202 repeatedly beyond 10 minutes, flag a potential provisioning hang.
- **404 on definition GET**: The subscription definition name may be misspelled or deleted -- prompt the user to list all definitions to verify.
- **api-version mismatch**: This is a preview API (`2017-11-01-preview`). If the service returns `InvalidApiVersionParameter`, surface that the version may have been retired or graduated to GA.
- **Throttling (429)**: Azure ARM APIs enforce rate limits. If a 429 response appears, extract `Retry-After` header and wait before retrying. Alert the user if repeated.
- **Deprecated preview API**: `2017-11-01-preview` is old. Proactively note that a newer stable or preview version may be available when the user first connects.

## Playbook

### 1. Create a New Subscription Definition and Track Provisioning

1. Call PUT /providers/Microsoft.Subscription/subscriptionDefinitions/{subscriptionDefinitionName} with the definition body and `api-version=2017-11-01-preview`.
2. If response is 200, the definition was created synchronously -- done.
3. If response is 202, extract the `operationId` from the `Location` or `Azure-AsyncOperation` header.
4. Poll GET /providers/Microsoft.Subscription/subscriptionOperations/{operationId} with the same `api-version`.
5. Repeat step 4 every 15-30 seconds until the response is 200 (completed) or an error is returned.

### 2. Audit All Subscription Definitions

1. Call GET /providers/Microsoft.Subscription/subscriptionDefinitions with `api-version=2017-11-01-preview`.
2. Parse the `value[]` array from the response.
3. If `nextLink` is present, follow it to retrieve additional pages.
4. For each definition, optionally call GET .../subscriptionDefinitions/{name} to retrieve full details.
5. Compile results into a summary with name, offer type, and status.

### 3. Check Available Operations Before Automating

1. Call GET /providers/Microsoft.Subscription/operations with `api-version=2017-11-01-preview`.
2. Review the returned operations list to confirm which actions are supported.
3. Use the operation names and descriptions to map to your automation requirements.
4. Proceed with the appropriate endpoint calls based on confirmed capabilities.

### 4. Update an Existing Subscription Definition

1. Call GET /providers/Microsoft.Subscription/subscriptionDefinitions/{subscriptionDefinitionName} to retrieve the current definition.
2. Modify the desired fields in the response body.
3. Call PUT /providers/Microsoft.Subscription/subscriptionDefinitions/{subscriptionDefinitionName} with the updated body.
4. Handle 200 (immediate) or 202 (async) as in Playbook 1.

### 5. Diagnose a Failed Subscription Operation

1. Identify the `operationId` from the original PUT response headers.
2. Call GET /providers/Microsoft.Subscription/subscriptionOperations/{operationId} with `api-version=2017-11-01-preview`.
3. Inspect the `status` field: if `Failed`, examine the `error` object for `code` and `message`.
4. Cross-reference the error code with Azure documentation or retry with corrected parameters.
5. If status is still 202 (in progress), wait and poll again -- do not assume failure from a single check.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
