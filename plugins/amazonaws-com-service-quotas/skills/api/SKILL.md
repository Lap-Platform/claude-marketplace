---
name: service-quotas
description: "Service Quotas API skill. Use when working with Service Quotas for root. Covers 19 endpoints."
version: 1.0.0
generator: lapsh
---

# Service Quotas
API version: 2019-06-24

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
3. POST / -- create first resource

## Endpoints

19 endpoints across 1 groups. See references/api-spec.lap for full details.

### root
| Method | Path | Description |
|--------|------|-------------|
| POST | / | Associates your quota request template with your organization. When a new Amazon Web Services account is created in your organization, the quota increase requests in the template are automatically applied to the account. You can add a quota increase request for any adjustable quota to your template. |
| POST | / | Deletes the quota increase request for the specified quota from your quota request template. |
| POST | / | Disables your quota request template. After a template is disabled, the quota increase requests in the template are not applied to new Amazon Web Services accounts in your organization. Disabling a quota request template does not apply its quota increase requests. |
| POST | / | Retrieves the default value for the specified quota. The default value does not reflect any quota increases. |
| POST | / | Retrieves the status of the association for the quota request template. |
| POST | / | Retrieves information about the specified quota increase request. |
| POST | / | Retrieves the applied quota value for the specified quota. For some quotas, only the default values are available. If the applied quota value is not available for a quota, the quota is not retrieved. |
| POST | / | Retrieves information about the specified quota increase request in your quota request template. |
| POST | / | Lists the default values for the quotas for the specified Amazon Web Service. A default value does not reflect any quota increases. |
| POST | / | Retrieves the quota increase requests for the specified Amazon Web Service. |
| POST | / | Retrieves the quota increase requests for the specified quota. |
| POST | / | Lists the quota increase requests in the specified quota request template. |
| POST | / | Lists the applied quota values for the specified Amazon Web Service. For some quotas, only the default values are available. If the applied quota value is not available for a quota, the quota is not retrieved. |
| POST | / | Lists the names and codes for the Amazon Web Services integrated with Service Quotas. |
| POST | / | Returns a list of the tags assigned to the specified applied quota. |
| POST | / | Adds a quota increase request to your quota request template. |
| POST | / | Submits a quota increase request for the specified quota. |
| POST | / | Adds tags to the specified applied quota. You can include one or more tags to add to the quota. |
| POST | / | Removes tags from the specified applied quota. You can specify one or more tags to remove. |

## Enhanced Skill Content
## Question Mapping

- "What AWS services support quotas?" -> POST / (ListServices)
- "What are the current quotas for a specific service?" -> POST / (ListServiceQuotas: ServiceCode required)
- "What is the default quota value for a specific quota?" -> POST / (GetAWSDefaultServiceQuota: ServiceCode + QuotaCode required)
- "What is my current applied quota for a service?" -> POST / (GetServiceQuota: ServiceCode + QuotaCode required, optional ContextId)
- "How do I request a quota increase?" -> POST / (RequestServiceQuotaIncrease: ServiceCode + QuotaCode + DesiredValue required)
- "What is the status of my quota increase request?" -> POST / (GetRequestedServiceQuotaChange: RequestId required)
- "Show me all pending quota increase requests" -> POST / (ListRequestedServiceQuotaChangeHistory: filter by Status=PENDING)
- "What quota change requests exist for a specific quota?" -> POST / (ListRequestedServiceQuotaChangeHistoryByQuota: ServiceCode + QuotaCode required)
- "How do I set up automatic quota increases via template?" -> POST / (PutServiceQuotaIncreaseRequestInTemplate: QuotaCode + ServiceCode + AwsRegion + DesiredValue)
- "Is the quota request template associated with my organization?" -> POST / (GetAssociationForServiceQuotaTemplate)
- "How do I enable the organization-wide quota template?" -> POST / (AssociateServiceQuotaTemplate)
- "How do I remove a quota from the increase template?" -> POST / (DeleteServiceQuotaIncreaseRequestFromTemplate: ServiceCode + QuotaCode + AwsRegion)
- "What tags are on a quota resource?" -> POST / (ListTagsForResource: ResourceARN required)
- "Is this quota adjustable?" -> POST / (GetServiceQuota: check Adjustable field in response)

## Response Tips

- **Quota objects**: `Value` is float64 -- compare with `DesiredValue` to see headroom. Check `Adjustable: true` before requesting an increase; `Unit` tells you the measurement (Count, Megabits, etc.).
- **Pagination**: All List endpoints return `NextToken`. Pass it back with the same params to get the next page. `MaxResults` caps page size. Absence of `NextToken` in response means last page.
- **Change requests**: `Status` field cycles through PENDING -> CASE_OPENED -> APPROVED/DENIED/NOT_APPROVED. `CaseId` links to the AWS Support case. `Created`/`LastUpdated` are timestamps.
- **Template responses**: Template items are region-specific (`AwsRegion` field). `GlobalQuota: true` means the quota applies across all regions regardless.
- **Error objects**: Quota responses may include nested `ErrorReason` with `ErrorCode` and `ErrorMessage` -- always check this even on 200 responses.
- **Tags**: Returned as `[Tag]` array. `TagResource` and `UntagResource` return empty 200 on success.

## Anomaly Flags

- **Non-adjustable quota approaching limit**: Surface when `GetServiceQuota` returns `Adjustable: false` and current usage is near `Value` -- the user cannot request an increase and must redesign.
- **Stale pending requests**: Flag `RequestedServiceQuotaChange` entries where `Status` is PENDING and `Created` is older than 7 days -- these may need follow-up via AWS Support.
- **ErrorReason present on 200**: A successful response can still contain `ErrorReason` nested inside the Quota object -- always surface `ErrorCode`/`ErrorMessage` if populated.
- **Template not associated**: If `GetAssociationForServiceQuotaTemplate` returns `DISASSOCIATED`, warn that PutServiceQuotaIncreaseRequestInTemplate entries will have no effect until the template is associated.
- **Global vs regional mismatch**: Flag when a user tries to set a template entry for a region-specific quota that is actually `GlobalQuota: true`, or vice versa.
- **Denied requests**: Proactively surface any `Status: DENIED` or `NOT_APPROVED` from ListRequestedServiceQuotaChangeHistory so users do not assume their increase went through.

## Playbook

### 1. Request a Quota Increase

1. Call **ListServices** to find the target `ServiceCode` (or use a known code like `ec2`).
2. Call **ListServiceQuotas** with the `ServiceCode` to browse available quotas and find the `QuotaCode`.
3. Call **GetServiceQuota** with `ServiceCode` + `QuotaCode` to check current value and confirm `Adjustable: true`.
4. Call **RequestServiceQuotaIncrease** with `ServiceCode`, `QuotaCode`, and desired `DesiredValue`.
5. Note the `RequestId` from the response.
6. Call **GetRequestedServiceQuotaChange** with the `RequestId` to monitor status over time.

### 2. Set Up Organization-Wide Quota Template

1. Call **GetAssociationForServiceQuotaTemplate** to check if the template is already associated.
2. If `DISASSOCIATED`, call **AssociateServiceQuotaTemplate** to enable it.
3. Call **PutServiceQuotaIncreaseRequestInTemplate** with `ServiceCode`, `QuotaCode`, `AwsRegion`, and `DesiredValue` for each quota you want auto-applied to new accounts.
4. Call **ListServiceQuotaIncreaseRequestsInTemplate** to verify all entries are present.

### 3. Audit Current Quotas vs Defaults

1. Call **ListServices** to get all available service codes.
2. For each service, call **ListServiceQuotas** (applied values) and **ListAWSDefaultServiceQuotas** (default values).
3. Compare `Value` fields between applied and default quotas -- differences indicate previously granted increases.
4. Flag any quotas where `ErrorReason` is populated, as these may have data retrieval issues.

### 4. Review and Clean Up Quota Change Requests

1. Call **ListRequestedServiceQuotaChangeHistory** with no filters to see all requests.
2. Filter by `Status` (PENDING, CASE_OPENED, APPROVED, DENIED) to categorize.
3. For any DENIED requests, review `QuotaName` and `DesiredValue` to decide whether to refile with a lower value or different justification.
4. For APPROVED requests, call **GetServiceQuota** to confirm the new value is now applied.

### 5. Tag and Organize Quota Resources

1. Call **GetServiceQuota** to retrieve the `QuotaArn` for the target quota.
2. Call **ListTagsForResource** with the `QuotaArn` to see existing tags.
3. Call **TagResource** with the `ResourceARN` and a `Tags` array to add cost-center, team, or environment labels.
4. To remove stale tags, call **UntagResource** with the `ResourceARN` and `TagKeys` array of keys to delete.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
