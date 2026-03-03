---
name: twilio-voice
description: "Twilio - Voice API skill. Use when working with Twilio - Voice for Archives, ByocTrunks, ConnectionPolicies. Covers 32 endpoints."
version: 1.0.0
generator: lapsh
---

# Twilio - Voice
API version: 1.0.0

## Auth
Bearer basic

## Base URL
https://voice.twilio.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /v1/ByocTrunks -- verify access
3. POST /v1/ByocTrunks -- create first ByocTrunks

## Endpoints

32 endpoints across 7 groups. See references/api-spec.lap for full details.

### Archives
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /v1/Archives/{Date}/Calls/{Sid} | Delete an archived call record from Bulk Export. Note: this does not also delete the record from the Voice API. |

### ByocTrunks
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/ByocTrunks |  |
| GET | /v1/ByocTrunks |  |
| GET | /v1/ByocTrunks/{Sid} |  |
| POST | /v1/ByocTrunks/{Sid} |  |
| DELETE | /v1/ByocTrunks/{Sid} |  |

### ConnectionPolicies
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/ConnectionPolicies |  |
| GET | /v1/ConnectionPolicies |  |
| GET | /v1/ConnectionPolicies/{Sid} |  |
| POST | /v1/ConnectionPolicies/{Sid} |  |
| DELETE | /v1/ConnectionPolicies/{Sid} |  |
| POST | /v1/ConnectionPolicies/{ConnectionPolicySid}/Targets |  |
| GET | /v1/ConnectionPolicies/{ConnectionPolicySid}/Targets |  |
| GET | /v1/ConnectionPolicies/{ConnectionPolicySid}/Targets/{Sid} |  |
| POST | /v1/ConnectionPolicies/{ConnectionPolicySid}/Targets/{Sid} |  |
| DELETE | /v1/ConnectionPolicies/{ConnectionPolicySid}/Targets/{Sid} |  |

### DialingPermissions
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/DialingPermissions/Countries/{IsoCode} | Retrieve voice dialing country permissions identified by the given ISO country code |
| GET | /v1/DialingPermissions/Countries | Retrieve all voice dialing country permissions for this account |
| POST | /v1/DialingPermissions/BulkCountryUpdates | Create a bulk update request to change voice dialing country permissions of one or more countries identified by the corresponding [ISO country code](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) |
| GET | /v1/DialingPermissions/Countries/{IsoCode}/HighRiskSpecialPrefixes | Fetch the high-risk special services prefixes from the country resource corresponding to the [ISO country code](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) |

### Settings
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/Settings | Retrieve voice dialing permissions inheritance for the sub-account |
| POST | /v1/Settings | Update voice dialing permissions inheritance for the sub-account |

### IpRecords
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/IpRecords |  |
| GET | /v1/IpRecords |  |
| GET | /v1/IpRecords/{Sid} |  |
| POST | /v1/IpRecords/{Sid} |  |
| DELETE | /v1/IpRecords/{Sid} |  |

### SourceIpMappings
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/SourceIpMappings |  |
| GET | /v1/SourceIpMappings |  |
| GET | /v1/SourceIpMappings/{Sid} |  |
| POST | /v1/SourceIpMappings/{Sid} |  |
| DELETE | /v1/SourceIpMappings/{Sid} |  |

## Enhanced Skill Content
## Question Mapping

- "How do I delete an archived call recording?" -> DELETE /v1/Archives/{Date}/Calls/{Sid}
- "How do I create a new BYOC trunk?" -> POST /v1/ByocTrunks
- "List all my BYOC trunks" -> GET /v1/ByocTrunks
- "How do I update the voice URL on a BYOC trunk?" -> POST /v1/ByocTrunks/{Sid}
- "How do I set up a connection policy with failover targets?" -> POST /v1/ConnectionPolicies then POST /v1/ConnectionPolicies/{ConnectionPolicySid}/Targets (multiple targets with priority/weight)
- "What countries can I dial and which risk levels are enabled?" -> GET /v1/DialingPermissions/Countries
- "How do I enable high-risk number dialing for a specific country?" -> POST /v1/DialingPermissions/BulkCountryUpdates
- "What are the high-risk special prefixes for a country?" -> GET /v1/DialingPermissions/Countries/{IsoCode}/HighRiskSpecialPrefixes
- "How do I check if dialing permissions inheritance is on?" -> GET /v1/Settings
- "How do I register an IP address for SIP trunking?" -> POST /v1/IpRecords
- "How do I map a source IP to a SIP domain?" -> POST /v1/SourceIpMappings
- "How do I remove a connection policy target?" -> DELETE /v1/ConnectionPolicies/{ConnectionPolicySid}/Targets/{Sid}
- "How do I list all IP records with pagination?" -> GET /v1/IpRecords with PageSize/Page/PageToken params
- "How do I delete a BYOC trunk I no longer need?" -> DELETE /v1/ByocTrunks/{Sid}
- "How do I change the priority and weight of a connection policy target?" -> POST /v1/ConnectionPolicies/{ConnectionPolicySid}/Targets/{Sid}

## Response Tips

- **List endpoints** (GET collections): Response wraps items in a named array (`byoc_trunks`, `connection_policies`, `targets`, `ip_records`, `source_ip_mappings`, `content`) with a `meta` object for pagination -- use `meta.next_page_url` to fetch additional pages, stop when it is null.
- **Create endpoints** (POST to collection): Return 201 with the full created resource including system-assigned `sid`, `account_sid`, timestamps, and canonical `url`.
- **Update endpoints** (POST to resource): Return 200 with the full updated resource; compare `date_updated` to confirm mutation took effect.
- **Delete endpoints**: Return 204 with no body -- any non-204 response indicates failure.
- **Settings**: POST returns 202 (accepted), not 200 -- the change may not take effect immediately.
- **Dialing Permissions**: Country lists use `content` as the array key (not a resource-specific name), and include nested fields like `country_codes` (array of strings) and boolean risk flags.
- **Bulk updates**: `BulkCountryUpdates` returns `update_count` (int) and `update_request` (string) -- verify `update_count` matches your expected number of changes.

## Anomaly Flags

- **202 on Settings update**: Surface that the settings change is asynchronous -- agent should poll GET /v1/Settings to confirm the update propagated.
- **CNAM lookup enabled on BYOC trunk**: Flag when `cnam_lookup_enabled` is true, as this adds latency and cost to every inbound call.
- **High-risk numbers enabled**: Proactively warn when `high_risk_special_numbers_enabled` or `high_risk_tollfraud_numbers_enabled` is true for any country -- these carry elevated fraud risk.
- **Connection policy target weight/priority imbalance**: Surface when all targets have equal priority and weight (no failover differentiation) or when a target has weight 0 (will never receive traffic).
- **Disabled targets**: Flag when a connection policy target has `enabled: false` -- it exists but is not routing traffic.
- **CIDR prefix length extremes**: Warn if an IP record has an unusually broad CIDR (e.g., prefix < 24) which could expose a wide address range.
- **Pagination truncation**: Alert when `meta.next_page_url` is present -- the user is seeing a partial result set.
- **Missing fallback URL**: Flag BYOC trunks where `voice_url` is set but `voice_fallback_url` is null -- calls will fail with no recovery path if the primary URL is unreachable.

## Playbook

### 1. Set up a BYOC trunk with a connection policy

1. Create a connection policy: POST /v1/ConnectionPolicies with a `friendly_name`.
2. Add a primary target: POST /v1/ConnectionPolicies/{ConnectionPolicySid}/Targets with `target` URI, `priority: 1`, `weight: 10`.
3. Add a failover target: POST /v1/ConnectionPolicies/{ConnectionPolicySid}/Targets with a different `target` URI, `priority: 2`, `weight: 10`.
4. Create the BYOC trunk: POST /v1/ByocTrunks with `voice_url`, `voice_fallback_url`, `status_callback_url`, and `connection_policy_sid` set to the policy SID from step 1.
5. Verify: GET /v1/ByocTrunks/{Sid} and confirm `connection_policy_sid` is populated.

### 2. Register IP addresses and map them to a SIP domain

1. Create an IP record: POST /v1/IpRecords with `ip_address` and `cidr_prefix_length` and an optional `friendly_name`.
2. Repeat for each IP that needs to send SIP traffic.
3. Map each IP to your SIP domain: POST /v1/SourceIpMappings with `ip_record_sid` and `sip_domain_sid`.
4. Verify mappings: GET /v1/SourceIpMappings and confirm each entry shows the correct `ip_record_sid` and `sip_domain_sid`.

### 3. Configure international dialing permissions

1. Review current permissions: GET /v1/DialingPermissions/Countries to see all countries and their risk flags.
2. Check a specific country: GET /v1/DialingPermissions/Countries/{IsoCode} for detailed info including `country_codes` and risk settings.
3. Review high-risk prefixes: GET /v1/DialingPermissions/Countries/{IsoCode}/HighRiskSpecialPrefixes before enabling high-risk dialing.
4. Apply changes: POST /v1/DialingPermissions/BulkCountryUpdates with the desired country configurations.
5. Confirm: Verify `update_count` in the response matches the number of countries you intended to update.

### 4. Clean up archived calls

1. Identify the archive date and call SID you want to remove.
2. Delete the archived call: DELETE /v1/Archives/{Date}/Calls/{Sid} (date format: YYYY-MM-DD).
3. Confirm deletion: Response should be 204 with no body.

### 5. Audit and update connection policy targets

1. List all connection policies: GET /v1/ConnectionPolicies.
2. For each policy, list its targets: GET /v1/ConnectionPolicies/{ConnectionPolicySid}/Targets.
3. Check each target for issues: disabled targets, zero-weight entries, or missing priority differentiation.
4. Update as needed: POST /v1/ConnectionPolicies/{ConnectionPolicySid}/Targets/{Sid} to adjust `priority`, `weight`, `enabled`, or `target` URI.
5. Remove stale targets: DELETE /v1/ConnectionPolicies/{ConnectionPolicySid}/Targets/{Sid} for any targets no longer in use.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
