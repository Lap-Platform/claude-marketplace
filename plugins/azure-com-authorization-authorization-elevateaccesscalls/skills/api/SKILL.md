---
name: authorizationmanagementclient
description: "AuthorizationManagementClient API skill. Use when working with AuthorizationManagementClient for providers. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# AuthorizationManagementClient
API version: 2015-07-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
3. POST /providers/Microsoft.Authorization/elevateAccess -- create first elevateAccess

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| POST | /providers/Microsoft.Authorization/elevateAccess | Elevates access for a Global Administrator. |

## Enhanced Skill Content
## Question Mapping

- "How do I elevate my access to manage all Azure subscriptions?" -> POST /providers/Microsoft.Authorization/elevateAccess
- "How do I get tenant-wide access as User Access Administrator?" -> POST /providers/Microsoft.Authorization/elevateAccess
- "How can I grant myself root scope permissions in Azure?" -> POST /providers/Microsoft.Authorization/elevateAccess
- "How do I enable Global Administrator to manage all subscriptions?" -> POST /providers/Microsoft.Authorization/elevateAccess
- "What endpoint do I call to elevate to tenant root group?" -> POST /providers/Microsoft.Authorization/elevateAccess
- "How do I get permissions to assign roles across all subscriptions?" -> POST /providers/Microsoft.Authorization/elevateAccess
- "How can I recover access to orphaned Azure subscriptions?" -> POST /providers/Microsoft.Authorization/elevateAccess
- "What API call makes me User Access Administrator at root scope?" -> POST /providers/Microsoft.Authorization/elevateAccess
- "How do I bootstrap RBAC management for a new tenant?" -> POST /providers/Microsoft.Authorization/elevateAccess
- "How do I regain control of subscriptions after losing admin access?" -> POST /providers/Microsoft.Authorization/elevateAccess
- "Can I elevate access temporarily to audit role assignments?" -> POST /providers/Microsoft.Authorization/elevateAccess (then manually remove the role after)
- "How do I troubleshoot 'no subscriptions found' for a Global Admin?" -> POST /providers/Microsoft.Authorization/elevateAccess

## Response Tips

- **elevateAccess (200)**: Empty response body on success. A 200 confirms the caller now has User Access Administrator at root scope (`/`). No payload to parse -- success is the status code itself. Errors return standard Azure error JSON with `code` and `message` fields.

## Anomaly Flags

- **403 Forbidden**: Caller is not a Global Administrator in Azure AD. This endpoint requires the Global Admin directory role -- no other role works.
- **401 Unauthorized**: OAuth2 token is expired, missing, or issued for the wrong tenant. Verify the token audience is `https://management.azure.com`.
- **409 Conflict**: Elevation may already be active. Check existing role assignments at root scope before retrying.
- **Lingering elevation**: This grants persistent access until explicitly removed. Agents should warn if elevation was performed but never revoked, as it violates least-privilege.
- **429 Too Many Requests**: Azure Resource Manager throttling. Back off and retry with the `Retry-After` header value.
- **Deprecated API version**: The spec uses `2015-07-01`. Surface a note if Azure documentation references a newer stable version.

## Playbook

### 1. Elevate and Audit All Subscription Role Assignments

1. Authenticate as a Global Administrator and obtain an OAuth2 token for `https://management.azure.com`.
2. Call `POST /providers/Microsoft.Authorization/elevateAccess` with `api-version=2015-07-01`.
3. Confirm 200 response.
4. List all subscriptions: `GET /subscriptions?api-version=2020-01-01`.
5. For each subscription, list role assignments: `GET /subscriptions/{id}/providers/Microsoft.Authorization/roleAssignments?api-version=2022-04-01`.
6. Export results, then remove your root-scope role assignment to restore least-privilege.

### 2. Recover Access to an Orphaned Subscription

1. Authenticate as Global Administrator.
2. Call `POST /providers/Microsoft.Authorization/elevateAccess`.
3. Navigate to the orphaned subscription and assign yourself Owner or Contributor: `PUT /subscriptions/{id}/providers/Microsoft.Authorization/roleAssignments/{assignmentId}?api-version=2022-04-01`.
4. Verify access by listing resources in the subscription.
5. Remove the root-scope User Access Administrator role assignment.

### 3. Bootstrap Tenant-Wide RBAC Governance

1. Elevate access via `POST /providers/Microsoft.Authorization/elevateAccess`.
2. Create a custom role definition at root scope with limited permissions for your governance team.
3. Assign the custom role to a security group at the management group or root scope.
4. Apply Azure Policy assignments at root scope for RBAC guardrails.
5. Remove your own elevation immediately after setup is complete.

### 4. Emergency Elevation with Immediate Revocation

1. Call `POST /providers/Microsoft.Authorization/elevateAccess` and note the exact timestamp.
2. Perform the required administrative action (role fix, policy update, etc.).
3. List your role assignments at root scope: `GET /providers/Microsoft.Authorization/roleAssignments?$filter=atScope()&api-version=2022-04-01`.
4. Identify the User Access Administrator assignment and delete it: `DELETE /providers/Microsoft.Authorization/roleAssignments/{id}?api-version=2022-04-01`.
5. Confirm removal succeeded with a follow-up GET. Log the elevation window duration for audit trail.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
