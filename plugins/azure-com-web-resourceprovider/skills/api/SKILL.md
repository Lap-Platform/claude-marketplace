---
name: api-client
description: "API Client API skill. Use when working with API Client for providers, subscriptions. Covers 17 endpoints."
version: 1.0.0
generator: lapsh
---

# API Client
API version: 2018-02-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.Web/publishingUsers/web -- verify access
3. POST /subscriptions/{subscriptionId}/providers/Microsoft.Web/checknameavailability -- create first checknameavailability

## Endpoints

17 endpoints across 2 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Web/publishingUsers/web | Gets publishing user |
| PUT | /providers/Microsoft.Web/publishingUsers/web | Updates publishing user |
| GET | /providers/Microsoft.Web/sourcecontrols | Gets the source controls available for Azure websites. |
| GET | /providers/Microsoft.Web/sourcecontrols/{sourceControlType} | Gets source control token |
| PUT | /providers/Microsoft.Web/sourcecontrols/{sourceControlType} | Updates source control token |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Web/billingMeters | Gets a list of meters for a given location. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Web/checknameavailability | Check if a resource name is available. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Web/deploymentLocations | Gets list of available geo regions plus ministamps |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Web/geoRegions | Get a list of available geographical regions. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Web/listSitesAssignedToHostName | List all apps that are assigned to a hostname. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Web/premieraddonoffers | List all premier add-on offers. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Web/skus | List all SKUs. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Web/verifyHostingEnvironmentVnet | Verifies if this VNET is compatible with an App Service Environment by analyzing the Network Security Group rules. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/moveResources | Move resources between resource groups. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/validate | Validate if a resource can be created. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/validateContainerSettings | Validate if the container settings are correct. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/validateMoveResources | Validate whether a resource can be moved. |

## Enhanced Skill Content
## Question Mapping

- "How do I get the current publishing user credentials?" -> GET /providers/Microsoft.Web/publishingUsers/web
- "How do I update or set publishing user credentials?" -> PUT /providers/Microsoft.Web/publishingUsers/web
- "What source control integrations are configured?" -> GET /providers/Microsoft.Web/sourcecontrols
- "How do I get details for a specific source control provider like GitHub?" -> GET /providers/Microsoft.Web/sourcecontrols/{sourceControlType}
- "How do I configure a source control integration token?" -> PUT /providers/Microsoft.Web/sourcecontrols/{sourceControlType}
- "What billing meters apply to my subscription in a given region?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/billingMeters
- "Is a specific app name available?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Web/checknameavailability
- "What deployment locations can I use?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/deploymentLocations
- "Which Azure regions support Linux app service plans?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/geoRegions
- "Which sites are assigned to a given hostname?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Web/listSitesAssignedToHostName
- "What premier add-on offers are available for my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/premieraddonoffers
- "What App Service SKUs can I use?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/skus
- "Can my VNet be used with an App Service Environment?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Web/verifyHostingEnvironmentVnet
- "How do I validate a web app configuration before creating it?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/validate
- "How do I move web resources between resource groups?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/moveResources

## Response Tips

- **Publishing users & source controls**: Responses are single-object envelopes with `properties` nested one level deep; extract credentials and tokens from there, not the top level.
- **Billing meters & SKUs**: Expect `value` arrays with `nextLink` for pagination; follow `nextLink` until null to retrieve all entries.
- **Check name availability**: Response contains `nameAvailable` (boolean), `reason`, and `message`; always check all three since `reason` distinguishes "Invalid" from "AlreadyExists".
- **Geo regions & deployment locations**: Filter results client-side using `sku`, `linuxWorkersEnabled`, and `xenonWorkersEnabled` query params rather than fetching everything.
- **Move & validate resources (204 responses)**: A 204 means success with no body; for async moves, check the `Location` or `Azure-AsyncOperation` header for long-running operation status.
- **Container settings validation**: Errors are returned inline in the 200 body as validation messages, not as HTTP error codes.

## Anomaly Flags

- **Rate limiting**: Surface `Retry-After` and `x-ms-ratelimit-remaining-subscription-reads`/`writes` headers when remaining calls drop below 50; Azure ARM throttles at the subscription level.
- **Async operations**: Flag any response containing `Azure-AsyncOperation` or `Location` headers -- the operation is not complete and requires polling.
- **Deprecated API version**: If the response includes `x-ms-deprecation` or a `warning` header, alert the user that version `2018-02-01` may be sunsetting.
- **Name conflicts**: When `checknameavailability` returns `nameAvailable: false`, proactively suggest appending a region suffix or random string.
- **VNet verification failures**: Surface the specific `verifyHostingEnvironmentVnet` error codes (subnet delegation, address space conflicts) since they require infrastructure changes, not just retries.
- **Missing subscriptionId**: Flag early if any subscription-scoped call returns 404 -- this typically means the subscription ID is wrong or the Microsoft.Web provider is not registered.

## Playbook

### 1. Set Up Source Control Integration (e.g., GitHub)

1. List existing integrations: `GET /providers/Microsoft.Web/sourcecontrols`
2. Pick the target type (e.g., `GitHub`) and check current config: `GET /providers/Microsoft.Web/sourcecontrols/GitHub`
3. Generate a personal access token in GitHub with `repo` and `admin:repo_hook` scopes
4. Update the source control with the token: `PUT /providers/Microsoft.Web/sourcecontrols/GitHub` with `requestMessage` containing the token and metadata
5. Verify by re-reading: `GET /providers/Microsoft.Web/sourcecontrols/GitHub` and confirm the token property is set

### 2. Validate and Create a New Web App

1. Check name availability: `POST /subscriptions/{subscriptionId}/providers/Microsoft.Web/checknameavailability` with `{ name, type: "Microsoft.Web/sites" }`
2. If unavailable, adjust the name and repeat step 1
3. List available regions: `GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/geoRegions` (filter by `sku` and `linuxWorkersEnabled` as needed)
4. Validate the planned configuration: `POST /subscriptions/{subscriptionId}/resourceGroups/{rg}/providers/Microsoft.Web/validate` with the `validateRequest` body
5. If validation passes, proceed with resource creation via the full Web Apps API

### 3. Move Web Resources Between Resource Groups

1. Identify resources to move in the source resource group
2. Validate the move: `POST /subscriptions/{subscriptionId}/resourceGroups/{sourceRg}/validateMoveResources` with `moveResourceEnvelope` listing resource IDs and target group
3. If validation returns 204, execute the move: `POST /subscriptions/{subscriptionId}/resourceGroups/{sourceRg}/moveResources` with the same envelope
4. Check the `Location` header for the async operation URL and poll until complete
5. Verify resources appear in the target resource group

### 4. Verify VNet Compatibility for App Service Environment

1. Gather the target VNet name, subnet, and resource group
2. Call `POST /subscriptions/{subscriptionId}/providers/Microsoft.Web/verifyHostingEnvironmentVnet` with `parameters` containing VNet resource ID, subnet name, and environment type
3. Inspect the response for validation errors (subnet delegation, address space, NSG rules)
4. Resolve any flagged issues in the Azure networking layer
5. Re-run verification until the response confirms compatibility

### 5. Review Billing and SKU Options for Cost Planning

1. List available SKUs: `GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/skus`
2. Get billing meters for your target region: `GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/billingMeters?billingLocation={region}`
3. Cross-reference meter IDs with SKU capabilities to identify cost-effective tiers
4. Optionally check premier add-on offers: `GET /subscriptions/{subscriptionId}/providers/Microsoft.Web/premieraddonoffers`
5. Use the billing meter rates and SKU constraints to model monthly cost before provisioning


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
