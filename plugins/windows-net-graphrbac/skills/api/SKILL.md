---
name: graphrbacmanagementclient
description: "GraphRbacManagementClient API skill. Use when working with GraphRbacManagementClient for {tenantID}. Covers 56 endpoints."
version: 1.0.0
generator: lapsh
---

# GraphRbacManagementClient
API version: 1.6

## Auth
OAuth2

## Base URL
https://graph.windows.net

## Setup
1. Configure auth: OAuth2
2. GET /{tenantID}/me -- verify access
3. POST /{tenantID}/applications -- create first applications

## Endpoints

56 endpoints across 1 groups. See references/api-spec.lap for full details.

### {tenantID}
| Method | Path | Description |
|--------|------|-------------|
| GET | /{tenantID}/me | Gets the details for the currently logged-in user. |
| GET | /{tenantID}/me/ownedObjects | Get the list of directory objects that are owned by the user. |
| POST | /{tenantID}/applications | Create a new application. |
| GET | /{tenantID}/applications | Lists applications by filter parameters. |
| POST | /{tenantID}/deletedApplications/{objectId}/restore | Restores the deleted application in the directory. |
| GET | /{tenantID}/deletedApplications | Gets a list of deleted applications in the directory. |
| DELETE | /{tenantID}/deletedApplications/{applicationObjectId} | Hard-delete an application. |
| DELETE | /{tenantID}/applications/{applicationObjectId} | Delete an application. |
| GET | /{tenantID}/applications/{applicationObjectId} | Get an application by object ID. |
| PATCH | /{tenantID}/applications/{applicationObjectId} | Update an existing application. |
| GET | /{tenantID}/applications/{applicationObjectId}/owners | Directory objects that are owners of the application. |
| POST | /{tenantID}/applications/{applicationObjectId}/$links/owners | Add an owner to an application. |
| DELETE | /{tenantID}/applications/{applicationObjectId}/$links/owners/{ownerObjectId} | Remove a member from owners. |
| GET | /{tenantID}/applications/{applicationObjectId}/keyCredentials | Get the keyCredentials associated with an application. |
| PATCH | /{tenantID}/applications/{applicationObjectId}/keyCredentials | Update the keyCredentials associated with an application. |
| GET | /{tenantID}/applications/{applicationObjectId}/passwordCredentials | Get the passwordCredentials associated with an application. |
| PATCH | /{tenantID}/applications/{applicationObjectId}/passwordCredentials | Update passwordCredentials associated with an application. |
| POST | /{tenantID}/isMemberOf | Checks whether the specified user, group, contact, or service principal is a direct or transitive member of the specified group. |
| DELETE | /{tenantID}/groups/{groupObjectId}/$links/members/{memberObjectId} | Remove a member from a group. |
| POST | /{tenantID}/groups/{groupObjectId}/$links/members | Add a member to a group. |
| POST | /{tenantID}/groups | Create a group in the directory. |
| GET | /{tenantID}/groups | Gets list of groups for the current tenant. |
| GET | /{tenantID}/groups/{objectId}/members | Gets the members of a group. |
| GET | /{tenantID}/groups/{objectId} | Gets group information from the directory. |
| DELETE | /{tenantID}/groups/{objectId} | Delete a group from the directory. |
| POST | /{tenantID}/groups/{objectId}/getMemberGroups | Gets a collection of object IDs of groups of which the specified group is a member. |
| GET | /{tenantID}/groups/{objectId}/owners | Directory objects that are owners of the group. |
| POST | /{tenantID}/groups/{objectId}/$links/owners | Add an owner to a group. |
| DELETE | /{tenantID}/groups/{objectId}/$links/owners/{ownerObjectId} | Remove a member from owners. |
| POST | /{tenantID}/servicePrincipals | Creates a service principal in the directory. |
| GET | /{tenantID}/servicePrincipals | Gets a list of service principals from the current tenant. |
| GET | /{tenantID}/servicePrincipalsByAppId/{applicationID}/objectId | Gets an object id for a given application id from the current tenant. |
| PATCH | /{tenantID}/servicePrincipals/{objectId} | Updates a service principal in the directory. |
| DELETE | /{tenantID}/servicePrincipals/{objectId} | Deletes a service principal from the directory. |
| GET | /{tenantID}/servicePrincipals/{objectId} | Gets service principal information from the directory. Query by objectId or pass a filter to query by appId |
| GET | /{tenantID}/servicePrincipals/{objectId}/appRoleAssignedTo | Principals (users, groups, and service principals) that are assigned to this service principal. |
| GET | /{tenantID}/servicePrincipals/{objectId}/appRoleAssignments | Applications that the service principal is assigned to. |
| GET | /{tenantID}/servicePrincipals/{objectId}/owners | Directory objects that are owners of this service principal. |
| POST | /{tenantID}/servicePrincipals/{objectId}/$links/owners | Add an owner to a service principal. |
| DELETE | /{tenantID}/servicePrincipals/{objectId}/$links/owners/{ownerObjectId} | Remove a member from owners. |
| GET | /{tenantID}/servicePrincipals/{objectId}/keyCredentials | Get the keyCredentials associated with the specified service principal. |
| PATCH | /{tenantID}/servicePrincipals/{objectId}/keyCredentials | Update the keyCredentials associated with a service principal. |
| GET | /{tenantID}/servicePrincipals/{objectId}/passwordCredentials | Gets the passwordCredentials associated with a service principal. |
| PATCH | /{tenantID}/servicePrincipals/{objectId}/passwordCredentials | Updates the passwordCredentials associated with a service principal. |
| POST | /{tenantID}/users | Create a new user. |
| GET | /{tenantID}/users | Gets list of users for the current tenant. |
| GET | /{tenantID}/users/{upnOrObjectId} | Gets user information from the directory. |
| PATCH | /{tenantID}/users/{upnOrObjectId} | Updates a user. |
| DELETE | /{tenantID}/users/{upnOrObjectId} | Delete a user. |
| POST | /{tenantID}/users/{objectId}/getMemberGroups | Gets a collection that contains the object IDs of the groups of which the user is a member. |
| POST | /{tenantID}/getObjectsByObjectIds | Gets the directory objects specified in a list of object IDs. You can also specify which resource collections (users, groups, etc.) should be searched by specifying the optional types parameter. |
| GET | /{tenantID}/domains | Gets a list of domains for the current tenant. |
| GET | /{tenantID}/domains/{domainName} | Gets a specific domain in the current tenant. |
| GET | /{tenantID}/oauth2PermissionGrants | Queries OAuth2 permissions grants for the relevant SP ObjectId of an app. |
| POST | /{tenantID}/oauth2PermissionGrants | Grants OAuth2 permissions for the relevant resource Ids of an app. |
| DELETE | /{tenantID}/oauth2PermissionGrants/{objectId} | Delete a OAuth2 permission grant for the relevant resource Ids of an app. |

## Enhanced Skill Content
## Question Mapping

- "Who am I signed in as?" -> GET /{tenantID}/me
- "What objects do I own in this tenant?" -> GET /{tenantID}/me/ownedObjects
- "How do I register a new application?" -> POST /{tenantID}/applications
- "List all applications in the tenant" -> GET /{tenantID}/applications
- "How do I restore a deleted application?" -> POST /{tenantID}/deletedApplications/{objectId}/restore
- "What groups does a user belong to?" -> POST /{tenantID}/users/{objectId}/getMemberGroups
- "Is a user or group a member of a specific group?" -> POST /{tenantID}/isMemberOf
- "How do I rotate credentials on a service principal?" -> PATCH /{tenantID}/servicePrincipals/{objectId}/passwordCredentials
- "Find a service principal by its application ID" -> GET /{tenantID}/servicePrincipalsByAppId/{applicationID}/objectId
- "Who owns this application?" -> GET /{tenantID}/applications/{applicationObjectId}/owners
- "How do I grant delegated permissions (OAuth2)?" -> POST /{tenantID}/oauth2PermissionGrants
- "What app role assignments does a service principal have?" -> GET /{tenantID}/servicePrincipals/{objectId}/appRoleAssignments
- "How do I add a member to a group?" -> POST /{tenantID}/groups/{groupObjectId}/$links/members
- "List all verified domains for this tenant" -> GET /{tenantID}/domains
- "How do I permanently delete a soft-deleted application?" -> DELETE /{tenantID}/deletedApplications/{applicationObjectId}

## Response Tips

- **Listing endpoints** (applications, groups, users, servicePrincipals): Responses use `odata.nextLink` for pagination -- follow the URL until absent. Filter with `$filter` (OData syntax). Users endpoint also supports `$top` and `$expand`.
- **Mutation endpoints** (POST create, PATCH update, DELETE): 201 means created (body contains the new object), 204 means success with no body -- do not attempt to parse a response on 204.
- **Credential endpoints** (keyCredentials, passwordCredentials): PATCH replaces the entire credential collection -- always GET first, merge, then PATCH to avoid wiping existing credentials.
- **Link endpoints** ($links/owners, $links/members): These manage navigation property references, not the objects themselves. POST expects a body with an `odata.id` URL pointing to the target directory object.
- **isMemberOf / getMemberGroups**: These are POST actions that return membership results in the body (not 204). `getMemberGroups` accepts a `securityEnabledOnly` boolean in the parameters map.

## Anomaly Flags

- **Credential overwrites**: Alert when PATCH is called on keyCredentials or passwordCredentials without a preceding GET -- this silently replaces all existing credentials.
- **Orphaned service principals**: Flag service principals with no owners (GET owners returns empty) as they cannot be self-managed.
- **Soft-delete window**: Surface when deletedApplications are listed -- these have a 30-day recovery window before permanent removal. Hard DELETE is irreversible.
- **OAuth2 permission grants without constraints**: Flag POST to oauth2PermissionGrants where scope is overly broad (e.g., blanket consent grants).
- **Missing api-version**: All calls require the `api-version` query parameter (common field). Flag requests that omit it -- the API will return 400 or use an unpredictable default.
- **Rate limiting (429 responses)**: Azure AD Graph throttles aggressively. Surface retry-after headers and recommend exponential backoff.
- **Deprecation notice**: Azure AD Graph API (graph.windows.net) is deprecated in favor of Microsoft Graph (graph.microsoft.com). Flag this to users and recommend migration planning.

## Playbook

### 1. Register an Application and Configure Credentials

1. POST /{tenantID}/applications with `displayName`, `homepage`, and `identifierUris` in the parameters map
2. Note the `objectId` from the 201 response
3. PATCH /{tenantID}/applications/{objectId}/keyCredentials to add a certificate credential (provide the full credential array)
4. PATCH /{tenantID}/applications/{objectId}/passwordCredentials to add a client secret
5. POST /{tenantID}/applications/{objectId}/$links/owners to assign an owner for ongoing management

### 2. Create a Group and Populate Members

1. POST /{tenantID}/groups with `displayName`, `mailEnabled`, `mailNickname`, and `securityEnabled`
2. Capture the group `objectId` from the 201 response
3. For each member, POST /{tenantID}/groups/{groupObjectId}/$links/members with the member's directory object URL as `odata.id`
4. POST /{tenantID}/groups/{groupObjectId}/$links/owners to assign a group owner
5. Verify with GET /{tenantID}/groups/{objectId}/members

### 3. Audit and Rotate Service Principal Credentials

1. GET /{tenantID}/servicePrincipals with `$filter=displayName eq 'MyApp'` to find the target
2. GET /{tenantID}/servicePrincipals/{objectId}/keyCredentials to list current certificates
3. GET /{tenantID}/servicePrincipals/{objectId}/passwordCredentials to list current secrets
4. Build a new credential array: add the new credential, set expiry on old ones
5. PATCH the respective credentials endpoint with the full updated array
6. Verify by GET-ing the credentials again and confirming the old credential is absent or expired

### 4. Check User Group Membership and Permissions

1. GET /{tenantID}/users/{upnOrObjectId} to confirm the user exists and get their objectId
2. POST /{tenantID}/users/{objectId}/getMemberGroups with `{ "securityEnabledOnly": false }` to get all group memberships
3. For a specific group check, POST /{tenantID}/isMemberOf with `{ "groupId": "...", "memberId": "..." }`
4. GET /{tenantID}/groups/{objectId} on any returned group IDs to retrieve group details

### 5. Restore a Deleted Application

1. GET /{tenantID}/deletedApplications to list recoverable applications (optionally filter with `$filter`)
2. Identify the target application's `objectId`
3. POST /{tenantID}/deletedApplications/{objectId}/restore to recover it
4. GET /{tenantID}/applications/{objectId} to confirm the restoration succeeded
5. Review owners and credentials -- restoration may not preserve all linked objects


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
