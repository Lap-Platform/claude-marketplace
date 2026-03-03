---
name: aws-systems-manager-incident-manager
description: "AWS Systems Manager Incident Manager API skill. Use when working with AWS Systems Manager Incident Manager for batchGetIncidentFindings, createReplicationSet, createResponsePlan. Covers 31 endpoints."
version: 1.0.0
generator: lapsh
---

# AWS Systems Manager Incident Manager
API version: 2018-05-10

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
2. GET /getIncidentRecord -- verify access
3. POST /batchGetIncidentFindings -- create first batchGetIncidentFindings

## Endpoints

31 endpoints across 29 groups. See references/api-spec.lap for full details.

### batchGetIncidentFindings
| Method | Path | Description |
|--------|------|-------------|
| POST | /batchGetIncidentFindings | Retrieves details about all specified findings for an incident, including descriptive details about each finding. A finding represents a recent application environment change made by an CodeDeploy deployment or an CloudFormation stack creation or update that can be investigated as a potential cause of the incident. |

### createReplicationSet
| Method | Path | Description |
|--------|------|-------------|
| POST | /createReplicationSet | A replication set replicates and encrypts your data to the provided Regions with the provided KMS key. |

### createResponsePlan
| Method | Path | Description |
|--------|------|-------------|
| POST | /createResponsePlan | Creates a response plan that automates the initial response to incidents. A response plan engages contacts, starts chat channel collaboration, and initiates runbooks at the beginning of an incident. |

### createTimelineEvent
| Method | Path | Description |
|--------|------|-------------|
| POST | /createTimelineEvent | Creates a custom timeline event on the incident details page of an incident record. Incident Manager automatically creates timeline events that mark key moments during an incident. You can create custom timeline events to mark important events that Incident Manager can detect automatically. |

### deleteIncidentRecord
| Method | Path | Description |
|--------|------|-------------|
| POST | /deleteIncidentRecord | Delete an incident record from Incident Manager. |

### deleteReplicationSet
| Method | Path | Description |
|--------|------|-------------|
| POST | /deleteReplicationSet | Deletes all Regions in your replication set. Deleting the replication set deletes all Incident Manager data. |

### deleteResourcePolicy
| Method | Path | Description |
|--------|------|-------------|
| POST | /deleteResourcePolicy | Deletes the resource policy that Resource Access Manager uses to share your Incident Manager resource. |

### deleteResponsePlan
| Method | Path | Description |
|--------|------|-------------|
| POST | /deleteResponsePlan | Deletes the specified response plan. Deleting a response plan stops all linked CloudWatch alarms and EventBridge events from creating an incident with this response plan. |

### deleteTimelineEvent
| Method | Path | Description |
|--------|------|-------------|
| POST | /deleteTimelineEvent | Deletes a timeline event from an incident. |

### getIncidentRecord
| Method | Path | Description |
|--------|------|-------------|
| GET | /getIncidentRecord | Returns the details for the specified incident record. |

### getReplicationSet
| Method | Path | Description |
|--------|------|-------------|
| GET | /getReplicationSet | Retrieve your Incident Manager replication set. |

### getResourcePolicies
| Method | Path | Description |
|--------|------|-------------|
| POST | /getResourcePolicies | Retrieves the resource policies attached to the specified response plan. |

### getResponsePlan
| Method | Path | Description |
|--------|------|-------------|
| GET | /getResponsePlan | Retrieves the details of the specified response plan. |

### getTimelineEvent
| Method | Path | Description |
|--------|------|-------------|
| GET | /getTimelineEvent | Retrieves a timeline event based on its ID and incident record. |

### listIncidentFindings
| Method | Path | Description |
|--------|------|-------------|
| POST | /listIncidentFindings | Retrieves a list of the IDs of findings, plus their last modified times, that have been identified for a specified incident. A finding represents a recent application environment change made by an CloudFormation stack creation or update or an CodeDeploy deployment that can be investigated as a potential cause of the incident. |

### listIncidentRecords
| Method | Path | Description |
|--------|------|-------------|
| POST | /listIncidentRecords | Lists all incident records in your account. Use this command to retrieve the Amazon Resource Name (ARN) of the incident record you want to update. |

### listRelatedItems
| Method | Path | Description |
|--------|------|-------------|
| POST | /listRelatedItems | List all related items for an incident record. |

### listReplicationSets
| Method | Path | Description |
|--------|------|-------------|
| POST | /listReplicationSets | Lists details about the replication set configured in your account. |

### listResponsePlans
| Method | Path | Description |
|--------|------|-------------|
| POST | /listResponsePlans | Lists all response plans in your account. |

### tags
| Method | Path | Description |
|--------|------|-------------|
| GET | /tags/{resourceArn} | Lists the tags that are attached to the specified response plan or incident. |
| POST | /tags/{resourceArn} | Adds a tag to a response plan. |
| DELETE | /tags/{resourceArn} | Removes a tag from a resource. |

### listTimelineEvents
| Method | Path | Description |
|--------|------|-------------|
| POST | /listTimelineEvents | Lists timeline events for the specified incident record. |

### putResourcePolicy
| Method | Path | Description |
|--------|------|-------------|
| POST | /putResourcePolicy | Adds a resource policy to the specified response plan. The resource policy is used to share the response plan using Resource Access Manager (RAM). For more information about cross-account sharing, see Cross-Region and cross-account incident management. |

### startIncident
| Method | Path | Description |
|--------|------|-------------|
| POST | /startIncident | Used to start an incident from CloudWatch alarms, EventBridge events, or manually. |

### updateDeletionProtection
| Method | Path | Description |
|--------|------|-------------|
| POST | /updateDeletionProtection | Update deletion protection to either allow or deny deletion of the final Region in a replication set. |

### updateIncidentRecord
| Method | Path | Description |
|--------|------|-------------|
| POST | /updateIncidentRecord | Update the details of an incident record. You can use this operation to update an incident record from the defined chat channel. For more information about using actions in chat channels, see Interacting through chat. |

### updateRelatedItems
| Method | Path | Description |
|--------|------|-------------|
| POST | /updateRelatedItems | Add or remove related items from the related items tab of an incident record. |

### updateReplicationSet
| Method | Path | Description |
|--------|------|-------------|
| POST | /updateReplicationSet | Add or delete Regions from your replication set. |

### updateResponsePlan
| Method | Path | Description |
|--------|------|-------------|
| POST | /updateResponsePlan | Updates the specified response plan. |

### updateTimelineEvent
| Method | Path | Description |
|--------|------|-------------|
| POST | /updateTimelineEvent | Updates a timeline event. You can update events of type Custom Event. |

## Enhanced Skill Content
## Question Mapping

- "How do I start a new incident?" -> POST /startIncident
- "Show me details of a specific incident" -> GET /getIncidentRecord
- "List all open incidents" -> POST /listIncidentRecords (with status filter)
- "What response plans are available?" -> POST /listResponsePlans
- "Create a new response plan for my team" -> POST /createResponsePlan
- "What happened during an incident?" -> POST /listTimelineEvents
- "Add a note to an incident timeline" -> POST /createTimelineEvent
- "How do I resolve an incident?" -> POST /updateIncidentRecord (set status to RESOLVED)
- "What regions is my replication set deployed in?" -> GET /getReplicationSet
- "Attach a related resource to an incident" -> POST /updateRelatedItems
- "Who triggered this incident and from what source?" -> GET /getIncidentRecord (check incidentRecordSource)
- "How do I protect my replication set from accidental deletion?" -> POST /updateDeletionProtection
- "What findings exist for an incident?" -> POST /listIncidentFindings
- "Tag a response plan for cost tracking" -> POST /tags/{resourceArn}
- "Remove tags from an incident resource" -> DELETE /tags/{resourceArn}

## Response Tips

- **List endpoints** (listIncidentRecords, listResponsePlans, listTimelineEvents, listReplicationSets): All return `nextToken` -- loop until `nextToken` is null/absent. Use `maxResults` to control page size.
- **Get endpoints** (getIncidentRecord, getResponsePlan, getReplicationSet, getTimelineEvent): Return deeply nested objects; access the top-level wrapper key first (e.g., `incidentRecord`, `replicationSet`, `event`).
- **Mutation endpoints** (create, update, delete, start): Most return 200 with an ARN or ID on success, or an empty body for deletes/updates -- treat non-200 as an error.
- **batchGetIncidentFindings**: Returns both `findings` (successes) and `errors` (partial failures) -- always check both arrays.
- **getResourcePolicies**: Paginated via POST with `nextToken`; policies are returned in `resourcePolicies` array.

## Anomaly Flags

- **Partial batch failures**: `batchGetIncidentFindings` returns a non-empty `errors` array alongside `findings` -- surface each failed finding ID and error reason.
- **Replication set status**: If `getReplicationSet` returns a status other than `ACTIVE` (e.g., `CREATING`, `UPDATING`, `DELETING`, `FAILED`), flag it as the set may be unavailable.
- **Deletion protection disabled**: When `getReplicationSet` shows `deletionProtected: false`, warn that the replication set can be accidentally deleted.
- **High impact incidents**: When `startIncident` or `updateIncidentRecord` uses impact level 1 (critical), flag for immediate attention.
- **Stale incidents**: If `listIncidentRecords` returns incidents with status `OPEN` and `creationTime` older than 7 days, flag as potentially stale.
- **Missing chat channel or engagements**: If `getResponsePlan` returns no `chatChannel` or empty `engagements`, warn that responders may not be notified.
- **Pagination truncation**: If any list call returns `nextToken` and the caller does not paginate, flag that results are incomplete.

## Playbook

### 1. Respond to a New Incident

1. Call `POST /listResponsePlans` to find the appropriate response plan ARN.
2. Call `POST /startIncident` with `responsePlanArn`, optional `impact` (1-5), `title`, and any `relatedItems`.
3. Note the returned `incidentRecordArn`.
4. Call `GET /getIncidentRecord` with the ARN to confirm the incident was created and review auto-populated fields.
5. Call `POST /createTimelineEvent` to log the initial triage note with `eventType` and `eventData`.

### 2. Investigate and Resolve an Incident

1. Call `GET /getIncidentRecord` to review current status, impact, and summary.
2. Call `POST /listTimelineEvents` with `incidentRecordArn` (use `sortBy: "EVENT_TIME"`, `sortOrder: "ASCENDING"`) to review the full timeline.
3. Call `POST /listRelatedItems` to see linked resources (CloudWatch alarms, runbooks, etc.).
4. Call `POST /batchGetIncidentFindings` with relevant `findingIds` to review root cause findings.
5. Call `POST /updateIncidentRecord` with `status: "RESOLVED"` and a final `summary` to close the incident.

### 3. Set Up a Response Plan with Integrations

1. Call `POST /createResponsePlan` with `name`, `incidentTemplate` (including `title`, `impact`, optional `summary` and `notificationTargets`).
2. Include `chatChannel` (SNS topic ARNs for AWS Chatbot) and `engagements` (SSM Contacts escalation plan ARNs).
3. Optionally include `actions` (SSM Automation runbooks) and `integrations` (PagerDuty, etc.).
4. Note the returned `arn`.
5. Call `POST /tags/{resourceArn}` to tag the plan for organization (e.g., `team`, `environment`).

### 4. Configure Multi-Region Replication

1. Call `POST /createReplicationSet` with a `regions` map specifying each region and its KMS key configuration.
2. Note the returned `arn`.
3. Call `GET /getReplicationSet` and poll until `status` becomes `ACTIVE`.
4. Call `POST /updateDeletionProtection` with `deletionProtected: true` to prevent accidental deletion.
5. To add or remove regions later, call `POST /updateReplicationSet` with `actions` specifying `addRegionAction` or `deleteRegionAction`.

### 5. Manage Resource Policies for Cross-Account Access

1. Call `POST /getResourcePolicies` with the `resourceArn` of the response plan or replication set. Paginate with `nextToken` if needed.
2. Review existing policies in the `resourcePolicies` array.
3. To grant cross-account access, call `POST /putResourcePolicy` with a JSON `policy` string and the `resourceArn`.
4. Note the returned `policyId`.
5. To revoke access, call `POST /deleteResourcePolicy` with the `policyId` and `resourceArn`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
