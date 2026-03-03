---
name: azure-stack-azure-bridge-client
description: "Azure Stack Azure Bridge Client API skill. Use when working with Azure Stack Azure Bridge Client for providers. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# Azure Stack Azure Bridge Client
API version: 2017-06-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.AzureStack/operations -- verify access

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.AzureStack/operations | Returns the list of supported REST operations. |
| GET | /providers/Microsoft.AzureStack/cloudManifestFiles | Returns a cloud specific manifest JSON file with latest version. |
| GET | /providers/Microsoft.AzureStack/cloudManifestFiles/{verificationVersion} | Returns a cloud specific manifest JSON file. |

## Enhanced Skill Content


## Question Mapping

- "What operations are available in Azure Stack?" -> GET /providers/Microsoft.AzureStack/operations
- "List all supported Azure Stack Bridge operations" -> GET /providers/Microsoft.AzureStack/operations
- "What can I do with the Azure Stack Bridge API?" -> GET /providers/Microsoft.AzureStack/operations
- "Get all cloud manifest files for Azure Stack" -> GET /providers/Microsoft.AzureStack/cloudManifestFiles
- "List available cloud manifests" -> GET /providers/Microsoft.AzureStack/cloudManifestFiles
- "What cloud manifest versions exist?" -> GET /providers/Microsoft.AzureStack/cloudManifestFiles
- "Get the cloud manifest for a specific version" -> GET /providers/Microsoft.AzureStack/cloudManifestFiles/{verificationVersion}
- "Retrieve cloud manifest file by verification version" -> GET /providers/Microsoft.AzureStack/cloudManifestFiles/{verificationVersion}
- "Get cloud manifest created on a specific date?" -> GET /providers/Microsoft.AzureStack/cloudManifestFiles/{verificationVersion} (use versionCreationDate filter)
- "Check if a specific Azure Stack version has a manifest" -> GET /providers/Microsoft.AzureStack/cloudManifestFiles/{verificationVersion}
- "What API version should I use for Azure Stack Bridge?" -> GET /providers/Microsoft.AzureStack/operations (inspect api-version in response)
- "How do I verify my Azure Stack deployment version?" -> GET /providers/Microsoft.AzureStack/cloudManifestFiles/{verificationVersion}
- "List manifests then fetch details for a specific version" -> GET /providers/Microsoft.AzureStack/cloudManifestFiles then GET /providers/Microsoft.AzureStack/cloudManifestFiles/{verificationVersion}

## Response Tips

- **Operations endpoint**: Returns a list of available operations with `name`, `display` info, and `isDataAction` flags. Check the `value` array for the full operation set.
- **Cloud manifest list**: Response contains an array of manifest summaries. Look for `verificationVersion` identifiers to use in detail lookups.
- **Cloud manifest by version**: Returns the full manifest object including deployment data and signatures. A 404 means the requested verification version does not exist.
- **All endpoints**: Require `api-version` as a query parameter (use `2017-06-01`). Missing it returns 400. OAuth2 token must be in the Authorization header.

## Anomaly Flags

- **Missing api-version parameter**: All three endpoints require it. Surface a warning if the caller omits it, as this guarantees a 400 error.
- **404 on version-specific manifest**: The verificationVersion may not exist. Suggest listing all manifests first to confirm valid versions.
- **Deprecated API version**: If responses include deprecation headers or warnings, flag that `2017-06-01` may be superseded by a newer version.
- **OAuth2 token expiry**: Surface proactively if a 401 is returned, as the bearer token likely expired and needs refresh.
- **Unexpected empty operations list**: If `/operations` returns an empty `value` array, flag this as potentially indicating a permissions or subscription issue.

## Playbook

### 1. Discover available API operations

1. Authenticate via OAuth2 to obtain a bearer token
2. Call `GET /providers/Microsoft.AzureStack/operations?api-version=2017-06-01`
3. Inspect the `value` array for operation names and descriptions
4. Use the operation names to understand what actions the API supports

### 2. List and inspect cloud manifests

1. Call `GET /providers/Microsoft.AzureStack/cloudManifestFiles?api-version=2017-06-01`
2. Parse the response for available verification versions
3. For each version of interest, call `GET /providers/Microsoft.AzureStack/cloudManifestFiles/{verificationVersion}?api-version=2017-06-01`
4. Review manifest content for deployment and update details

### 3. Validate a specific Azure Stack version

1. Obtain the target verification version string from your Azure Stack deployment
2. Call `GET /providers/Microsoft.AzureStack/cloudManifestFiles/{verificationVersion}?api-version=2017-06-01`
3. If 200: the version is valid -- inspect the manifest for compatibility details
4. If 404: the version is unrecognized -- list all manifests to find the closest match

### 4. Filter manifest by creation date

1. Identify the target verification version and approximate creation date
2. Call `GET /providers/Microsoft.AzureStack/cloudManifestFiles/{verificationVersion}?api-version=2017-06-01&versionCreationDate={date}`
3. Compare the returned manifest against your expected deployment timeline
4. Use this to confirm you are referencing the correct manifest revision


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
