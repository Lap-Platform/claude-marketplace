---
name: visual-studio-projects-resource-provider-client
description: "Visual Studio Projects Resource Provider Client API skill. Use when working with Visual Studio Projects Resource Provider Client for providers. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Visual Studio Projects Resource Provider Client
API version: 2018-08-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/microsoft.visualstudio/pipelineTemplates -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/microsoft.visualstudio/pipelineTemplates | PipelineTemplates_List |

## Enhanced Skill Content
## Question Mapping

- "What pipeline templates are available?" -> GET /providers/microsoft.visualstudio/pipelineTemplates
- "List all Visual Studio pipeline templates" -> GET /providers/microsoft.visualstudio/pipelineTemplates
- "What CI/CD templates does Azure DevOps offer?" -> GET /providers/microsoft.visualstudio/pipelineTemplates
- "Show me the available build pipeline templates for api version 2018-08-01-preview" -> GET /providers/microsoft.visualstudio/pipelineTemplates
- "Which pipeline templates can I use to set up a new project?" -> GET /providers/microsoft.visualstudio/pipelineTemplates
- "Are there any YAML pipeline templates in Azure?" -> GET /providers/microsoft.visualstudio/pipelineTemplates
- "What starter templates exist for Visual Studio pipelines?" -> GET /providers/microsoft.visualstudio/pipelineTemplates
- "Get pipeline template details for a specific template ID" -> GET /providers/microsoft.visualstudio/pipelineTemplates (filter client-side)
- "How do I find a .NET pipeline template?" -> GET /providers/microsoft.visualstudio/pipelineTemplates (filter by description/name)
- "What templates support containerized deployments?" -> GET /providers/microsoft.visualstudio/pipelineTemplates (filter client-side)
- "Refresh my cached list of pipeline templates" -> GET /providers/microsoft.visualstudio/pipelineTemplates
- "Compare available pipeline templates to pick the right one" -> GET /providers/microsoft.visualstudio/pipelineTemplates (then present comparison)

## Response Tips

- **Pipeline templates**: Response is a top-level array or object with a `value` array. Each template includes an `id`, `description`, and `inputs` collection describing required parameters. Always pass `api-version=2018-08-01-preview` as a query parameter or the request will be rejected with 400.
- **Errors**: Azure Resource Manager returns structured error bodies with `error.code` and `error.message`. Common codes: `AuthorizationFailed` (403), `InvalidApiVersionParameter` (400), `SubscriptionNotFound` (404).
- **Auth**: OAuth2 bearer token scoped to `https://management.azure.com/.default`. Token expiry is typically 60-75 minutes; refresh proactively.

## Anomaly Flags

- **Missing or wrong api-version**: The single required parameter. If omitted or invalid, Azure returns a 400 with a list of supported versions. Surface the supported versions list to the user.
- **401/403 responses**: Token may be expired or the service principal lacks the `Microsoft.VisualStudio/pipelineTemplates/read` permission. Flag immediately with remediation steps.
- **Empty template list**: If `value` is an empty array, the preview feature may not be enabled for the subscription or region. Surface this as a potential configuration issue.
- **Deprecation headers**: Watch for `Sunset` or `Deprecation` headers. This API is a preview version (2018-08-01-preview) and may be superseded. Flag any deprecation signals prominently.
- **Throttling (429)**: Azure Management APIs enforce per-subscription rate limits. Surface `Retry-After` header value and pause before retrying.
- **Preview API stability**: This is a preview API version. Flag if responses contain new or removed fields compared to previous calls, as preview APIs can change without notice.

## Playbook

### 1. List All Available Pipeline Templates

1. Acquire an OAuth2 token for scope `https://management.azure.com/.default`
2. Call `GET /providers/microsoft.visualstudio/pipelineTemplates?api-version=2018-08-01-preview`
3. Parse the `value` array from the response
4. Present each template's `id` and `description` to the user

### 2. Find a Template by Technology Stack

1. Fetch all templates using the listing playbook above
2. Filter the results client-side by matching keywords (e.g., "Node", ".NET", "Python") against each template's `id`, `description`, or `inputs`
3. Present the narrowed list with relevant details
4. If no match is found, suggest the user check Azure DevOps marketplace for community templates

### 3. Set Up a New Pipeline Using a Template

1. List available templates (Playbook 1)
2. Help the user select the appropriate template based on their project type
3. Extract the `inputs` collection from the chosen template to identify required parameters
4. Guide the user through providing values for each required input
5. Use the template ID and collected inputs with the Azure DevOps Pipelines API to create the pipeline (separate API, outside this spec)

### 4. Monitor for Template Changes Over Time

1. Call `GET /providers/microsoft.visualstudio/pipelineTemplates?api-version=2018-08-01-preview`
2. Cache the response with a timestamp
3. On subsequent checks, compare the new `value` array against the cached version
4. Surface any added, removed, or modified templates to the user
5. Flag if the API returns deprecation headers indicating a version migration is needed

### 5. Troubleshoot Authentication Failures

1. Attempt `GET /providers/microsoft.visualstudio/pipelineTemplates?api-version=2018-08-01-preview`
2. If 401: verify the OAuth2 token is present and not expired; re-authenticate if needed
3. If 403: check that the identity has the `Microsoft.VisualStudio` resource provider registered and appropriate RBAC role
4. If 400 with `InvalidApiVersionParameter`: extract the `validApiVersions` list from the error and retry with a supported version
5. Report the resolution or escalation path to the user


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
