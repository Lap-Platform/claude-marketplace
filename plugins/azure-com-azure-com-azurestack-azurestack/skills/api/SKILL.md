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

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all operations?" -> GET /providers/Microsoft.AzureStack/operations
- "List all cloudManifestFiles?" -> GET /providers/Microsoft.AzureStack/cloudManifestFiles
- "Get cloudManifestFile details?" -> GET /providers/Microsoft.AzureStack/cloudManifestFiles/{verificationVersion}
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
