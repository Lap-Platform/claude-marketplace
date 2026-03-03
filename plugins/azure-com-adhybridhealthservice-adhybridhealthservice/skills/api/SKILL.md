---
name: adhybridhealthservice
description: "ADHybridHealthService API skill. Use when working with ADHybridHealthService for providers. Covers 77 endpoints."
version: 1.0.0
generator: lapsh
---

# ADHybridHealthService
API version: 2014-01-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.ADHybridHealthService/addsservices -- verify access
3. POST /providers/Microsoft.ADHybridHealthService/addsservices -- create first addsservices

## Endpoints

77 endpoints across 1 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.ADHybridHealthService/addsservices | Gets the details of Active Directory Domain Service, for a tenant, that are onboarded to Azure Active Directory Connect Health. |
| POST | /providers/Microsoft.ADHybridHealthService/addsservices | Onboards a service for a given tenant in Azure Active Directory Connect Health. |
| GET | /providers/Microsoft.ADHybridHealthService/addsservices/{serviceName} | Gets the details of an Active Directory Domain Service for a tenant having Azure AD Premium license and is onboarded to Azure Active Directory Connect Health. |
| DELETE | /providers/Microsoft.ADHybridHealthService/addsservices/{serviceName} | Deletes an Active Directory Domain Service which is onboarded to Azure Active Directory Connect Health. |
| PATCH | /providers/Microsoft.ADHybridHealthService/addsservices/{serviceName} | Updates an Active Directory Domain Service properties of an onboarded service. |
| GET | /providers/Microsoft.ADHybridHealthService/addsservices/{serviceName}/alerts | Gets the alerts for a given Active Directory Domain Service. |
| GET | /providers/Microsoft.ADHybridHealthService/addsservices/{serviceName}/configuration | Gets the service configurations. |
| GET | /providers/Microsoft.ADHybridHealthService/addsservices/{serviceName}/dimensions/{dimension} | Gets the dimensions for a given dimension type in a server. |
| GET | /providers/Microsoft.ADHybridHealthService/addsservices/{serviceName}/addsservicemembers | Gets the details of the Active Directory Domain servers, for a given Active Directory Domain Service, that are onboarded to Azure Active Directory Connect Health. |
| GET | /providers/Microsoft.ADHybridHealthService/addsservices/{serviceName}/addomainservicemembers | Gets the details of the servers, for a given Active Directory Domain Service, that are onboarded to Azure Active Directory Connect Health. |
| GET | /providers/Microsoft.ADHybridHealthService/addsservices/{serviceName}/features/{featureName}/userpreference | Gets the user preferences for a given feature. |
| DELETE | /providers/Microsoft.ADHybridHealthService/addsservices/{serviceName}/features/{featureName}/userpreference | Deletes the user preferences for a given feature. |
| POST | /providers/Microsoft.ADHybridHealthService/addsservices/{serviceName}/features/{featureName}/userpreference | Adds the user preferences for a given feature. |
| GET | /providers/Microsoft.ADHybridHealthService/addsservices/{serviceName}/forestsummary | Gets the forest summary for a given Active Directory Domain Service, that is onboarded to Azure Active Directory Connect Health. |
| GET | /providers/Microsoft.ADHybridHealthService/addsservices/{serviceName}/metrics/{metricName}/groups/{groupName} | Gets the server related metrics for a given metric and group combination. |
| GET | /providers/Microsoft.ADHybridHealthService/addsservices/{serviceName}/metrics/{metricName}/groups/{groupName}/average | Gets the average of the metric values for a given metric and group combination. |
| GET | /providers/Microsoft.ADHybridHealthService/addsservices/{serviceName}/metrics/{metricName}/groups/{groupName}/sum | Gets the sum of the metric values for a given metric and group combination. |
| GET | /providers/Microsoft.ADHybridHealthService/addsservices/{serviceName}/metricmetadata | Gets the service related metrics information. |
| GET | /providers/Microsoft.ADHybridHealthService/addsservices/{serviceName}/metricmetadata/{metricName} | Gets the service related metric information. |
| GET | /providers/Microsoft.ADHybridHealthService/addsservices/{serviceName}/metricmetadata/{metricName}/groups/{groupName} | Gets the service related metrics for a given metric and group combination. |
| GET | /providers/Microsoft.ADHybridHealthService/addsservices/{serviceName}/replicationdetails | Gets complete domain controller list along with replication details for a given Active Directory Domain Service, that is onboarded to Azure Active Directory Connect Health. |
| GET | /providers/Microsoft.ADHybridHealthService/addsservices/{serviceName}/replicationstatus | Gets Replication status for a given Active Directory Domain Service, that is onboarded to Azure Active Directory Connect Health. |
| GET | /providers/Microsoft.ADHybridHealthService/addsservices/{serviceName}/replicationsummary | Gets complete domain controller list along with replication details for a given Active Directory Domain Service, that is onboarded to Azure Active Directory Connect Health. |
| GET | /providers/Microsoft.ADHybridHealthService/addsservices/{serviceName}/servicemembers | Gets the details of the servers, for a given Active Directory Domain Controller service, that are onboarded to Azure Active Directory Connect Health Service. |
| POST | /providers/Microsoft.ADHybridHealthService/addsservices/{serviceName}/servicemembers | Onboards  a server, for a given Active Directory Domain Controller service, to Azure Active Directory Connect Health Service. |
| GET | /providers/Microsoft.ADHybridHealthService/addsservices/{serviceName}/servicemembers/{serviceMemberId} | Gets the details of a server, for a given Active Directory Domain Controller service, that are onboarded to Azure Active Directory Connect Health Service. |
| DELETE | /providers/Microsoft.ADHybridHealthService/addsservices/{serviceName}/servicemembers/{serviceMemberId} | Deletes a Active Directory Domain Controller server that has been onboarded to Azure Active Directory Connect Health Service. |
| GET | /providers/Microsoft.ADHybridHealthService/addsservices/{serviceName}/servicemembers/{serviceMemberId}/alerts | Gets the details of an alert for a given Active Directory Domain Controller service and server combination. |
| GET | /providers/Microsoft.ADHybridHealthService/addsservices/{serviceName}/servicemembers/{serviceMemberId}/credentials | Gets the credentials of the server which is needed by the agent to connect to Azure Active Directory Connect Health Service. |
| GET | /providers/Microsoft.ADHybridHealthService/addsservices/premiumCheck | Gets the details of Active Directory Domain Services for a tenant having Azure AD Premium license and is onboarded to Azure Active Directory Connect Health. |
| GET | /providers/Microsoft.ADHybridHealthService/operations | Lists the available Azure Data Factory API operations. |
| POST | /providers/Microsoft.ADHybridHealthService/configuration | Onboards a tenant in Azure Active Directory Connect Health. |
| GET | /providers/Microsoft.ADHybridHealthService/configuration | Gets the details of a tenant onboarded to Azure Active Directory Connect Health. |
| PATCH | /providers/Microsoft.ADHybridHealthService/configuration | Updates tenant properties for tenants onboarded to Azure Active Directory Connect Health. |
| GET | /providers/Microsoft.ADHybridHealthService/reports/DevOps/IsDevOps | Checks if the user is enabled for Dev Ops access. |
| GET | /providers/Microsoft.ADHybridHealthService/services | Gets the details of services, for a tenant, that are onboarded to Azure Active Directory Connect Health. |
| POST | /providers/Microsoft.ADHybridHealthService/services | Onboards a service for a given tenant in Azure Active Directory Connect Health. |
| GET | /providers/Microsoft.ADHybridHealthService/services/premiumCheck | Gets the details of services for a tenant having Azure AD Premium license and is onboarded to Azure Active Directory Connect Health. |
| GET | /providers/Microsoft.ADHybridHealthService/services/{serviceName} | Gets the details of a service for a tenant having Azure AD Premium license and is onboarded to Azure Active Directory Connect Health. |
| DELETE | /providers/Microsoft.ADHybridHealthService/services/{serviceName} | Deletes a service which is onboarded to Azure Active Directory Connect Health. |
| PATCH | /providers/Microsoft.ADHybridHealthService/services/{serviceName} | Updates the service properties of an onboarded service. |
| GET | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/alerts | Gets the alerts for a given service. |
| GET | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/checkServiceFeatureAvailibility/{featureName} | Checks if the service has all the pre-requisites met to use a feature. |
| GET | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/exporterrors/counts | Gets the count of latest AAD export errors. |
| GET | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/exporterrors/listV2 | Gets the categorized export errors. |
| GET | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/exportstatus | Gets the export status. |
| POST | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/feedbacktype/alerts/feedback | Adds an alert feedback submitted by customer. |
| GET | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/feedbacktype/alerts/{shortName}/alertfeedback | Gets a list of all alert feedback for a given tenant and alert type. |
| GET | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/metrics/{metricName}/groups/{groupName} | Gets the server related metrics for a given metric and group combination. |
| GET | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/metrics/{metricName}/groups/{groupName}/average | Gets the average of the metric values for a given metric and group combination. |
| GET | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/metrics/{metricName}/groups/{groupName}/sum | Gets the sum of the metric values for a given metric and group combination. |
| GET | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/metricmetadata | Gets the service related metrics information. |
| GET | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/metricmetadata/{metricName} | Gets the service related metrics information. |
| GET | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/metricmetadata/{metricName}/groups/{groupName} | Gets the service related metrics for a given metric and group combination. |
| PATCH | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/monitoringconfiguration | Updates the service level monitoring configuration. |
| GET | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/monitoringconfigurations | Gets the service level monitoring configurations. |
| GET | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/reports/badpassword/details/user | Gets the bad password login attempt report for an user |
| GET | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/servicemembers | Gets the details of the servers, for a given service, that are onboarded to Azure Active Directory Connect Health Service. |
| POST | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/servicemembers | Onboards  a server, for a given service, to Azure Active Directory Connect Health Service. |
| GET | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/servicemembers/{serviceMemberId} | Gets the details of a server, for a given service, that are onboarded to Azure Active Directory Connect Health Service. |
| DELETE | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/servicemembers/{serviceMemberId} | Deletes a server that has been onboarded to Azure Active Directory Connect Health Service. |
| GET | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/servicemembers/{serviceMemberId}/alerts | Gets the details of an alert for a given service and server combination. |
| GET | /providers/Microsoft.ADHybridHealthService/service/{serviceName}/servicemembers/{serviceMemberId}/connectors | Gets the connector details for a service. |
| GET | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/servicemembers/{serviceMemberId}/credentials | Gets the credentials of the server which is needed by the agent to connect to Azure Active Directory Connect Health Service. |
| DELETE | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/servicemembers/{serviceMemberId}/data | Deletes the data uploaded by the server to Azure Active Directory Connect Health Service. |
| GET | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/servicemembers/{serviceMemberId}/datafreshness | Gets the last time when the server uploaded data to Azure Active Directory Connect Health Service. |
| GET | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/servicemembers/{serviceMemberId}/exportstatus | Gets the export status. |
| GET | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/servicemembers/{serviceMemberId}/globalconfiguration | Gets the global configuration. |
| GET | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/servicemembers/{serviceMemberId}/metrics/{metricName}/groups/{groupName} | Gets the server related metrics for a given metric and group combination. |
| GET | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/servicemembers/{serviceMemberId}/serviceconfiguration | Gets the service configuration. |
| GET | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/TenantWhitelisting/{featureName} | Checks if the tenant, to which a service is registered, is listed as allowed to use a feature. |
| GET | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/reports/riskyIp/blobUris | Gets all Risky IP report URIs for the last 7 days. |
| POST | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/reports/riskyIp/generateBlobUri | Initiate the generation of a new Risky IP report. Returns the URI for the new one. |
| GET | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/servicemembers/{serviceMemberId}/metrics/{metricName} | Gets the list of connectors and run profile names. |
| GET | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/ipAddressAggregates | Gets the IP address aggregates for a given service. |
| GET | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/ipAddressAggregateSettings | Gets the IP address aggregate settings. |
| PATCH | /providers/Microsoft.ADHybridHealthService/services/{serviceName}/ipAddressAggregateSettings | Updates the IP address aggregate settings alert thresholds. |

## Enhanced Skill Content
## Question Mapping

- "What AD DS services are registered?" -> GET /providers/Microsoft.ADHybridHealthService/addsservices
- "Show me details for a specific ADDS service" -> GET /providers/Microsoft.ADHybridHealthService/addsservices/{serviceName}
- "Are there any active alerts for my sync service?" -> GET /providers/Microsoft.ADHybridHealthService/services/{serviceName}/alerts
- "What servers are members of this service?" -> GET /providers/Microsoft.ADHybridHealthService/services/{serviceName}/servicemembers
- "Register a new health monitoring service" -> POST /providers/Microsoft.ADHybridHealthService/services
- "Remove a decommissioned service member" -> DELETE /providers/Microsoft.ADHybridHealthService/services/{serviceName}/servicemembers/{serviceMemberId}
- "What is the AD replication status across domain controllers?" -> GET /providers/Microsoft.ADHybridHealthService/addsservices/{serviceName}/replicationstatus
- "Show replication details with error info" -> GET /providers/Microsoft.ADHybridHealthService/addsservices/{serviceName}/replicationdetails
- "Get the forest summary for my AD DS environment" -> GET /providers/Microsoft.ADHybridHealthService/addsservices/{serviceName}/forestsummary
- "Are there sync export errors in my service?" -> GET /providers/Microsoft.ADHybridHealthService/services/{serviceName}/exporterrors/counts
- "Which users had bad password attempts?" -> GET /providers/Microsoft.ADHybridHealthService/services/{serviceName}/reports/badpassword/details/user
- "Download risky IP report blobs" -> GET /providers/Microsoft.ADHybridHealthService/services/{serviceName}/reports/riskyIp/blobUris
- "Is my tenant on the premium tier?" -> GET /providers/Microsoft.ADHybridHealthService/services/premiumCheck
- "What metrics are available for a service?" -> GET /providers/Microsoft.ADHybridHealthService/services/{serviceName}/metricmetadata
- "Check if data from a service member is fresh" -> GET /providers/Microsoft.ADHybridHealthService/services/{serviceName}/servicemembers/{serviceMemberId}/datafreshness

## Response Tips

- **Service listings** (`/services`, `/addsservices`): Support `$filter`, `skipCount`, and `takeCount` for pagination -- always pass `takeCount` to avoid unbounded results.
- **Alerts** (`/alerts`): Filter by `state` (active/resolved), `from`/`to` date range; results may be nested under a value array with continuation tokens.
- **Metrics** (`/metrics/{metricName}/groups/{groupName}`): Require `fromDate`/`toDate` for time-scoped data; `/average` and `/sum` variants return aggregated scalars instead of series.
- **Replication** (`/replicationdetails`, `/replicationsummary`): Use `nextPartitionKey` and `nextRowKey` for server-side pagination across large AD topologies.
- **Deletes**: Service deletion returns 204 (no body); service member deletion returns 200 -- check status code, not response body.
- **Export errors** (`/exporterrors/listV2`): Requires `errorBucket` to scope which error category to retrieve.
- **IP aggregates** (`/ipAddressAggregates`): Uses `skiptoken` for continuation-style pagination, not offset-based.

## Anomaly Flags

- **Stale data freshness**: Surface proactively when `/datafreshness` indicates a service member has not reported in over 24 hours -- likely agent offline or network issue.
- **Replication failures**: Flag non-zero error counts in `/replicationdetails` (especially with `withDetails=true`) as these indicate AD replication topology problems.
- **Export error spikes**: Alert when `/exporterrors/counts` shows increasing error counts, which signal sync pipeline failures.
- **Premium check failures**: If `/premiumCheck` returns a non-premium status, warn that advanced features (risky IP reports, certain metrics) may be unavailable.
- **Risky IP activity**: Proactively surface when `/ipAddressAggregates` returns entries, as these represent potentially malicious login sources.
- **Bad password reports**: Flag when `/reports/badpassword/details/user` returns results -- may indicate brute-force or credential-stuffing attacks.
- **Deprecated api-version**: If the `api-version` parameter uses `2014-01-01`, note that newer API versions may be available and this version may be deprecated.
- **Service member deletion without confirm**: Warn when calling DELETE on a service member without the `confirm` parameter, as behavior may vary.

## Playbook

### Investigate AD Replication Health

1. List all ADDS services: `GET /addsservices`
2. For each service, check replication status: `GET /addsservices/{serviceName}/replicationstatus`
3. If issues found, pull detailed replication info: `GET /addsservices/{serviceName}/replicationdetails?withDetails=true`
4. Review the replication summary by site: `GET /addsservices/{serviceName}/replicationsummary?isGroupbySite=true`
5. Check forest-level overview: `GET /addsservices/{serviceName}/forestsummary`

### Triage Service Alerts

1. List all monitored services: `GET /services`
2. Pull active alerts for a service: `GET /services/{serviceName}/alerts?state=active`
3. Drill into per-member alerts: `GET /services/{serviceName}/servicemembers/{serviceMemberId}/alerts?state=active`
4. Submit feedback on an alert: `POST /services/{serviceName}/feedbacktype/alerts/feedback` with alert feedback payload
5. Review historical feedback: `GET /services/{serviceName}/feedbacktype/alerts/{shortName}/alertfeedback`

### Onboard a New Service and Members

1. Register the service: `POST /services` with service configuration map
2. Verify registration: `GET /services/{serviceName}`
3. Add service members (agents): `POST /services/{serviceName}/servicemembers` with member details
4. Confirm member connectivity: `GET /services/{serviceName}/servicemembers/{serviceMemberId}/datafreshness`
5. Review available metrics: `GET /services/{serviceName}/metricmetadata`

### Analyze Risky IP and Bad Password Activity

1. Check IP address aggregates: `GET /services/{serviceName}/ipAddressAggregates`
2. Review aggregate settings: `GET /services/{serviceName}/ipAddressAggregateSettings`
3. Pull bad password reports: `GET /services/{serviceName}/reports/badpassword/details/user`
4. Generate risky IP report blob: `POST /services/{serviceName}/reports/riskyIp/generateBlobUri`
5. Download report: `GET /services/{serviceName}/reports/riskyIp/blobUris`

### Monitor Sync Export Health

1. Get export status overview: `GET /services/{serviceName}/exportstatus`
2. Check error counts by category: `GET /services/{serviceName}/exporterrors/counts`
3. List specific errors: `GET /services/{serviceName}/exporterrors/listV2?errorBucket={bucket}`
4. Check per-member export status: `GET /services/{serviceName}/servicemembers/{serviceMemberId}/exportstatus`
5. Verify connector health: `GET /service/{serviceName}/servicemembers/{serviceMemberId}/connectors`


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
