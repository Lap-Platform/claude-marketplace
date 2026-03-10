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

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all pipelineTemplates?" -> GET /providers/microsoft.visualstudio/pipelineTemplates
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
