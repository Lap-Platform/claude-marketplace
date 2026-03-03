---
name: storagemanagementclient
description: "StorageManagementClient API skill. Use when working with StorageManagementClient for subscriptions. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# StorageManagementClient
API version: 2019-08-08-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/acquisitions -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/acquisitions | Returns a list of BLOB acquisitions. |

## Enhanced Skill Content
## Question Mapping

- "What storage acquisitions exist in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/acquisitions
- "List all storage acquisitions for a specific location?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/acquisitions
- "How do I check storage acquisition status in Azure Stack?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/acquisitions
- "What storage accounts have been acquired in eastus?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/acquisitions
- "Show me all pending storage acquisitions?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/acquisitions
- "Can I audit storage provisioning activity for a region?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/acquisitions
- "What storage resources are allocated in my Azure Stack location?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/acquisitions
- "How do I monitor storage capacity acquisitions?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/acquisitions
- "List acquisitions filtered by a specific Azure Stack region?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/acquisitions
- "What is the current storage acquisition inventory?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/acquisitions
- "Are there any failed storage acquisitions in my environment?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/acquisitions
- "How do I get storage admin acquisition details for compliance reporting?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/acquisitions

## Response Tips

- **Acquisitions list (200)**: Expect an array of acquisition objects, likely wrapped in a `value` property following Azure ARM conventions. Each acquisition may contain `id`, `name`, `type`, `properties`, and `location` fields. Check for a `nextLink` property to handle pagination -- if present, follow it to retrieve additional results. The `properties` sub-object holds the operational details (status, timestamps, capacity).

## Anomaly Flags

- **Preview API version**: This API uses `2019-08-08-preview` -- surface a warning that this is a preview version, may be deprecated or changed without notice, and should not be relied upon for production workloads.
- **Empty acquisitions list**: If the response returns an empty `value` array, flag that no acquisitions exist for the given location -- the user may have specified the wrong location or subscription.
- **HTTP 404 on location**: Surface immediately if the location path parameter does not match a valid Azure Stack location, as this indicates a configuration issue.
- **HTTP 401/403 errors**: Flag OAuth2 token expiry or insufficient RBAC permissions on the Storage Admin resource provider. The caller needs the appropriate Azure Stack admin role.
- **Throttling (HTTP 429)**: Surface `Retry-After` header value and recommend backing off. Azure ARM APIs enforce per-subscription rate limits.
- **Deprecation headers**: Watch for `Sunset` or `Deprecation` response headers signaling this preview endpoint is being retired.

## Playbook

### 1. List All Storage Acquisitions for a Location

1. Authenticate via OAuth2 and obtain a bearer token with scope `https://management.azure.com/.default`
2. Identify your `subscriptionId` and target `location` (e.g., `local`, `eastus`)
3. Call `GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/acquisitions` with header `Authorization: Bearer {token}`
4. Parse the `value` array from the response
5. If `nextLink` is present, follow it with another GET to retrieve the next page
6. Repeat until no `nextLink` is returned

### 2. Audit Storage Acquisitions Across All Locations

1. Retrieve the list of available Azure Stack locations for your subscription (via the Azure Resource Manager locations API)
2. For each location, call the acquisitions endpoint
3. Aggregate all results into a single collection
4. Filter or sort by acquisition status or timestamp as needed for the audit report
5. Flag any locations returning errors or empty results for follow-up

### 3. Monitor for New or Failed Acquisitions

1. Establish a baseline by calling the acquisitions endpoint and recording all current acquisition IDs
2. On a scheduled interval, re-query the endpoint
3. Diff the current results against the baseline to identify new acquisitions
4. Check the `properties.status` (or equivalent) field on each acquisition for failure states
5. Surface any new failures or unexpected status changes to the operator

### 4. Validate Permissions Before Querying

1. Attempt a call to the acquisitions endpoint with the current OAuth2 token
2. If HTTP 403 is returned, check the token's role assignments against the subscription
3. Ensure the identity has the `Storage Admin` or equivalent role on the target subscription
4. Re-authenticate with elevated permissions if needed
5. Retry the acquisitions call and confirm a 200 response

### 5. Transition Off Preview API

1. Check Azure documentation for a GA (stable) version of the Storage Admin acquisitions API
2. Compare the preview response schema against the GA schema for breaking changes
3. Update the `api-version` query parameter from `2019-08-08-preview` to the GA version
4. Test the GA endpoint in a non-production environment
5. Update all automation and monitoring scripts to use the stable version


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
