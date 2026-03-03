---
name: apimanagementclient
description: "ApiManagementClient API skill. Use when working with ApiManagementClient for subscriptions. Covers 9 endpoints."
version: 1.0.0
generator: lapsh
---

# ApiManagementClient
API version: 2019-12-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/subscriptions -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/subscriptions/{sid}/regeneratePrimaryKey -- create first regeneratePrimaryKey

## Endpoints

9 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/subscriptions | Lists all subscriptions of the API Management service instance. |
| HEAD | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/subscriptions/{sid} | Gets the entity state (Etag) version of the apimanagement subscription specified by its identifier. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/subscriptions/{sid} | Gets the specified Subscription entity. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/subscriptions/{sid} | Creates or updates the subscription of specified user to the specified product. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/subscriptions/{sid} | Updates the details of a subscription specified by its identifier. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/subscriptions/{sid} | Deletes the specified subscription. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/subscriptions/{sid}/regeneratePrimaryKey | Regenerates primary key of existing subscription of the API Management service instance. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/subscriptions/{sid}/regenerateSecondaryKey | Regenerates secondary key of existing subscription of the API Management service instance. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/subscriptions/{sid}/listSecrets | Gets the subscription keys. |

## Enhanced Skill Content
## Question Mapping

- "List all subscriptions in my API Management service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/subscriptions
- "Filter subscriptions by a specific product or user?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/subscriptions (with $filter)
- "Does subscription {sid} exist?" -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/subscriptions/{sid}
- "Get details of a specific subscription?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/subscriptions/{sid}
- "Create a new subscription for an API product?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/subscriptions/{sid}
- "Update an existing subscription's display name or state?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/subscriptions/{sid}
- "Cancel or delete a subscription?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/subscriptions/{sid}
- "Rotate the primary key for a subscription?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/subscriptions/{sid}/regeneratePrimaryKey
- "Rotate the secondary key for a subscription?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/subscriptions/{sid}/regenerateSecondaryKey
- "Retrieve the subscription keys (primary and secondary)?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/subscriptions/{sid}/listSecrets
- "How do I check if a subscription is still active before calling its API?" -> HEAD .../{sid} then GET .../{sid}
- "How do I safely rotate keys without downtime?" -> POST .../regenerateSecondaryKey, migrate consumers, then POST .../regeneratePrimaryKey
- "How do I provision a new user with API access?" -> PUT .../{sid} with scope and product parameters

## Response Tips

- **List (GET collection):** Returns a paged array; look for `nextLink` to fetch additional pages. Use `$filter` (OData syntax) to narrow by `stateComment`, `userId`, `productId`, or `displayName`.
- **Existence check (HEAD):** Returns 200 with no body if the subscription exists; 404 if not. Use this before updates to avoid blind writes.
- **Detail (GET by sid):** Returns the full subscription contract including `primaryKey`, `secondaryKey`, `state`, `scope`, and `expirationDate`. Check `state` for `active`, `suspended`, `cancelled`, or `expired`.
- **Create/Update (PUT/PATCH):** PUT returns 201 on creation, 200 on update. PATCH returns 204 with no body on success. Both require `If-Match: *` header for concurrency control.
- **Delete (DELETE):** Returns 200 or 204 on success. A 404 means the subscription was already removed.
- **Key operations (POST):** regeneratePrimaryKey/regenerateSecondaryKey return 204 with no body. listSecrets returns 200 with the current key pair.

## Anomaly Flags

- **Subscription state drift:** Surface when a subscription's `state` is `suspended` or `expired` -- the consumer may be unaware their access is cut off.
- **Missing If-Match header:** PUT and PATCH calls that omit `If-Match` will fail with 412 Precondition Failed. Proactively remind the caller to include it.
- **Key exposure via listSecrets:** Flag when listSecrets is called -- secrets are returned in plaintext and should not be logged or stored insecurely.
- **Approaching expiration:** When GET returns an `expirationDate` within 7 days, alert the user to renew or extend the subscription.
- **Stale filter results:** If a list call with `$filter` returns zero results, suggest verifying the filter syntax (OData) before assuming no subscriptions match.
- **204 vs 200 ambiguity on DELETE:** Both are success codes. If the caller expects a response body, note that 204 means the resource was removed without a body.
- **Preview API version:** This API version (`2019-12-01-preview`) is a preview release. Surface a warning that behavior may change in GA, and recommend checking for a stable version.

## Playbook

### 1. Provision a New API Subscription

1. Decide on a subscription ID (`sid`) and gather the target `scope` (product or API path).
2. PUT to `/subscriptions/.../subscriptions/{sid}` with a body containing `displayName`, `scope`, `ownerId`, and `state: "active"`.
3. Confirm a 201 response (created) and note the returned `primaryKey` and `secondaryKey`.
4. Share the keys securely with the API consumer.

### 2. Zero-Downtime Key Rotation

1. Call POST `.../regenerateSecondaryKey` to rotate the secondary key (consumers are still using the primary key).
2. Call POST `.../listSecrets` to retrieve the new secondary key.
3. Distribute the new secondary key to all consumers and have them switch over.
4. Once all consumers are using the new secondary key, call POST `.../regeneratePrimaryKey`.
5. Optionally retrieve the new primary key via `listSecrets` and store it for the next rotation cycle.

### 3. Audit and Clean Up Inactive Subscriptions

1. GET the subscription list with `$filter=state eq 'cancelled' or state eq 'expired'`.
2. For each returned subscription, review the `displayName` and `ownerId` to confirm it is safe to remove.
3. DELETE each confirmed subscription by `sid`.
4. Verify removal by calling HEAD on each deleted `sid` and expecting a 404.

### 4. Check Subscription Health Before Integration

1. Call HEAD on the target subscription `sid` to confirm it exists (expect 200).
2. GET the full subscription detail and verify `state` is `active`.
3. Check `expirationDate` -- if within 30 days, flag for renewal.
4. Call `listSecrets` to verify keys are retrievable and match what the consuming application has configured.

### 5. Bulk Subscription Inventory

1. GET the subscription list without filters to retrieve the first page.
2. If the response contains `nextLink`, follow it to fetch subsequent pages until all subscriptions are collected.
3. Group subscriptions by `state` to get a breakdown of active, suspended, cancelled, and expired.
4. For any `suspended` subscriptions, GET the detail to check `stateComment` for the suspension reason.
5. Export the inventory for reporting or feed into a cleanup workflow.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
