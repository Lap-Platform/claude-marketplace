---
name: automationmanagement
description: "AutomationManagement API skill. Use when working with AutomationManagement for subscriptions. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# AutomationManagement
API version: 2015-10-31

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/schedules -- verify access

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/schedules/{scheduleName} | Create a schedule. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/schedules/{scheduleName} | Update the schedule identified by schedule name. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/schedules/{scheduleName} | Retrieve the schedule identified by schedule name. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/schedules/{scheduleName} | Delete the schedule identified by schedule name. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/schedules | Retrieve a list of schedules. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new automation schedule?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/schedules/{scheduleName}
- "How do I update an existing schedule's properties?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/schedules/{scheduleName}
- "How do I replace a schedule entirely?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/schedules/{scheduleName}
- "How do I get details of a specific schedule?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/schedules/{scheduleName}
- "How do I list all schedules in an automation account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/schedules
- "How do I delete a schedule?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/schedules/{scheduleName}
- "How do I check if a schedule already exists before creating it?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/schedules/{scheduleName}
- "How do I change just the description of a schedule without replacing it?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/schedules/{scheduleName}
- "How do I see all schedules across my automation account?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/schedules
- "How do I disable a schedule without deleting it?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/schedules/{scheduleName}
- "What happens if I create a schedule with a name that already exists?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/schedules/{scheduleName}
- "How do I recreate a schedule that was deleted?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/schedules/{scheduleName}

## Response Tips

- **PUT (create/update)**: 201 means created new, 200 means updated existing; 409 means a naming conflict exists -- check for duplicate schedule names or a schedule in a terminal state that blocks reuse.
- **PATCH (partial update)**: 200 returns the full updated schedule object; send only the fields you want to change in the request body.
- **GET (single)**: 200 returns the full schedule resource including properties like frequency, interval, start time, expiry, and enabled state; a 404 means the schedule name is wrong or was deleted.
- **GET (list)**: 200 returns an array of schedule objects; watch for `nextLink` pagination if the automation account has many schedules -- follow it until null.
- **DELETE**: 200 confirms deletion; the operation is idempotent so deleting a nonexistent schedule may still return 200.

## Anomaly Flags

- **409 Conflict on PUT**: Surface immediately -- the schedule name collides with an existing or expired schedule that cannot be overwritten. The user may need to delete the old one first or choose a different name.
- **Expired or disabled schedules**: When listing or fetching schedules, flag any with an expiry date in the past or an `isEnabled: false` state, as these will not trigger runbooks.
- **Missing required `parameters` body on PUT/PATCH**: Both mutating endpoints require a `parameters` object. A 400 response likely means the request body was malformed or missing required fields like `startTime` or `frequency`.
- **Pagination truncation**: If the list endpoint returns a `nextLink` and the caller stops after the first page, flag that results are incomplete.
- **OAuth2 token expiry**: All endpoints require OAuth2. Surface 401 responses as token refresh needed rather than a permissions issue.

## Playbook

### 1. Create a New Recurring Schedule

1. Call GET on the specific schedule name to verify it does not already exist (expect 404).
2. Call PUT with the schedule name and a `parameters` body containing `startTime`, `frequency` (e.g., Hour, Day, Week), `interval`, and `isEnabled: true`.
3. Confirm a 201 response indicating the schedule was created.
4. Call GET on the schedule name to verify all properties were applied correctly.

### 2. Safely Update a Schedule Property

1. Call GET on the schedule name to retrieve the current configuration.
2. Identify the field to change (e.g., `description`, `isEnabled`, `expiryTime`).
3. Call PATCH with only the changed fields in the `parameters` body.
4. Confirm a 200 response and verify the returned object reflects the update.

### 3. Audit and Clean Up Stale Schedules

1. Call GET (list) to retrieve all schedules in the automation account. Follow `nextLink` if paginated.
2. Filter results for schedules where `isEnabled` is false or `expiryTime` is in the past.
3. For each stale schedule, decide whether to DELETE or re-enable via PATCH.
4. Call DELETE for each schedule to be removed, confirming 200 for each.
5. Re-list schedules to verify cleanup is complete.

### 4. Replace a Schedule with New Settings

1. Call GET on the schedule to capture current settings for reference.
2. Call PUT with the same schedule name but a completely new `parameters` body (new frequency, interval, start time, etc.).
3. If you receive 409, call DELETE first to remove the conflicting schedule, then retry the PUT.
4. Confirm 200 (updated) or 201 (recreated) and verify via a follow-up GET.

### 5. Disable and Re-enable a Schedule

1. Call GET on the schedule name to confirm it exists and check its current `isEnabled` state.
2. Call PATCH with `parameters` containing `isEnabled: false` to disable it.
3. Confirm the 200 response shows `isEnabled: false`.
4. When ready to re-enable, call PATCH with `isEnabled: true`.
5. Call GET to verify the schedule is active and the next run time is correctly calculated.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
