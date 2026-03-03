---
name: insightappsec-api
description: "InsightAppSec API skill. Use when working with InsightAppSec for apps, attack-templates, blackouts. Covers 102 endpoints."
version: 1.0.0
generator: lapsh
---

# InsightAppSec API
API version: v1

## Auth
ApiKey (inferred from docs)

## Base URL
https://[region].api.insight.rapid7.com/ias/v1

## Setup
1. Set your API key in the appropriate header
2. GET /apps -- verify access
3. POST /apps -- create first apps

## Endpoints

102 endpoints across 14 groups. See references/api-spec.lap for full details.

### apps
| Method | Path | Description |
|--------|------|-------------|
| GET | /apps | Get Apps |
| POST | /apps | Create App |
| GET | /apps/{app-id} | Get App |
| PUT | /apps/{app-id} | Update App |
| DELETE | /apps/{app-id} | Delete App |
| GET | /apps/{app-id}/files | Get Files |
| POST | /apps/{app-id}/files | Create File |
| GET | /apps/{app-id}/files/{file-id} | Get File |
| PUT | /apps/{app-id}/files/{file-id} | Update File |
| POST | /apps/{app-id}/files/{file-id} | Upload File Content |
| DELETE | /apps/{app-id}/files/{file-id} | Delete File |
| GET | /apps/{app-id}/tags | Get App Tags |
| POST | /apps/{app-id}/tags | Add App Tag |
| DELETE | /apps/{app-id}/tags/{tag-id} | Remove App Tag |
| GET | /apps/{app-id}/users | Get App Users |
| POST | /apps/{app-id}/users | Add App User |
| DELETE | /apps/{app-id}/users/{user-id} | Remove App User |

### attack-templates
| Method | Path | Description |
|--------|------|-------------|
| GET | /attack-templates | Get Attack Templates |
| POST | /attack-templates | Create Attack Template |
| GET | /attack-templates/module-configs | Get Attack Modules Configs |
| GET | /attack-templates/{attack-template-id} | Get Attack Template |
| PUT | /attack-templates/{attack-template-id} | Update Attack Template |
| DELETE | /attack-templates/{attack-template-id} | Delete Attack Template |
| GET | /attack-templates/{attack-template-id}/modules | Get Attack Modules |
| POST | /attack-templates/{attack-template-id}/modules | Create Attack Module |
| PUT | /attack-templates/{attack-template-id}/modules/{attack-module-id} | Update Attack Module |
| DELETE | /attack-templates/{attack-template-id}/modules/{attack-module-id} | Delete Attack Module |

### blackouts
| Method | Path | Description |
|--------|------|-------------|
| GET | /blackouts | Get Blackouts |
| POST | /blackouts | Create Blackout |
| GET | /blackouts/{blackout-id} | Get Blackout |
| PUT | /blackouts/{blackout-id} | Update Blackout |
| DELETE | /blackouts/{blackout-id} | Delete Blackout |

### engine-groups
| Method | Path | Description |
|--------|------|-------------|
| GET | /engine-groups | Get Engine Groups |
| POST | /engine-groups | Create Engine Group |
| GET | /engine-groups/{engine-group-id} | Get Engine Group |
| PUT | /engine-groups/{engine-group-id} | Update Engine Group |
| DELETE | /engine-groups/{engine-group-id} | Delete Engine Group |
| GET | /engine-groups/{engine-group-id}/engines | Get Engine Group Engines |

### engines
| Method | Path | Description |
|--------|------|-------------|
| GET | /engines | Get Engines |
| POST | /engines | Create Engine |
| GET | /engines/{engine-id} | Get Engine |
| PUT | /engines/{engine-id} | Update Engine |
| DELETE | /engines/{engine-id} | Delete Engine |
| GET | /engines/{engine-id}/credential | Get Engine Credential |
| PUT | /engines/{engine-id}/credential | Regenerate Engine Credential |
| DELETE | /engines/{engine-id}/credential | Delete Engine Credential |
| POST | /engines/{engine-id}/upgrade | Upgrade Engine |

### modules
| Method | Path | Description |
|--------|------|-------------|
| GET | /modules | Get Modules |
| GET | /modules/{module-id} | Get Module |
| GET | /modules/{module-id}/attacks/{attack-id} | Get Attack |
| GET | /modules/{module-id}/attacks/{attack-id}/documentation | Get Attack Documentation |

### reports
| Method | Path | Description |
|--------|------|-------------|
| GET | /reports | Get Reports |
| POST | /reports | Generate Report |
| GET | /reports/{report-id} | Get Report |
| DELETE | /reports/{report-id} | Delete Report |

### scan-configs
| Method | Path | Description |
|--------|------|-------------|
| GET | /scan-configs | Get Scan Configs |
| POST | /scan-configs | Create Scan Config |
| GET | /scan-configs/options/default | Get Scan Configs Options Default |
| GET | /scan-configs/{scan-config-id} | Get Scan Config |
| PUT | /scan-configs/{scan-config-id} | Update Scan Config |
| DELETE | /scan-configs/{scan-config-id} | Delete Scan Config |
| GET | /scan-configs/{scan-config-id}/options | Get Scan Config Options |
| PUT | /scan-configs/{scan-config-id}/options | Update Scan Config Options |
| PATCH | /scan-configs/{scan-config-id}/options | Patch Scan Config Options |

### scans
| Method | Path | Description |
|--------|------|-------------|
| GET | /scans | Get Scans |
| POST | /scans | Submit Scan |
| GET | /scans/{scan-id} | Get Scan |
| DELETE | /scans/{scan-id} | Delete Scan |
| GET | /scans/{scan-id}/action | Get Scan Action |
| PUT | /scans/{scan-id}/action | Submit Scan Action |
| GET | /scans/{scan-id}/engine-events | Get Scan Engine Events |
| GET | /scans/{scan-id}/execution-details | Get Scan Execution Details |
| GET | /scans/{scan-id}/platform-events | Get Scan Platform Events |

### schedules
| Method | Path | Description |
|--------|------|-------------|
| GET | /schedules | Get Schedules |
| POST | /schedules | Create Schedule |
| GET | /schedules/{schedule-id} | Get Schedule |
| PUT | /schedules/{schedule-id} | Update Schedule |
| DELETE | /schedules/{schedule-id} | Delete Schedule |

### search
| Method | Path | Description |
|--------|------|-------------|
| POST | /search | Perform Search |

### tags
| Method | Path | Description |
|--------|------|-------------|
| GET | /tags | Get Tags |
| POST | /tags | Create Tag |
| GET | /tags/{tag-id} | Get Tag |
| PUT | /tags/{tag-id} | Update Tag |
| DELETE | /tags/{tag-id} | Delete Tag |

### targets
| Method | Path | Description |
|--------|------|-------------|
| GET | /targets | Get Targets |
| POST | /targets | Create Target |
| GET | /targets/{target-id} | Get Target |
| PUT | /targets/{target-id} | Update Target |
| DELETE | /targets/{target-id} | Delete Target |

### vulnerabilities
| Method | Path | Description |
|--------|------|-------------|
| GET | /vulnerabilities | Get Vulnerabilities |
| POST | /vulnerabilities/variances/documentation | Get Vulnerability Variances Documentation |
| GET | /vulnerabilities/{vuln-id} | Get Vulnerability |
| PUT | /vulnerabilities/{vuln-id} | Update Vulnerability |
| GET | /vulnerabilities/{vuln-id}/comments | Get Vulnerability Comments |
| POST | /vulnerabilities/{vuln-id}/comments | Create Vulnerability Comment |
| GET | /vulnerabilities/{vuln-id}/comments/{comment-id} | Get Vulnerability Comment |
| PUT | /vulnerabilities/{vuln-id}/comments/{comment-id} | Update Vulnerability Comment |
| DELETE | /vulnerabilities/{vuln-id}/comments/{comment-id} | Delete Vulnerability Comment |
| GET | /vulnerabilities/{vuln-id}/discoveries | Get Vulnerability Discoveries |
| GET | /vulnerabilities/{vuln-id}/discoveries/{vuln-discovery-id} | Get Vulnerability Discovery |
| GET | /vulnerabilities/{vuln-id}/history | Get Vulnerability History |
| GET | /vulnerabilities/{vuln-id}/variances/{variance-id}/documentation | Get Vulnerability Variance Documentation |

## Enhanced Skill Content
## Question Mapping

- "What apps are registered in InsightAppSec?" -> GET /apps
- "How do I create a new application to scan?" -> POST /apps
- "What vulnerabilities have been found?" -> GET /vulnerabilities
- "Show me details for a specific vulnerability" -> GET /vulnerabilities/{vuln-id}
- "How do I kick off a scan?" -> POST /scans
- "What is the current status of my scan?" -> GET /scans/{scan-id}
- "How do I pause or stop a running scan?" -> PUT /scans/{scan-id}/action
- "How many links have been crawled so far in this scan?" -> GET /scans/{scan-id}/execution-details
- "How do I generate a PCI compliance report?" -> POST /reports
- "What scan configs are available?" -> GET /scan-configs
- "How do I search for all critical vulnerabilities?" -> POST /search (type=VULNERABILITY)
- "What engines are online and available?" -> GET /engines
- "How do I set up a recurring scan schedule?" -> POST /schedules
- "How do I create a maintenance blackout window?" -> POST /blackouts
- "How do I mark a vulnerability as a false positive?" -> PUT /vulnerabilities/{vuln-id}

## Response Tips

- **List endpoints** (apps, scans, vulns, etc.): Responses use `{data, metadata, links}` structure. Use `metadata` for total counts and `links` for HATEOAS navigation. Paginate with `index`, `size`, and `page-token` query params.
- **Single resource GETs**: Return the object directly with a `links` array for related actions; always check `links` for discoverable sub-resource URLs.
- **Create (POST)**: Returns 201 with the resource Location header; the response body may be empty -- use the returned ID or Location to fetch the full object.
- **Update (PUT/PATCH)**: Returns 200 on success; scan-config options support both PUT (full replace) and PATCH (partial update).
- **Delete**: Returns 204 No Content with an empty body; a 409 means the resource is in use or has dependencies.
- **Search (POST /search)**: Returns `{data: [map], metadata, links}`; the `type` field determines the shape of objects in `data` -- each type returns different fields.
- **Vulnerabilities**: Severity uses `SAFE|INFORMATIONAL|LOW|MEDIUM|HIGH|CRITICAL`; status uses `UNREVIEWED|FALSE_POSITIVE|VERIFIED|IGNORED|REMEDIATED|DUPLICATE` -- both are string enums.
- **Scans**: The `status` field has 16 possible values tracking the full lifecycle from PENDING through COMPLETE or FAILED; `failure_reason` explains why a scan failed.

## Anomaly Flags

- **Engine status degradation**: Surface when any engine reports status `FAILED`, `OFFLINE`, or `PARKED` -- especially `failure_reason` values like `INITIALIZATION_FAILED` or `UPGRADE_FAILED`.
- **Scan failures**: Proactively alert on scans with status `FAILED` and flag the `failure_reason` (e.g., `LICENSE_INVALID`, `ENGINE_UNAVAILABLE`, `BAD_AUTH`, `INSUFFICIENT_MEMORY`).
- **415 Unsupported Media Type**: Every endpoint can return 415 -- if seen, the request is missing `Content-Type: application/json`.
- **409 Conflict**: Indicates a naming collision or resource-in-use condition; surface when creates or deletes return 409 so the user can resolve the conflict.
- **422 Unprocessable Entity**: Validation failure on write operations; surface the response body which contains field-level error details.
- **Blackout overlap**: When a scan returns status `BLACKED_OUT`, flag that an active blackout window is blocking execution and link to GET /blackouts.
- **Stale vulnerabilities**: Flag vulnerabilities where `newly_discovered` is false and `status` is still `UNREVIEWED` -- these are known but untriaged findings.
- **Engine upgrade available**: When `upgradeable` is true and `latest_version` is false on an engine, proactively suggest running POST /engines/{id}/upgrade.
- **Scan authentication issues**: Surface scans stuck in `AWAITING_AUTHENTICATION` or `AUTHENTICATING` status, or those that failed with `BAD_AUTH` or `BOOTSTRAP_AUTHENTICATION_FAILURE`.

## Playbook

### 1. Set Up and Run a Full Application Scan

1. Create the app: POST /apps with `{name, description}`
2. Create or select an attack template: GET /attack-templates to list existing, or POST /attack-templates to create one
3. Create a scan config: POST /scan-configs with `{name, app: {id}, attack_template: {id}}`
4. Optionally tune scan options: PUT /scan-configs/{id}/options (auth config, proxy, performance settings)
5. Launch the scan: POST /scans with `{scan_config: {id}}`
6. Monitor progress: poll GET /scans/{id}/execution-details for `links_crawled`, `attacked`, `vulnerable` counts
7. When status is `COMPLETE`, review results: GET /vulnerabilities (or POST /search with type=VULNERABILITY)

### 2. Triage and Remediate Vulnerabilities

1. Search for critical/high vulnerabilities: POST /search with `{type: "VULNERABILITY", query: "vulnerability.severity = 'CRITICAL'"}`
2. Get full details for each finding: GET /vulnerabilities/{vuln-id}
3. Review variance documentation: GET /vulnerabilities/{vuln-id}/variances/{variance-id}/documentation for remediation guidance
4. Check discovery history: GET /vulnerabilities/{vuln-id}/discoveries to see which scans found it
5. Add analyst notes: POST /vulnerabilities/{vuln-id}/comments with `{content: "..."}`
6. Update status: PUT /vulnerabilities/{vuln-id} with `{status: "VERIFIED"}` or `{status: "FALSE_POSITIVE"}`
7. Run a verification scan: POST /scans with `scan_type: "VERIFICATION"` to confirm the fix

### 3. Schedule Recurring Scans with Blackout Windows

1. Identify the scan config to schedule: GET /scan-configs and pick the target config ID
2. Create a schedule: POST /schedules with `{name, enabled: true, scan_config: {id}, first_start: "<ISO datetime>", rrule: "FREQ=WEEKLY;BYDAY=SA"}`
3. Define a blackout window for maintenance: POST /blackouts with `{name, enabled: true, first_start, first_end, scope: "GLOBAL"}`
4. Verify the schedule is active: GET /schedules/{id} and confirm `enabled: true`
5. Monitor scheduled scan runs: GET /scans with sort by submit_time to see triggered scans

### 4. Generate a Compliance Report

1. Run a scan and wait for completion: GET /scans/{id} until status is `COMPLETE`
2. Generate the report: POST /reports with `{name: "PCI Q1 2026", type: "PCI_COMPLIANCE", format: "PDF", scan: {id}}`
3. Poll report status: GET /reports/{id} until `status` indicates generation is complete
4. Download or share the report using the links in the response
5. Clean up old reports if needed: DELETE /reports/{id}

### 5. Manage Scan Engines and Engine Groups

1. List all engines: GET /engines to check status and versions
2. Flag any engines with `status: "OFFLINE"` or `status: "FAILED"` for investigation
3. Upgrade outdated engines: for each engine where `upgradeable: true`, call POST /engines/{id}/upgrade
4. Organize engines into groups: POST /engine-groups with `{name, description}`, then PUT /engines/{id} to assign `engine_group`
5. Verify group membership: GET /engine-groups/{id}/engines to confirm engines are correctly assigned
6. Rotate engine credentials if needed: PUT /engines/{id}/credential to regenerate, or DELETE /engines/{id}/credential to revoke


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
