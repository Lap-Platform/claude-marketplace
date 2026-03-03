---
name: cdnmanagementclient
description: "CdnManagementClient API skill. Use when working with CdnManagementClient for subscriptions, providers. Covers 35 endpoints."
version: 1.0.0
generator: lapsh
---

# CdnManagementClient
API version: 2019-06-15-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.Cdn/operations -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/generateSsoUri -- create first generateSsoUri

## Endpoints

35 endpoints across 2 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Cdn/profiles | Lists all of the CDN profiles within an Azure subscription. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles | Lists all of the CDN profiles within a resource group. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName} | Gets a CDN profile with the specified profile name under the specified subscription and resource group. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName} | Creates a new CDN profile with a profile name under the specified subscription and resource group. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName} | Updates an existing CDN profile with the specified profile name under the specified subscription and resource group. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName} | Deletes an existing CDN profile with the specified parameters. Deleting a profile will result in the deletion of all of the sub-resources including endpoints, origins and custom domains. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/generateSsoUri | Generates a dynamic SSO URI used to sign in to the CDN supplemental portal. Supplemental portal is used to configure advanced feature capabilities that are not yet available in the Azure portal, such as core reports in a standard profile; rules engine, advanced HTTP reports, and real-time stats and alerts in a premium profile. The SSO URI changes approximately every 10 minutes. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/getSupportedOptimizationTypes | Gets the supported optimization types for the current profile. A user can create an endpoint with an optimization type from the listed values. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/checkResourceUsage | Checks the quota and actual usage of endpoints under the given CDN profile. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints | Lists existing CDN endpoints. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName} | Gets an existing CDN endpoint with the specified endpoint name under the specified subscription, resource group and profile. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName} | Creates a new CDN endpoint with the specified endpoint name under the specified subscription, resource group and profile. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName} | Updates an existing CDN endpoint with the specified endpoint name under the specified subscription, resource group and profile. Only tags and Origin HostHeader can be updated after creating an endpoint. To update origins, use the Update Origin operation. To update custom domains, use the Update Custom Domain operation. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName} | Deletes an existing CDN endpoint with the specified endpoint name under the specified subscription, resource group and profile. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}/start | Starts an existing CDN endpoint that is on a stopped state. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}/stop | Stops an existing running CDN endpoint. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}/purge | Removes a content from CDN. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}/load | Pre-loads a content to CDN. Available for Verizon Profiles. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}/validateCustomDomain | Validates the custom domain mapping to ensure it maps to the correct CDN endpoint in DNS. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}/checkResourceUsage | Checks the quota and usage of geo filters and custom domains under the given endpoint. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}/origins | Lists all of the existing origins within an endpoint. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}/origins/{originName} | Gets an existing origin within an endpoint. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}/origins/{originName} | Updates an existing origin within an endpoint. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}/customDomains | Lists all of the existing custom domains within an endpoint. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}/customDomains/{customDomainName} | Gets an existing custom domain within an endpoint. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}/customDomains/{customDomainName} | Creates a new custom domain within an endpoint. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}/customDomains/{customDomainName} | Deletes an existing custom domain within an endpoint. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}/customDomains/{customDomainName}/disableCustomHttps | Disable https delivery of the custom domain. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}/customDomains/{customDomainName}/enableCustomHttps | Enable https delivery of the custom domain. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Cdn/checkNameAvailability | Check the availability of a resource name. This is needed for resources where name is globally unique, such as a CDN endpoint. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Cdn/validateProbe | Check if the probe path is a valid path and the file can be accessed. Probe path is the path to a file hosted on the origin server to help accelerate the delivery of dynamic content via the CDN endpoint. This path is relative to the origin path specified in the endpoint configuration. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Cdn/checkResourceUsage | Check the quota and actual usage of the CDN profiles under the given subscription. |

### providers
| Method | Path | Description |
|--------|------|-------------|
| POST | /providers/Microsoft.Cdn/checkNameAvailability | Check the availability of a resource name. This is needed for resources where name is globally unique, such as a CDN endpoint. |
| GET | /providers/Microsoft.Cdn/operations | Lists all of the available CDN REST API operations. |
| GET | /providers/Microsoft.Cdn/edgenodes | Edgenodes are the global Point of Presence (POP) locations used to deliver CDN content to end users. |

## Enhanced Skill Content
## Question Mapping

- "List all CDN profiles in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Cdn/profiles
- "What CDN profiles exist in a specific resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles
- "Get details for a specific CDN profile?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}
- "Create or update a CDN profile?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}
- "Delete a CDN profile?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}
- "What endpoints are configured under a CDN profile?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints
- "Purge cached content from a CDN endpoint?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}/purge
- "Pre-load content into a CDN endpoint cache?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}/load
- "Start a stopped CDN endpoint?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}/start
- "Stop a running CDN endpoint?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}/stop
- "Check if a CDN name is available globally?" -> POST /providers/Microsoft.Cdn/checkNameAvailability
- "Enable HTTPS on a custom domain?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}/customDomains/{customDomainName}/enableCustomHttps
- "What custom domains are on my CDN endpoint?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}/customDomains
- "What optimization types does my profile support?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/getSupportedOptimizationTypes
- "What edge node locations are available?" -> GET /providers/Microsoft.Cdn/edgenodes

## Response Tips

- **Profiles/Endpoints/Origins/CustomDomains (GET list):** Responses are paged via `nextLink`; keep following it until absent. Each item includes `properties.provisioningState` and `properties.resourceState` for status.
- **PUT/PATCH (create/update):** 200 means completed synchronously, 201 means created, 202 means accepted for async processing -- check the `Location` or `Azure-AsyncOperation` header and poll until terminal state.
- **DELETE:** 202 means deletion is in progress (poll the async operation URL), 204 means the resource was already gone -- both are success.
- **POST actions (purge/load/start/stop):** 202 means the operation is queued; the response body may be empty. Use the operation URL from headers to track completion.
- **checkNameAvailability:** Returns `{ nameAvailable: bool, reason: string, message: string }` -- check `nameAvailable` before attempting resource creation.
- **checkResourceUsage:** Returns an array of quota objects with `currentValue` and `limit` -- compare these to gauge remaining capacity.
- **Error responses:** All endpoints return `ErrorResponse` with `error.code` and `error.message` on 4xx/5xx; parse `error.code` for programmatic handling.

## Anomaly Flags

- **Resource quota near limit:** After calling checkResourceUsage, alert when `currentValue` exceeds 80% of `limit` for profiles or endpoints.
- **Stuck provisioning state:** If a profile or endpoint shows `provisioningState` of "Creating" or "Deleting" for an extended period, surface as potentially stuck.
- **Endpoint in stopped state:** Flag endpoints where `resourceState` is "Stopped" -- they are not serving traffic and may be unintentional.
- **Custom domain without HTTPS:** When listing custom domains, flag any where HTTPS is not enabled (`customHttpsProvisioningState` is "Disabled").
- **202 without async operation header:** If a mutating call returns 202 but no `Azure-AsyncOperation` or `Location` header, flag it -- the operation cannot be tracked.
- **Deprecated API version:** This spec uses `2019-06-15-preview`; surface a warning that this is a preview version and recommend checking for a newer GA version.
- **Failed purge/load operations:** If polling an async purge or load operation results in a failed terminal state, alert immediately since stale content may be served.

## Playbook

### 1. Set Up a New CDN Profile and Endpoint

1. Call POST /providers/Microsoft.Cdn/checkNameAvailability with the desired profile name to confirm it is available.
2. Call PUT .../profiles/{profileName} with the `profile` body (sku, location, tags) to create the profile. If 202, poll the async operation until complete.
3. Call PUT .../profiles/{profileName}/endpoints/{endpointName} with the `endpoint` body (origins, optimization type). Poll if 202.
4. Call GET .../profiles/{profileName}/endpoints/{endpointName} to verify `resourceState` is "Running".
5. Call POST .../endpoints/{endpointName}/validateCustomDomain to verify your custom domain CNAME is set up correctly before adding it.

### 2. Purge and Pre-Load Content

1. Call POST .../endpoints/{endpointName}/purge with `contentFilePaths` listing the paths to invalidate (e.g., `["/css/*", "/images/logo.png"]`).
2. Poll the async operation from the 202 response until it reaches a terminal state.
3. Call POST .../endpoints/{endpointName}/load with the specific file paths to pre-warm into edge caches.
4. Poll the load operation until complete.
5. Verify by requesting the content through the CDN URL and checking response headers for a cache HIT.

### 3. Add and Secure a Custom Domain

1. Call POST .../endpoints/{endpointName}/validateCustomDomain with `{ hostName: "cdn.example.com" }` to confirm DNS is properly configured.
2. Call PUT .../endpoints/{endpointName}/customDomains/{customDomainName} with the hostname properties.
3. Poll the 202 response until the custom domain is provisioned.
4. Call POST .../customDomains/{customDomainName}/enableCustomHttps (optionally pass `customDomainHttpsParameters` for bring-your-own-cert).
5. Poll until `customHttpsProvisioningState` reaches "Enabled" -- this can take several minutes as certificate provisioning occurs.

### 4. Audit Resource Usage Across a Subscription

1. Call POST /subscriptions/{subscriptionId}/providers/Microsoft.Cdn/checkResourceUsage to get subscription-level quotas.
2. Call GET .../profiles to list all profiles in the subscription.
3. For each profile, call POST .../profiles/{profileName}/checkResourceUsage to see per-profile endpoint quotas.
4. For each endpoint, call POST .../endpoints/{endpointName}/checkResourceUsage to see per-endpoint resource usage.
5. Aggregate results and flag any resources above 80% utilization.

### 5. Safely Decommission a CDN Endpoint

1. Call POST .../endpoints/{endpointName}/stop to halt traffic. Poll the 202 until the endpoint state is "Stopped".
2. Call GET .../endpoints/{endpointName}/customDomains to list all custom domains.
3. For each custom domain, call POST .../customDomains/{name}/disableCustomHttps and then DELETE .../customDomains/{name}. Poll each deletion.
4. Call DELETE .../endpoints/{endpointName}. Poll the 202 until complete (or receive 204 confirming removal).
5. If the profile has no remaining endpoints, optionally call DELETE .../profiles/{profileName} to clean up.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
