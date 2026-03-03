---
name: scim-provisioning-overview
description: "SCIM Provisioning Overview API skill. Use when working with SCIM Provisioning Overview for resources. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# SCIM Provisioning Overview

## Auth
Bearer bearer

## Base URL
https://api.frontegg.com/directory

## Setup
1. Set Authorization header with your Bearer token
2. GET /resources/v1/configurations/scim2 -- verify access
3. POST /resources/v1/configurations/scim2 -- create first scim2

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### resources
| Method | Path | Description |
|--------|------|-------------|
| GET | /resources/v1/configurations/scim2 | Get all SCIM configurations |
| POST | /resources/v1/configurations/scim2 | Create a SCIM configuration |
| GET | /resources/v1/configurations/scim2/{id} | Get a SCIM configuration by ID |
| PATCH | /resources/v1/configurations/scim2/{id} | Update a SCIM configuration |
| DELETE | /resources/v1/configurations/scim2/{id} | Delete a SCIM configuration |

## Enhanced Skill Content
## Question Mapping

- "How do I list all SCIM configurations?" -> GET /resources/v1/configurations/scim2
- "What SCIM connections exist for a specific tenant?" -> GET /resources/v1/configurations/scim2 (with tenantId filter)
- "How do I set up SCIM provisioning with Okta?" -> POST /resources/v1/configurations/scim2 (source: okta)
- "How do I create a new Azure AD SCIM connection?" -> POST /resources/v1/configurations/scim2 (source: azure-ad)
- "How do I get the SCIM bearer token for a connection?" -> POST /resources/v1/configurations/scim2 (token returned on creation)
- "What are the details of a specific SCIM configuration?" -> GET /resources/v1/configurations/scim2/{id}
- "When was a SCIM connection last synced?" -> GET /resources/v1/configurations/scim2/{id} (check lastSync)
- "How do I enable user management sync for an existing connection?" -> PATCH /resources/v1/configurations/scim2/{id}
- "How do I disable syncToUserManagement on a SCIM config?" -> PATCH /resources/v1/configurations/scim2/{id} (syncToUserManagement: false)
- "How do I remove a SCIM provisioning connection?" -> DELETE /resources/v1/configurations/scim2/{id}
- "How do I filter SCIM configs by identity provider source?" -> GET /resources/v1/configurations/scim2 (with source filter)
- "How do I rotate the SCIM token for a connection?" -> DELETE /resources/v1/configurations/scim2/{id} then POST /resources/v1/configurations/scim2
- "Can I rename a SCIM connection?" -> POST /resources/v1/configurations/scim2 (connectionName is set at creation; no rename via PATCH)

## Response Tips

- **GET (list):** Returns an array of configuration objects. Filter server-side using query params (tenantId, source, connectionName, id) rather than fetching all and filtering client-side.
- **POST (create):** Returns 201 with the new config including the `token` field -- this is the only time the SCIM bearer token is returned. Store it immediately.
- **GET (by id):** Returns the full config object. `lastSync` is nullable (null if never synced). `createdAt` is always present.
- **PATCH (update):** Returns 204 with no body. Follow up with a GET to confirm the change took effect.
- **DELETE:** Returns 204 with no body. A subsequent GET on the same id should return 404.

## Anomaly Flags

- **Token exposure on create:** The SCIM `token` is only returned once during POST. If the user does not capture it, flag that they must delete and recreate the connection to get a new token.
- **Null lastSync:** If `lastSync` is null on a connection that is not newly created, surface that syncing may not be configured on the identity provider side.
- **syncToUserManagement disabled:** If a user creates a connection without setting `syncToUserManagement: true`, flag that provisioned users will not appear in Frontegg user management until this is enabled via PATCH.
- **Source value "other":** If the source is set to `other`, flag that the user should verify their identity provider supports SCIM 2.0 and may need manual endpoint configuration.
- **Orphaned connections:** If listing returns connections with very old or null `lastSync` values, surface these as potentially stale integrations that should be reviewed or deleted.

## Playbook

### Set Up SCIM Provisioning for a New Identity Provider

1. Call POST /resources/v1/configurations/scim2 with the appropriate `source` (okta, azure-ad, frontegg, or other) and optional `connectionName`.
2. Capture the `token` from the 201 response -- this is the only time it is returned.
3. Copy the SCIM base URL (`https://api.frontegg.com/directory/resources/v1/configurations/scim2`) and the token into your identity provider's SCIM settings.
4. Optionally call PATCH /resources/v1/configurations/scim2/{id} to enable `syncToUserManagement: true`.
5. Verify the connection by checking GET /resources/v1/configurations/scim2/{id} and confirming `lastSync` populates after the first sync.

### Rotate a SCIM Connection Token

1. Call GET /resources/v1/configurations/scim2/{id} to capture the current config details (source, connectionName, syncToUserManagement).
2. Call DELETE /resources/v1/configurations/scim2/{id} to remove the old connection.
3. Call POST /resources/v1/configurations/scim2 with the same source, connectionName, and settings.
4. Capture the new `token` from the 201 response.
5. Update the token in your identity provider's SCIM configuration.

### Audit and Clean Up Stale SCIM Connections

1. Call GET /resources/v1/configurations/scim2 to list all connections.
2. For each connection, check the `lastSync` field -- identify any that are null or older than your expected sync interval.
3. For stale connections, call GET /resources/v1/configurations/scim2/{id} to review full details.
4. Call DELETE /resources/v1/configurations/scim2/{id} for any confirmed-stale connections.

### Enable User Management Sync on an Existing Connection

1. Call GET /resources/v1/configurations/scim2/{id} to confirm the current `syncToUserManagement` value.
2. Call PATCH /resources/v1/configurations/scim2/{id} with `syncToUserManagement: true`.
3. Call GET /resources/v1/configurations/scim2/{id} to verify the update was applied.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
