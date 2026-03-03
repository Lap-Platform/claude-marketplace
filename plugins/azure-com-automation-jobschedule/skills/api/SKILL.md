---
name: automationmanagement
description: "AutomationManagement API skill. Use when working with AutomationManagement for subscriptions. Covers 4 endpoints."
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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/jobSchedules -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/jobSchedules/{jobScheduleId} | Delete the job schedule identified by job schedule name. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/jobSchedules/{jobScheduleId} | Retrieve the job schedule identified by job schedule name. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/jobSchedules/{jobScheduleId} | Create a job schedule. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/jobSchedules | Retrieve a list of job schedules. |

## Enhanced Skill Content
## Question Mapping

- "How do I link a runbook to a schedule?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/jobSchedules/{jobScheduleId}
- "How do I remove a runbook from a schedule?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/jobSchedules/{jobScheduleId}
- "What schedule is assigned to a specific job?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/jobSchedules/{jobScheduleId}
- "List all job schedules in my automation account" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/jobSchedules
- "Which runbooks are scheduled to run?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/jobSchedules
- "How do I filter job schedules by a specific runbook?" -> GET ...jobSchedules?$filter={expression}
- "Does a particular job schedule exist?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Automation/automationAccounts/{automationAccountName}/jobSchedules/{jobScheduleId}
- "How do I replace a job schedule association?" -> DELETE then PUT on the same jobScheduleId
- "How do I create a new job schedule with parameters?" -> PUT ...jobSchedules/{jobScheduleId} with parameters body including runbook, schedule, and runOn properties
- "How do I clean up all job schedules for an automation account?" -> GET ...jobSchedules then DELETE each returned jobScheduleId
- "What GUID do I use for a new job schedule?" -> Generate a new UUID/GUID client-side and pass it as jobScheduleId in PUT
- "How do I verify a job schedule was deleted?" -> GET the same jobScheduleId after DELETE and expect a 404

## Response Tips

- **Single job schedule (GET by ID):** Response contains `properties` with `schedule`, `runbook`, `runOn`, and `parameters` nested objects -- always check `properties.schedule.name` and `properties.runbook.name` for the association details.
- **List job schedules (GET all):** Response includes a `value` array and may include `nextLink` for pagination -- follow `nextLink` URLs until absent to retrieve all results.
- **Create (PUT):** Returns 201 on success with the created resource; a 409 indicates a conflicting schedule association already exists for that GUID.
- **Delete (DELETE):** Returns 200 on success with no body; a 404 means the job schedule was already removed or never existed.
- **Errors:** Azure returns a standard `error` object with `code` and `message` fields -- surface the `message` value directly to the user.

## Anomaly Flags

- **404 on GET/DELETE:** The job schedule GUID does not exist -- confirm the jobScheduleId and automation account name are correct before retrying.
- **409 on PUT:** A job schedule with that GUID already exists -- generate a new GUID or delete the existing one first.
- **Throttling (429):** Azure Resource Manager enforces rate limits per subscription -- if received, back off and retry using the `Retry-After` header value.
- **Empty `value` array on list:** The automation account has no job schedules -- verify the account name and resource group are correct, or check if schedules were recently purged.
- **Missing `nextLink` on large accounts:** If you expect many job schedules but receive fewer than ~100, confirm `$filter` is not unintentionally limiting results.
- **Deprecated API version:** This spec targets `2015-10-31` -- surface a warning if Azure documentation recommends a newer api-version for Automation.

## Playbook

### 1. Schedule a Runbook to Run on a Recurring Schedule

1. Identify the target automation account, resource group, and subscription ID.
2. Look up the runbook name and schedule name you want to associate.
3. Generate a new GUID to use as the `jobScheduleId`.
4. Call PUT on `/jobSchedules/{newGUID}` with a body containing `properties.schedule.name`, `properties.runbook.name`, and optionally `properties.parameters` and `properties.runOn`.
5. Confirm the 201 response and note the returned job schedule ID.

### 2. List and Filter Active Job Schedules

1. Call GET on `/jobSchedules` with no filter to retrieve all associations.
2. If looking for a specific runbook, add `$filter=properties/runbook/name eq 'MyRunbook'`.
3. Iterate through the `value` array in the response.
4. Follow any `nextLink` URLs to paginate through remaining results.
5. Extract `properties.schedule.name` and `properties.runbook.name` from each entry to build a summary table.

### 3. Remove a Runbook-Schedule Association

1. If you know the `jobScheduleId`, call DELETE directly on that ID.
2. If you only know the runbook or schedule name, first list all job schedules (GET all) and filter locally.
3. Match the entry by `properties.runbook.name` or `properties.schedule.name`.
4. Call DELETE on the matching `jobScheduleId`.
5. Optionally call GET on the same ID to confirm it returns 404.

### 4. Replace a Job Schedule with Updated Parameters

1. Call GET on the existing `jobScheduleId` to retrieve current properties.
2. Call DELETE on that `jobScheduleId` to remove the old association.
3. Call PUT with the same or a new `jobScheduleId`, supplying updated `properties.parameters` or a different `properties.runOn` target.
4. Verify the 201 response contains the updated configuration.

### 5. Audit All Scheduled Runbooks Across an Account

1. Call GET on `/jobSchedules` to list every association.
2. Paginate through all `nextLink` pages to collect the complete set.
3. Group results by `properties.runbook.name` to see which runbooks have schedules.
4. Flag any runbooks with multiple schedule associations for review.
5. Cross-reference with known schedule frequencies to identify overlapping or redundant runs.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
