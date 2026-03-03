---
name: diagnostics-api-client
description: "Diagnostics API Client API skill. Use when working with Diagnostics API Client for subscriptions. Covers 22 endpoints."
version: 1.0.0
generator: lapsh
---

# Diagnostics API Client
API version: 2018-02-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/detectors -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/diagnostics/{diagnosticCategory}/analyses/{analysisName}/execute -- create first execute

## Endpoints

22 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/detectors | List Hosting Environment Detector Responses |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/detectors/{detectorName} | Get Hosting Environment Detector Response |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/detectors | List Site Detector Responses |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/detectors/{detectorName} | Get site detector response |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/diagnostics | Get Diagnostics Categories |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/diagnostics/{diagnosticCategory} | Get Diagnostics Category |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/diagnostics/{diagnosticCategory}/analyses | Get Site Analyses |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/diagnostics/{diagnosticCategory}/analyses/{analysisName} | Get Site Analysis |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/diagnostics/{diagnosticCategory}/analyses/{analysisName}/execute | Execute Analysis |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/diagnostics/{diagnosticCategory}/detectors | Get Detectors |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/diagnostics/{diagnosticCategory}/detectors/{detectorName} | Get Detector |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/diagnostics/{diagnosticCategory}/detectors/{detectorName}/execute | Execute Detector |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/slots/{slot}/detectors | List Site Detector Responses |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/slots/{slot}/detectors/{detectorName} | Get site detector response |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/slots/{slot}/diagnostics | Get Diagnostics Categories |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/slots/{slot}/diagnostics/{diagnosticCategory} | Get Diagnostics Category |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/slots/{slot}/diagnostics/{diagnosticCategory}/analyses | Get Site Analyses |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/slots/{slot}/diagnostics/{diagnosticCategory}/analyses/{analysisName} | Get Site Analysis |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/slots/{slot}/diagnostics/{diagnosticCategory}/analyses/{analysisName}/execute | Execute Analysis |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/slots/{slot}/diagnostics/{diagnosticCategory}/detectors | Get Detectors |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/slots/{slot}/diagnostics/{diagnosticCategory}/detectors/{detectorName} | Get Detector |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/slots/{slot}/diagnostics/{diagnosticCategory}/detectors/{detectorName}/execute | Execute Detector |

## Enhanced Skill Content
## Question Mapping

- "What detectors are available for my App Service Environment?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/detectors
- "Get details for a specific detector on my hosting environment?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/hostingEnvironments/{name}/detectors/{detectorName}
- "List all detectors for my web app?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/detectors
- "What diagnostic categories exist for my site?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/diagnostics
- "Show me the analyses available under a diagnostic category?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/diagnostics/{diagnosticCategory}/analyses
- "Run a specific diagnostic analysis on my web app?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/diagnostics/{diagnosticCategory}/analyses/{analysisName}/execute
- "Execute a detector within a diagnostic category?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/diagnostics/{diagnosticCategory}/detectors/{detectorName}/execute
- "What detectors are available for my staging slot?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/slots/{slot}/detectors
- "Run a diagnostic analysis on a specific deployment slot?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/slots/{slot}/diagnostics/{diagnosticCategory}/analyses/{analysisName}/execute
- "Get detector results for a time range on my web app?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/detectors/{detectorName} (use startTime, endTime, timeGrain)
- "Compare diagnostics between production and a deployment slot?" -> GET .../sites/{siteName}/diagnostics + GET .../sites/{siteName}/slots/{slot}/diagnostics (two calls)
- "What diagnostic detectors apply to a category on my slot?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/slots/{slot}/diagnostics/{diagnosticCategory}/detectors
- "Get a specific analysis result for a diagnostic category?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Web/sites/{siteName}/diagnostics/{diagnosticCategory}/analyses/{analysisName}

## Response Tips

- **Detector listings** (GET .../detectors): Returns a `value` array of detector resources; each has `properties.metadata` with display names, descriptions, and supported score types. Paginate via `nextLink` if present.
- **Detector details** (GET .../detectors/{name}): Single resource object; `properties.dataset` contains time-series data points scoped to the optional startTime/endTime/timeGrain parameters. Empty datasets mean no signals in that window.
- **Diagnostic categories** (GET .../diagnostics): Returns `value` array; each entry is a category name used as a path segment in deeper calls. Treat as an enumeration for subsequent requests.
- **Analyses** (GET .../analyses, GET .../analyses/{name}): Analysis resources include `properties.abnormalTimePeriods` and `properties.payload` with structured diagnostic findings. Null or empty arrays indicate no issues detected.
- **Execute endpoints** (POST .../execute): Returns the same shape as the corresponding GET detail endpoint but with freshly computed results. These can be slower; expect latency up to 30s for complex analyses.
- **Error responses**: ARM standard error body with `error.code` and `error.message`. Common codes: `ResourceNotFound` (404), `AuthorizationFailed` (403), `Conflict` (409 for concurrent executions).

## Anomaly Flags

- **Throttling headers**: Surface `x-ms-ratelimit-remaining-subscription-reads` and `Retry-After` when approaching limits; Azure ARM defaults to 12,000 reads per hour per subscription.
- **Long-running executions**: If a POST /execute call takes over 10s, flag it as potentially hitting a complex diagnostic path and suggest narrowing the time window.
- **Empty detector datasets**: When a detector returns an empty `dataset` array for a broad time range, surface this as a possible misconfiguration or an inactive detector.
- **Abnormal time periods**: When any analysis response contains non-empty `abnormalTimePeriods`, proactively highlight these with their start/end times and severity.
- **api-version mismatch**: If the user targets a resource that returns `NoRegisteredProviderFound` or `InvalidApiVersionParameter`, flag that the 2018-02-01 version may not be available in their region or subscription.
- **Slot vs production drift**: When running the same detector on both a slot and production, flag significant differences in diagnostic scores or abnormal periods.

## Playbook

### 1. Diagnose a Web App Issue End-to-End

1. List diagnostic categories: GET .../sites/{siteName}/diagnostics
2. Pick the relevant category (e.g., "availability") and list its analyses: GET .../sites/{siteName}/diagnostics/{diagnosticCategory}/analyses
3. Execute the most relevant analysis: POST .../sites/{siteName}/diagnostics/{diagnosticCategory}/analyses/{analysisName}/execute with startTime and endTime covering the incident window
4. Review the response for `abnormalTimePeriods` and `payload` findings
5. If findings point to a specific detector, drill in: GET .../sites/{siteName}/detectors/{detectorName} with the same time range

### 2. Compare Slot Health Before Swap

1. List detectors for the production site: GET .../sites/{siteName}/detectors
2. List detectors for the target slot: GET .../sites/{siteName}/slots/{slot}/detectors
3. For each critical detector (e.g., CPU, memory, HTTP errors), fetch details for both:
   - GET .../sites/{siteName}/detectors/{detectorName}?startTime=...&endTime=...
   - GET .../sites/{siteName}/slots/{slot}/detectors/{detectorName}?startTime=...&endTime=...
4. Compare datasets side by side; flag any detector where the slot shows worse metrics than production

### 3. Monitor an App Service Environment

1. List all detectors for the ASE: GET .../hostingEnvironments/{name}/detectors
2. Identify infrastructure-level detectors (e.g., front-end health, worker pool status)
3. Fetch each detector's details with a recent time window: GET .../hostingEnvironments/{name}/detectors/{detectorName}?startTime=...&endTime=...&timeGrain=PT1H
4. Surface any detectors with non-empty abnormal signals or degraded scores

### 4. Narrow Down Intermittent Failures with Time Grain

1. Start broad: execute an analysis with timeGrain=PT1H over the past 24 hours: POST .../diagnostics/{category}/analyses/{name}/execute?startTime=...&endTime=...&timeGrain=PT1H
2. Identify the hour(s) with abnormal signals from the response
3. Re-execute with timeGrain=PT5M scoped to the problematic hour(s)
4. Correlate the finer-grained data with deployment logs or config changes in that window

### 5. Audit All Diagnostic Capabilities for a Site

1. List all top-level detectors: GET .../sites/{siteName}/detectors
2. List all diagnostic categories: GET .../sites/{siteName}/diagnostics
3. For each category, list its detectors: GET .../sites/{siteName}/diagnostics/{category}/detectors
4. For each category, list its analyses: GET .../sites/{siteName}/diagnostics/{category}/analyses
5. Compile into a capability map showing which detectors and analyses are available per category


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
