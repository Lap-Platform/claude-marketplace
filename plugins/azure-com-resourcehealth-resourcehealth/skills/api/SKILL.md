---
name: microsoftresourcehealth
description: "Microsoft.ResourceHealth API skill. Use when working with Microsoft.ResourceHealth for providers, subscriptions, {resourceUri}. Covers 12 endpoints."
version: 1.0.0
generator: lapsh
---

# Microsoft.ResourceHealth
API version: 2018-07-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.ResourceHealth/metadata -- verify access

## Endpoints

12 endpoints across 3 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.ResourceHealth/metadata/{name} | Gets the metadata entity. |
| GET | /providers/Microsoft.ResourceHealth/metadata | Gets the list of metadata entities. |
| GET | /providers/Microsoft.ResourceHealth/emergingIssues/{issueName} | Gets Azure services' emerging issues. |
| GET | /providers/Microsoft.ResourceHealth/emergingIssues | Lists Azure services' emerging issues. |
| GET | /providers/Microsoft.ResourceHealth/operations | Lists available operations for the resourcehealth resource provider |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.ResourceHealth/events | Lists current service health events in the subscription. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.ResourceHealth/impactedResources | Lists the current availability status for impacted resources in the subscription. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.ResourceHealth/availabilityStatuses | Lists the current availability status for all the resources in the subscription. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ResourceHealth/availabilityStatuses | Lists the current availability status for all the resources in the resource group. |

### {resourceUri}
| Method | Path | Description |
|--------|------|-------------|
| GET | /{resourceUri}/providers/Microsoft.ResourceHealth/events | Lists current service health events for given resource. |
| GET | /{resourceUri}/providers/Microsoft.ResourceHealth/availabilityStatuses/current | Gets current availability status for a single resource |
| GET | /{resourceUri}/providers/Microsoft.ResourceHealth/availabilityStatuses | Lists all historical availability transitions and impacting events for a single resource. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Get metadata details?" -> GET /providers/Microsoft.ResourceHealth/metadata/{name}
- "List all metadata?" -> GET /providers/Microsoft.ResourceHealth/metadata
- "Get emergingIssue details?" -> GET /providers/Microsoft.ResourceHealth/emergingIssues/{issueName}
- "List all emergingIssues?" -> GET /providers/Microsoft.ResourceHealth/emergingIssues
- "List all events?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.ResourceHealth/events
- "List all events?" -> GET /{resourceUri}/providers/Microsoft.ResourceHealth/events
- "List all impactedResources?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.ResourceHealth/impactedResources
- "List all availabilityStatuses?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.ResourceHealth/availabilityStatuses
- "List all availabilityStatuses?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ResourceHealth/availabilityStatuses
- "List all current?" -> GET /{resourceUri}/providers/Microsoft.ResourceHealth/availabilityStatuses/current
- "List all availabilityStatuses?" -> GET /{resourceUri}/providers/Microsoft.ResourceHealth/availabilityStatuses
- "List all operations?" -> GET /providers/Microsoft.ResourceHealth/operations
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
