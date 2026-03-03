---
name: blueprintclient
description: "BlueprintClient API skill. Use when working with BlueprintClient for {resourceScope}. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# BlueprintClient
API version: 2018-11-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments -- verify access
3. POST /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName}/whoIsBlueprint -- create first whoIsBlueprint

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### {resourceScope}
| Method | Path | Description |
|--------|------|-------------|
| PUT | /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName} | Create or update a blueprint assignment. |
| GET | /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName} | Get a blueprint assignment. |
| DELETE | /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName} | Delete a blueprint assignment. |
| POST | /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName}/whoIsBlueprint | Get Blueprints service SPN objectId |
| GET | /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments | List blueprint assignments within a subscription or a management group. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new blueprint assignment?" -> PUT /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName}
- "How do I update an existing blueprint assignment?" -> PUT /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName}
- "What blueprint assignments exist in my subscription?" -> GET /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments
- "How do I get details of a specific blueprint assignment?" -> GET /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName}
- "How do I delete a blueprint assignment?" -> DELETE /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName}
- "How do I delete a blueprint assignment and all its managed resources?" -> DELETE /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName} (with `deleteBehavior` parameter)
- "Which managed identity is used by a blueprint assignment?" -> POST /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName}/whoIsBlueprint
- "How do I assign a blueprint to a management group?" -> PUT /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName} (resourceScope = management group ID)
- "How do I list all blueprint assignments at subscription scope?" -> GET /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments (resourceScope = subscriptions/{subId})
- "How do I check if a blueprint assignment already exists before creating one?" -> GET /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName} (check for 200 vs 404)
- "How do I replace the parameters on an existing blueprint assignment?" -> PUT /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName} (full replace with updated assignment body)
- "How do I find the service principal behind a blueprint deployment?" -> POST /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName}/whoIsBlueprint

## Response Tips

- **PUT (create/update):** Returns 201 on success. The response body contains the full assignment object including provisioning state -- check `properties.provisioningState` for deployment progress.
- **GET (single):** Returns 200 with the assignment object. A 404 means the assignment does not exist at that scope.
- **GET (list):** Returns 200 with a paginated array. Look for `nextLink` in the response to fetch additional pages.
- **DELETE:** Returns 202 (accepted, deletion in progress) or 204 (already gone). 202 includes a `Location` header for polling the long-running operation.
- **whoIsBlueprint POST:** Returns 200 with the managed identity (service principal) details tied to the assignment.

## Anomaly Flags

- **202 on DELETE without polling:** Deletion is async. Surface a reminder to poll the operation status via the `Location` header until completion.
- **provisioningState stuck:** After PUT, if subsequent GETs show `provisioningState` is `failed` or remains non-terminal for an extended period, flag it immediately.
- **deleteBehavior omitted on DELETE:** If the user deletes an assignment without specifying `deleteBehavior`, warn that managed resources may be orphaned depending on the blueprint definition.
- **Scope mismatch:** If `resourceScope` does not match expected patterns (`subscriptions/{id}` or `providers/Microsoft.Management/managementGroups/{id}`), flag a likely malformed request before sending.
- **api-version drift:** This spec targets `2018-11-01-preview`. If the user references GA endpoints or newer preview versions, surface a version mismatch warning.
- **404 on GET after PUT 201:** If a newly created assignment returns 404 on immediate GET, flag likely eventual consistency delay.

## Playbook

### 1. Assign a Blueprint to a Subscription

1. Set `resourceScope` to `subscriptions/{subscriptionId}`
2. Choose an `assignmentName` (unique within scope)
3. Build the `assignment` body with blueprint ID, parameters, resource groups, and managed identity config
4. Call PUT `/{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName}` with `api-version=2018-11-01-preview`
5. Confirm 201 response, then poll GET on the same path until `provisioningState` reaches `succeeded` or `failed`

### 2. Audit All Blueprint Assignments in a Scope

1. Set `resourceScope` to the target subscription or management group
2. Call GET `/{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments` with `api-version=2018-11-01-preview`
3. Iterate through the `value` array in the response
4. If `nextLink` is present, follow it to retrieve additional pages
5. For each assignment, inspect `properties.provisioningState` and `properties.blueprintId` to catalog what is deployed

### 3. Investigate the Managed Identity Behind an Assignment

1. Identify the `assignmentName` and `resourceScope`
2. Call POST `/{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName}/whoIsBlueprint`
3. Extract the service principal object ID from the response
4. Use the object ID to audit role assignments or Activity Log entries in Azure AD / IAM

### 4. Safely Remove a Blueprint Assignment and Its Resources

1. Call GET on the assignment to confirm it exists and review its current state
2. Call DELETE `/{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName}` with `deleteBehavior=all` to remove managed resources
3. Capture the `Location` header from the 202 response
4. Poll the operation URL until it returns a terminal status
5. Verify with a final GET (expect 404) to confirm full removal

### 5. Update Blueprint Assignment Parameters

1. Call GET on the existing assignment to retrieve the current `assignment` body
2. Modify the desired fields (parameters, resource groups, lock mode) in the retrieved body
3. Call PUT with the full updated `assignment` body to the same path
4. Confirm 201 response and monitor `provisioningState` via GET until the update completes


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
