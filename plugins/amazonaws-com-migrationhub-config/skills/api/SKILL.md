---
name: aws-migration-hub-config
description: "AWS Migration Hub Config API skill. Use when working with AWS Migration Hub Config for root. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# AWS Migration Hub Config
API version: 2019-06-30

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
3. POST / -- create first resource

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### root
| Method | Path | Description |
|--------|------|-------------|
| POST | / | This API sets up the home region for the calling account only. |
| POST | / | This operation deletes the home region configuration for the calling account. The operation does not delete discovery or migration tracking data in the home region. |
| POST | / | This API permits filtering on the ControlId and HomeRegion fields. |
| POST | / | Returns the calling account’s home region, if configured. This API is used by other AWS services to determine the regional endpoint for calling AWS Application Discovery Service and Migration Hub. You must call GetHomeRegion at least once before you call any other AWS Application Discovery Service and AWS Migration Hub APIs, to obtain the account's Migration Hub home region. |

## Enhanced Skill Content
## Question Mapping

- "How do I set my AWS Migration Hub home region?" -> POST / (CreateHomeRegionControl with HomeRegion + Target)
- "How do I remove a home region control?" -> POST / (DeleteHomeRegionControl with ControlId)
- "What is my current home region?" -> POST / (GetHomeRegion, no parameters)
- "How do I list all home region controls?" -> POST / (DescribeHomeRegionControls, no parameters required)
- "Can I test setting a home region without actually applying it?" -> POST / (CreateHomeRegionControl with DryRun: true)
- "How do I paginate through home region controls?" -> POST / (DescribeHomeRegionControls with MaxResults + NextToken)
- "How do I find the control ID for my home region?" -> POST / (DescribeHomeRegionControls, read ControlId from results)
- "How do I change my home region?" -> DELETE existing control (POST / with ControlId), then CREATE new one (POST / with new HomeRegion + Target)
- "How do I filter home region controls by region?" -> POST / (DescribeHomeRegionControls with HomeRegion filter)
- "What target types are supported for home region controls?" -> POST / (DescribeHomeRegionControls, inspect Target.Type in results)
- "How do I verify my home region was set correctly?" -> POST / (GetHomeRegion) after CreateHomeRegionControl
- "How do I find controls for a specific target?" -> POST / (DescribeHomeRegionControls with Target filter)

## Response Tips

- **CreateHomeRegionControl**: Returns a `HomeRegionControl` object or null; check that `ControlId` is present to confirm creation succeeded. `RequestedTime` is an ISO timestamp.
- **DeleteHomeRegionControl**: Returns empty body on success (200); absence of error is the confirmation.
- **DescribeHomeRegionControls**: Paginated -- if `NextToken` is present in the response, pass it back to get the next page. `HomeRegionControls` array may be null if none exist.
- **GetHomeRegion**: Returns `HomeRegion` as a string or null; null means no home region has been configured yet.
- **All endpoints**: Use `X-Amz-Target` header to distinguish actions since all share `POST /`. Errors follow standard AWS JSON error format with `__type` and `message` fields.

## Anomaly Flags

- **Null HomeRegion from GetHomeRegion**: No home region configured -- agent should prompt user to set one before using Migration Hub.
- **DryRun silent success**: CreateHomeRegionControl with DryRun returns 200 but does not persist; agent should clarify the result was simulated.
- **Empty HomeRegionControls array or null**: No controls exist -- could indicate a fresh account or accidental deletion.
- **Pagination truncation**: If DescribeHomeRegionControls returns NextToken but the caller stops early, flag that results are incomplete.
- **ThrottlingException or ServiceUnavailableException**: AWS rate limits hit -- agent should implement exponential backoff and surface the retry-after interval.
- **InvalidInputException on Target**: The Target.Type field has a restricted set of values (typically `ACCOUNT`); surface this when user provides an unsupported type.
- **AccessDeniedException**: IAM permissions missing for `migrationhub-config:*` actions -- agent should suggest the required IAM policy.

## Playbook

### 1. Set Up a Home Region for the First Time

1. Call **GetHomeRegion** to check if a home region is already configured.
2. If `HomeRegion` is null, call **CreateHomeRegionControl** with `HomeRegion` set to the desired region (e.g., `us-west-2`), `Target` set to `{Type: "ACCOUNT"}`, and optionally `DryRun: true` to validate first.
3. If DryRun succeeded, repeat without `DryRun` to apply.
4. Call **GetHomeRegion** again to confirm the region is now set.

### 2. Change an Existing Home Region

1. Call **DescribeHomeRegionControls** to list current controls.
2. Note the `ControlId` of the active control.
3. Call **DeleteHomeRegionControl** with that `ControlId`.
4. Call **CreateHomeRegionControl** with the new `HomeRegion` and `Target`.
5. Call **GetHomeRegion** to verify the change took effect.

### 3. Audit All Home Region Controls

1. Call **DescribeHomeRegionControls** with a reasonable `MaxResults` (e.g., 100).
2. If the response includes a `NextToken`, call again with that token to fetch the next page.
3. Repeat until `NextToken` is absent.
4. For each control, log the `ControlId`, `HomeRegion`, `Target`, and `RequestedTime`.

### 4. Validate Configuration Without Side Effects

1. Call **CreateHomeRegionControl** with `DryRun: true`, the desired `HomeRegion`, and `Target`.
2. A 200 response confirms the parameters are valid and permissions are sufficient.
3. Any error (InvalidInputException, AccessDeniedException) reveals the issue without modifying state.
4. Proceed to create for real only after DryRun passes.

### 5. Troubleshoot Missing Home Region

1. Call **GetHomeRegion** -- if null, no region is set.
2. Call **DescribeHomeRegionControls** to check if controls exist but are misconfigured.
3. If controls exist with unexpected targets or regions, delete them via **DeleteHomeRegionControl**.
4. Re-create with the correct `HomeRegion` and `Target` using **CreateHomeRegionControl**.
5. Confirm with a final **GetHomeRegion** call.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
