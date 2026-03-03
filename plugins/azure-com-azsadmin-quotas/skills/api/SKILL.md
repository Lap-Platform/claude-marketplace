---
name: compute-admin-client
description: "Compute Admin Client API skill. Use when working with Compute Admin Client for subscriptions. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# Compute Admin Client
API version: 2018-02-09

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/quotas -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/quotas/{quotaName} | Returns the requested Compute quota. |
| PUT | /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/quotas/{quotaName} | Creates or Updates a Compute Quota. |
| DELETE | /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/quotas/{quotaName} | Deletes specified Compute quota |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/quotas | Lists all Compute quotas. |

## Enhanced Skill Content
## Question Mapping

- "What compute quotas exist in this location?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/quotas
- "Show me the details of a specific compute quota" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/quotas/{quotaName}
- "What are the current VM limits for this region?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/quotas/{quotaName}
- "Create a new compute quota with custom limits" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/quotas/{quotaName}
- "Update an existing compute quota" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/quotas/{quotaName}
- "Set the maximum number of VMs allowed for a tenant" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/quotas/{quotaName}
- "Remove a compute quota" -> DELETE /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/quotas/{quotaName}
- "Delete the custom quota I created earlier" -> DELETE /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/quotas/{quotaName}
- "List all quota definitions available in eastus" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/quotas
- "How do I cap the number of cores a tenant can use?" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/quotas/{quotaName}
- "Does a quota named 'Default' exist in this location?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/quotas/{quotaName}
- "Clone an existing quota with modified limits" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/quotas/{quotaName} + PUT /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/quotas/{quotaName}

## Response Tips

- **Single quota (GET by name):** Response is a single resource object with `id`, `name`, `type`, and `properties` containing numeric limits (cores, VMs, scale sets). A 404 means the quota name does not exist in that location.
- **Quota list (GET all):** Response contains a `value` array of quota objects. No pagination -- Azure Stack admin quotas are a bounded set. An empty `value` array means no quotas are configured.
- **Create/Update (PUT):** Returns the full quota object as created or modified. The request body must include `properties` with the desired limits. Omitted properties may reset to defaults.
- **Delete (DELETE):** Returns 200 on success. Attempting to delete a built-in or in-use quota may return an error with a descriptive `message` field in the error body.

## Anomaly Flags

- **404 on GET by name:** The quota does not exist -- surface this clearly rather than returning an empty result, and suggest listing all quotas to verify the name.
- **PUT with missing properties:** If the response shows limit values that differ from what was sent, flag that omitted fields may have been reset to defaults.
- **Delete of built-in quota:** If DELETE returns an error, flag that built-in/default quotas typically cannot be removed.
- **OAuth token expiry:** Surface 401 responses proactively -- the bearer token may have expired and needs refresh.
- **Subscription or location mismatch:** A 404 at the subscription or location level (not just quotaName) indicates the path parameters are wrong -- flag which segment likely failed.
- **Throttling (429):** If Azure returns retry-after headers, surface the wait time and offer to retry automatically.

## Playbook

### 1. Audit All Compute Quotas in a Location

1. Call GET `/subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/quotas` to list all quotas.
2. For each quota in the `value` array, review `properties` for core counts, VM limits, and scale set limits.
3. Flag any quotas with unusually high or zero limits.

### 2. Create a Custom Tenant Quota

1. Call GET on the list endpoint to review existing quotas for reference values.
2. Call PUT `/subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/quotas/{quotaName}` with a new `quotaName` and a body specifying desired `properties` (core limit, VM limit, scale set limit).
3. Verify the response matches the intended configuration.
4. Assign the new quota to a tenant plan or offer (outside this API).

### 3. Modify Limits on an Existing Quota

1. Call GET `/subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/quotas/{quotaName}` to retrieve current values.
2. Adjust the desired fields in `properties`.
3. Call PUT with the same `quotaName` and the updated body.
4. Compare the response to confirm all changes took effect.

### 4. Safely Remove a Custom Quota

1. Call GET on the specific quota to confirm it exists and note its current configuration.
2. Verify the quota is not referenced by any active plan or offer (outside this API).
3. Call DELETE `/subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/quotas/{quotaName}`.
4. Call GET on the same quota to confirm it returns 404.
5. If DELETE fails, check the error message -- built-in quotas and quotas in use cannot be deleted.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
