---
name: akamai-application-security-api
description: "Akamai: Application Security API skill. Use when working with Akamai: Application Security for activations, api-discovery, configs. Covers 213 endpoints."
version: 1.0.0
generator: lapsh
---

# Akamai: Application Security API
API version: v1

## Auth
No authentication required.

## Base URL
https://{hostname}/appsec/v1

## Setup
1. No auth setup needed
2. GET /api-discovery -- verify access
3. POST /activations -- create first activations

## Endpoints

213 endpoints across 10 groups. See references/api-spec.lap for full details.

### activations
| Method | Path | Description |
|--------|------|-------------|
| POST | /activations | Activate a configuration version |
| GET | /activations/status/{statusId} | Get an activation request status |
| GET | /activations/{activationId} | Get activation status |

### api-discovery
| Method | Path | Description |
|--------|------|-------------|
| GET | /api-discovery | List discovered APIs |
| GET | /api-discovery/host/{hostname}/basepath/{basePath} | Get a discovered API |
| PUT | /api-discovery/host/{hostname}/basepath/{basePath} | Modify an API's visibility |
| POST | /api-discovery/host/{hostname}/basepath/{basePath}/endpoints | Create an endpoint or resource |
| GET | /api-discovery/host/{hostname}/basepath/{basePath}/endpoints | List discovered API endpoints |

### configs
| Method | Path | Description |
|--------|------|-------------|
| POST | /configs | Create a configuration |
| GET | /configs | List configurations |
| GET | /configs/{configId} | Get a security configuration |
| PUT | /configs/{configId} | Rename a security configuration |
| DELETE | /configs/{configId} | Delete a configuration |
| GET | /configs/{configId}/activations | List activation history |
| POST | /configs/{configId}/custom-rules | Create a custom rule |
| GET | /configs/{configId}/custom-rules | List custom rules |
| GET | /configs/{configId}/custom-rules/{ruleId} | Get a custom rule |
| PUT | /configs/{configId}/custom-rules/{ruleId} | Modify a custom rule |
| DELETE | /configs/{configId}/custom-rules/{ruleId} | Remove a custom rule |
| GET | /configs/{configId}/failover-hostnames | List failover hostnames |
| POST | /configs/{configId}/notification/subscription/{feature} | Subscribe or unsubscribe to recommendation emails |
| GET | /configs/{configId}/notification/subscription/{feature} | List subscribers |
| POST | /configs/{configId}/versions | Clone a configuration version |
| GET | /configs/{configId}/versions | List configuration versions |
| POST | /configs/{configId}/versions/diff | Compare two versions |
| GET | /configs/{configId}/versions/{versionNumber} | Get configuration version details |
| DELETE | /configs/{configId}/versions/{versionNumber} | Delete a configuration version |
| GET | /configs/{configId}/versions/{versionNumber}/advanced-settings/cookie-settings | Get cookie settings |
| PUT | /configs/{configId}/versions/{versionNumber}/advanced-settings/cookie-settings | Modify cookie settings |
| GET | /configs/{configId}/versions/{versionNumber}/advanced-settings/evasive-path-match | Get evasive path match settings for a configuration |
| PUT | /configs/{configId}/versions/{versionNumber}/advanced-settings/evasive-path-match | Modify evasive path match settings for a configuration |
| GET | /configs/{configId}/versions/{versionNumber}/advanced-settings/logging | Get the HTTP header log settings for a configuration |
| PUT | /configs/{configId}/versions/{versionNumber}/advanced-settings/logging | Modify HTTP header log settings for a configuration |
| GET | /configs/{configId}/versions/{versionNumber}/advanced-settings/logging/attack-payload | Get the attack payload log settings for a configuration |
| PUT | /configs/{configId}/versions/{versionNumber}/advanced-settings/logging/attack-payload | Modify attack payload log settings for a configuration |
| GET | /configs/{configId}/versions/{versionNumber}/advanced-settings/pii-learning | Get PII learning settings for a configuration |
| PUT | /configs/{configId}/versions/{versionNumber}/advanced-settings/pii-learning | Enable PII learning settings for a configuration |
| GET | /configs/{configId}/versions/{versionNumber}/advanced-settings/pragma-header | Get Pragma settings for a configuration |
| PUT | /configs/{configId}/versions/{versionNumber}/advanced-settings/pragma-header | Modify Pragma settings for a configuration |
| GET | /configs/{configId}/versions/{versionNumber}/advanced-settings/prefetch | Get prefetch requests |
| PUT | /configs/{configId}/versions/{versionNumber}/advanced-settings/prefetch | Modify prefetch requests |
| GET | /configs/{configId}/versions/{versionNumber}/advanced-settings/request-body | Get request body size settings for a configuration |
| PUT | /configs/{configId}/versions/{versionNumber}/advanced-settings/request-body | Modify request body inspection limit settings for a configuration |
| GET | /configs/{configId}/versions/{versionNumber}/bypass-network-lists | Get bypass network lists settings |
| PUT | /configs/{configId}/versions/{versionNumber}/bypass-network-lists | Modify the bypass network lists settings |
| POST | /configs/{configId}/versions/{versionNumber}/custom-deny | Create a custom deny action |
| GET | /configs/{configId}/versions/{versionNumber}/custom-deny | List custom deny actions |
| GET | /configs/{configId}/versions/{versionNumber}/custom-deny/{customDenyId} | Get a custom deny action |
| PUT | /configs/{configId}/versions/{versionNumber}/custom-deny/{customDenyId} | Modify a custom deny action |
| DELETE | /configs/{configId}/versions/{versionNumber}/custom-deny/{customDenyId} | Remove a custom deny action |
| GET | /configs/{configId}/versions/{versionNumber}/hostname-coverage/match-targets | Get the hostname coverage match targets |
| GET | /configs/{configId}/versions/{versionNumber}/hostname-coverage/overlapping | List hostname overlaps |
| POST | /configs/{configId}/versions/{versionNumber}/malware-policies | Create a malware policy |
| GET | /configs/{configId}/versions/{versionNumber}/malware-policies | List malware policies |
| GET | /configs/{configId}/versions/{versionNumber}/malware-policies/content-types | List supported malware policy content types |
| GET | /configs/{configId}/versions/{versionNumber}/malware-policies/{malwarePolicyId} | Get a malware policy |
| PUT | /configs/{configId}/versions/{versionNumber}/malware-policies/{malwarePolicyId} | Modify a malware policy |
| DELETE | /configs/{configId}/versions/{versionNumber}/malware-policies/{malwarePolicyId} | Remove a malware policy |
| POST | /configs/{configId}/versions/{versionNumber}/match-targets | Create a match target |
| GET | /configs/{configId}/versions/{versionNumber}/match-targets | List match targets |
| PUT | /configs/{configId}/versions/{versionNumber}/match-targets/sequence | Modify match target order |
| GET | /configs/{configId}/versions/{versionNumber}/match-targets/{targetId} | Get a match target |
| PUT | /configs/{configId}/versions/{versionNumber}/match-targets/{targetId} | Modify a match target |
| DELETE | /configs/{configId}/versions/{versionNumber}/match-targets/{targetId} | Remove a match target |
| PUT | /configs/{configId}/versions/{versionNumber}/protect-eval-hostnames | Protect evaluation hostnames |
| POST | /configs/{configId}/versions/{versionNumber}/rate-policies | Create a rate policy |
| GET | /configs/{configId}/versions/{versionNumber}/rate-policies | List rate policies |
| GET | /configs/{configId}/versions/{versionNumber}/rate-policies/{ratePolicyId} | Get a rate policy |
| PUT | /configs/{configId}/versions/{versionNumber}/rate-policies/{ratePolicyId} | Modify a rate policy |
| DELETE | /configs/{configId}/versions/{versionNumber}/rate-policies/{ratePolicyId} | Remove a rate policy |
| PUT | /configs/{configId}/versions/{versionNumber}/rate-policies/{ratePolicyId}/evaluation | Modify a rate policy evaluation |
| POST | /configs/{configId}/versions/{versionNumber}/reputation-profiles | Create a reputation profile |
| GET | /configs/{configId}/versions/{versionNumber}/reputation-profiles | List reputation profiles |
| GET | /configs/{configId}/versions/{versionNumber}/reputation-profiles/{reputationProfileId} | Get a reputation profile |
| PUT | /configs/{configId}/versions/{versionNumber}/reputation-profiles/{reputationProfileId} | Modify a reputation profile |
| DELETE | /configs/{configId}/versions/{versionNumber}/reputation-profiles/{reputationProfileId} | Remove a reputation profile |
| POST | /configs/{configId}/versions/{versionNumber}/security-policies | Clone or create a security policy |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies | List security policies |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId} | Get a security policy |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId} | Modify a security policy |
| DELETE | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId} | Remove a security policy |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/advanced-settings/evasive-path-match | Get evasive path match settings |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/advanced-settings/evasive-path-match | Modify evasive path match settings |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/advanced-settings/logging | Get HTTP header log settings |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/advanced-settings/logging | Modify HTTP header log settings |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/advanced-settings/logging/attack-payload | Get attack payload logging settings for a policy |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/advanced-settings/logging/attack-payload | Modify attack payload logging settings for a policy |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/advanced-settings/pragma-header | Get Pragma settings for a security policy |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/advanced-settings/pragma-header | Modify Pragma settings for a security policy |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/advanced-settings/request-body | Get request body inspection limit settings for a security policy |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/advanced-settings/request-body | Modify request body size settings for a security policy |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/api-endpoints | List API endpoints |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/api-request-constraints | List API request constraints and actions |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/api-request-constraints | Modify the request constraint action for all APIs |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/api-request-constraints/{apiId} | Modify an API request constraint's action |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/attack-groups | List attack groups |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/attack-groups/{attackGroupId} | Get the action for an attack group |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/attack-groups/{attackGroupId} | Modify the action for an attack group |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/attack-groups/{attackGroupId}/condition-exception | Get the exceptions of an attack group |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/attack-groups/{attackGroupId}/condition-exception | Modify the exceptions of an attack group |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/bypass-network-lists | Get the bypass network lists settings for a security policy |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/bypass-network-lists | Modify the bypass network lists settings for a security policy |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/cpc | Get Client-Side Protection & Compliance settings |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/cpc | Modify Client-Side Protections & Compliance settings |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/custom-rules | List custom rule actions |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/custom-rules/{ruleId} | Modify a custom rule action |
| POST | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/eval | Set evaluation mode |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/eval-groups | List evaluation attack groups |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/eval-groups/{attackGroupId} | Get the action for an evaluation attack group |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/eval-groups/{attackGroupId} | Modify the action for an evaluation attack group |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/eval-groups/{attackGroupId}/condition-exception | Get the exceptions of an evaluation attack group |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/eval-groups/{attackGroupId}/condition-exception | Modify the exceptions of an evaluation attack group |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/eval-hostnames | List evaluation hostnames for a security policy |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/eval-hostnames | Modify evaluation hostnames for a security policy |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/eval-penalty-box | Get the penalty box for a policy in evaluation mode |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/eval-penalty-box | Modify the evaluation penalty box |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/eval-penalty-box/conditions | Get penalty box conditions in evaluation mode |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/eval-penalty-box/conditions | Modify the penalty box conditions in evaluation mode |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/eval-rules | List evaluation rules |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/eval-rules/{ruleId} | Get the action of an evaluation rule |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/eval-rules/{ruleId} | Modify the action of an evaluation rule |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/eval-rules/{ruleId}/condition-exception | Get the conditions and exceptions for an evaluation rule |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/eval-rules/{ruleId}/condition-exception | Modify the conditions and exceptions for an evaluation rule |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/ip-geo-firewall | Get IP/Geo Firewall settings |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/ip-geo-firewall | Modify IP/Geo Firewall settings |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/malware-policies | List malware policy actions |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/malware-policies/{malwarePolicyId} | Modify a malware policy action |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/mode | Get the current mode |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/mode | Modify the mode |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/penalty-box | Get the penalty box |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/penalty-box | Modify the penalty box |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/penalty-box/conditions | Get penalty box condition |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/penalty-box/conditions | Modify the penalty box conditions |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/protect-eval-hostnames | Protect evaluation hostnames for a security policy |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/protections | Get protections |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/protections | Modify protections |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/rapid-rules | List rapid rules |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/rapid-rules/action | Get rapid rules' default action |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/rapid-rules/action | Update rapid rules' default action |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/rapid-rules/status | Get rapid rules' status |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/rapid-rules/status | Update rapid rules' status |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/rapid-rules/{ruleId}/condition-exception | List a rapid rule's conditions and exceptions |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/rapid-rules/{ruleId}/condition-exception | Update a rapid rule's conditions and exceptions |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/rapid-rules/{ruleId}/lock | Get a rapid rule's lock status |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/rapid-rules/{ruleId}/lock | Update a rapid rule's lock status |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/rapid-rules/{ruleId}/versions/{ruleVersion}/action | Get a rapid rule's action |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/rapid-rules/{ruleId}/versions/{ruleVersion}/action | Update a rapid rule's action |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/rate-policies | List rate policy actions |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/rate-policies/{ratePolicyId} | Modify a rate policy action |
| POST | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/recommendations | Respond to exception recommendations |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/recommendations | Get tuning recommendations for a policy |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/recommendations/attack-groups/{attackGroupId} | List tuning recommendations for an attack group |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/recommendations/rules/{ruleId} | List tuning recommendations for a rule |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/reputation-analysis | Get reputation analysis settings |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/reputation-analysis | Modify reputation analysis settings |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/reputation-profiles | List reputation profile actions |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/reputation-profiles/{reputationProfileId} | Get the action for a reputation profile |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/reputation-profiles/{reputationProfileId} | Modify the action for a reputation profile |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/rules | List rules |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/rules | Upgrade KRS ruleset |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/rules/threat-intel | Get adaptive intelligence settings |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/rules/threat-intel | Modify adaptive intelligence settings |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/rules/upgrade-details | Get upgrade details |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/rules/{ruleId} | Get the action for a rule |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/rules/{ruleId} | Modify the action for a rule |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/rules/{ruleId}/condition-exception | Get the conditions and exceptions of a rule |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/rules/{ruleId}/condition-exception | Modify the conditions and exceptions of a rule |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/selected-hostnames | List selected hostnames for a security policy |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/selected-hostnames | Modify selected hostnames for a security policy |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/slow-post | Get slow POST protection settings |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/slow-post | Modify slow POST protection settings |
| GET | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/url-protections | List URL protection policy actions |
| PUT | /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/url-protections/{urlProtectionPolicyId} | Modify a URL protection policy action |
| GET | /configs/{configId}/versions/{versionNumber}/selectable-hostnames | List selectable hostnames |
| GET | /configs/{configId}/versions/{versionNumber}/selected-hostnames | List selected hostnames |
| PUT | /configs/{configId}/versions/{versionNumber}/selected-hostnames | Modify selected hostnames |
| GET | /configs/{configId}/versions/{versionNumber}/selected-hostnames/eval-hostnames | List evaluation hostnames |
| PUT | /configs/{configId}/versions/{versionNumber}/selected-hostnames/eval-hostnames | Modify evaluation hostnames |
| GET | /configs/{configId}/versions/{versionNumber}/siem | Get SIEM settings |
| PUT | /configs/{configId}/versions/{versionNumber}/siem | Modify SIEM settings |
| POST | /configs/{configId}/versions/{versionNumber}/url-protections | Create a URL protection policy |
| GET | /configs/{configId}/versions/{versionNumber}/url-protections | List URL protection policies |
| GET | /configs/{configId}/versions/{versionNumber}/url-protections/{urlProtectionPolicyId} | Get a URL protection policy |
| PUT | /configs/{configId}/versions/{versionNumber}/url-protections/{urlProtectionPolicyId} | Modify a URL protection policy |
| DELETE | /configs/{configId}/versions/{versionNumber}/url-protections/{urlProtectionPolicyId} | Remove a URL protection policy |
| GET | /configs/{configId}/versions/{versionNumber}/version-notes | Get the version notes |
| PUT | /configs/{configId}/versions/{versionNumber}/version-notes | Modify version notes |

### contracts-groups
| Method | Path | Description |
|--------|------|-------------|
| GET | /contracts-groups | List contracts and groups |

### contracts
| Method | Path | Description |
|--------|------|-------------|
| GET | /contracts/{contractId}/groups/{groupId}/selectable-hostnames | List available hostnames for a new configuration |

### cves
| Method | Path | Description |
|--------|------|-------------|
| GET | /cves | List CVEs |
| POST | /cves/subscribe | Subscribe to CVEs |
| GET | /cves/subscribed | List subscribed CVEs |
| POST | /cves/unsubscribe | Unsubscribe from CVEs |
| GET | /cves/{cveId} | Get a CVE |
| GET | /cves/{cveId}/security-coverage | Get CVE coverage |

### export
| Method | Path | Description |
|--------|------|-------------|
| GET | /export/configs/{configId}/versions/{versionNumber} | Export a configuration version |

### hostname-coverage
| Method | Path | Description |
|--------|------|-------------|
| GET | /hostname-coverage | Get hostname coverage |

### onboardings
| Method | Path | Description |
|--------|------|-------------|
| POST | /onboardings | Create an onboarding |
| GET | /onboardings | List onboardings |
| GET | /onboardings/{onboardingId} | Get an onboarding |
| DELETE | /onboardings/{onboardingId} | Delete an onboarding |
| POST | /onboardings/{onboardingId}/activations | Activate an onboarding |
| GET | /onboardings/{onboardingId}/activations/{activationId} | Get an onboarding activation |
| GET | /onboardings/{onboardingId}/certificate-validation | List onboarding certificate challenges |
| POST | /onboardings/{onboardingId}/certificate-validation/validate | Validate onboarding certificate |
| GET | /onboardings/{onboardingId}/cname-to-akamai | List hostname CNAME DNS records |
| POST | /onboardings/{onboardingId}/cname-to-akamai/validate | Validate hostname CNAME DNS records |
| GET | /onboardings/{onboardingId}/origin-validation | List origin hostname DNS records |
| POST | /onboardings/{onboardingId}/origin-validation/skip | Skip origin hostnames DNS record validation |
| POST | /onboardings/{onboardingId}/origin-validation/validate | Validate origin hostnames DNS records |
| GET | /onboardings/{onboardingId}/settings | Get onboarding settings |
| PUT | /onboardings/{onboardingId}/settings | Modify onboarding settings |

### siem-definitions
| Method | Path | Description |
|--------|------|-------------|
| GET | /siem-definitions | Get SIEM versions |

## Enhanced Skill Content
## Question Mapping

- "How do I activate a security configuration to production?" -> POST /activations
- "What is the status of my activation?" -> GET /activations/{activationId}
- "List all my security configurations" -> GET /configs
- "What security policies exist in this config version?" -> GET /configs/{configId}/versions/{versionNumber}/security-policies
- "How do I create a new rate policy to throttle abusive clients?" -> POST /configs/{configId}/versions/{versionNumber}/rate-policies
- "Which hostnames are protected by my configuration?" -> GET /configs/{configId}/versions/{versionNumber}/selected-hostnames
- "How do I block traffic from a specific country?" -> PUT /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/ip-geo-firewall
- "What CVEs is my configuration vulnerable to?" -> GET /cves
- "How do I check if a specific CVE is covered by my WAF rules?" -> GET /cves/{cveId}/security-coverage
- "How do I export a full snapshot of my security config?" -> GET /export/configs/{configId}/versions/{versionNumber}
- "What APIs has Akamai discovered on my traffic?" -> GET /api-discovery
- "How do I create a new version of my config before making changes?" -> POST /configs/{configId}/versions
- "What are the tuning recommendations for my security policy?" -> GET /configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/recommendations
- "How do I set up SIEM integration for security events?" -> PUT /configs/{configId}/versions/{versionNumber}/siem
- "How do I onboard a new hostname with security protections?" -> POST /onboardings

## Response Tips

- **Activations**: POST may return 200 (immediate) or 202 (async with `statusId`) -- poll `GET /activations/status/{statusId}` until 303 redirect to the completed activation resource.
- **Configs & Versions**: `GET /configs/{configId}/versions` is paginated via `page` and `pageSize` (default 25); always check `totalSize` against returned `versionList` length. The response nests `production` and `staging` status maps inside each version.
- **Security Policies**: Deeply nested under `/configs/{configId}/versions/{versionNumber}/security-policies/{policyId}/...` -- always confirm you have the correct `configId`, `versionNumber`, and `policyId` triple before mutating.
- **Rate Policies**: The `evaluation` nested object contains a separate set of thresholds for A/B testing; check `evaluationStatus` to know if an eval is active.
- **CVEs**: The `impactScore` is a float (CVSS-style); `coverage` is a string status, not a boolean -- parse it as an enum.
- **Match Targets**: Responses split into `apiTargets` and `websiteTargets` arrays inside a `matchTargets` wrapper object -- do not assume a flat list.
- **Onboardings**: Multi-step flow returns `currentStep`/`totalSteps` plus a `nextSteps` array with actionable links; follow `onboardingLink` URIs for navigation.
- **Errors**: 403 consistently means Forbidden (permissions issue with your API client credentials); 400 may include structured validation detail -- surface the error body, not just the status code.

## Anomaly Flags

- **Activation stuck in pending**: If `GET /activations/{activationId}` returns `status` other than `ACTIVATED` or `FAILED` for more than 30 minutes, surface a warning that the activation may be stalled.
- **Eval mode expiring soon**: When `GET .../security-policies/{policyId}/mode` shows `eval: true` with an `expires` datetime approaching, alert the user to finalize eval decisions before auto-expiry.
- **Rate policy evaluation active**: If any rate policy has `evaluation.evaluationStatus` set to an active state, flag that changes to thresholds will not take effect until the evaluation is applied or discarded via `PUT .../rate-policies/{ratePolicyId}/evaluation`.
- **Unmatched hostnames**: If `GET /hostname-coverage` returns entries with `hasMatchTarget: false`, proactively warn that those hostnames have no security policy coverage.
- **Version drift**: If `latestVersion` from `GET /configs/{configId}` significantly exceeds `productionVersion` or `stagingVersion`, flag that many undeployed changes exist.
- **CVE subscription gaps**: If `GET /cves` returns CVEs with `impactSeverity` of "HIGH" or "CRITICAL" that are not in `GET /cves/subscribed`, recommend subscribing for update notifications.
- **403 Forbidden on write operations**: Surface immediately as an API credential permissions issue -- the user likely needs to update their API client authorization grants.
- **Config with no security policies**: If `GET .../security-policies` returns an empty `policies` array, warn that the config version has no active protection.

## Playbook

### 1. Create and Activate a New Security Configuration

1. List available contracts and groups: `GET /contracts-groups`
2. Get selectable hostnames for your contract: `GET /contracts/{contractId}/groups/{groupId}/selectable-hostnames`
3. Create the configuration: `POST /configs` with `name`, `description`, and `hostnames`
4. Note the returned `configId` -- the first version is created automatically
5. Add a security policy: `POST /configs/{configId}/versions/1/security-policies` with `policyName` and `policyPrefix`
6. Configure protections on the policy: `PUT .../security-policies/{policyId}/protections` enabling desired controls
7. Set selected hostnames for the policy: `PUT .../security-policies/{policyId}/selected-hostnames`
8. Activate to staging first: `POST /activations` with `network: "STAGING"` and your `configId`/`configVersion`
9. Poll activation status until complete, then repeat for `network: "PRODUCTION"`

### 2. Tune WAF Rules Using Recommendations

1. Identify your config, version, and policy: `GET /configs` then `GET /configs/{configId}/versions/{versionNumber}/security-policies`
2. Retrieve recommendations: `GET .../security-policies/{policyId}/recommendations`
3. Review `ruleRecommendations` and `attackGroupRecommendations` arrays for suggested action changes
4. For each recommendation you agree with: `POST .../security-policies/{policyId}/recommendations` with `action: "ACCEPT"` and the `selectorId`
5. For false-positive rules, decline instead: `action: "DECLINE"`
6. Create a new version and activate to apply changes

### 3. Investigate and Mitigate a CVE

1. Check all known CVEs: `GET /cves` (optionally filter with `modifiedAfter` for recent ones)
2. Get details on the specific CVE: `GET /cves/{cveId}` -- review `impactSeverity`, `description`, and `mitigation.attackGroups`
3. Check your coverage: `GET /cves/{cveId}/security-coverage` to see which configs/policies already protect against it
4. If gaps exist, update the relevant attack group actions: `PUT .../security-policies/{policyId}/attack-groups/{attackGroupId}` with `action: "deny"`
5. Subscribe for future updates: `POST /cves/subscribe` with the CVE ID
6. Activate the updated config version to production

### 4. Set Up Rate Limiting

1. Create a new config version: `POST /configs/{configId}/versions` with `createFromVersion` set to the current active version
2. Create a rate policy: `POST .../rate-policies` specifying `averageThreshold`, `burstThreshold`, `clientIdentifier` (e.g., `"ip"`), and `matchType`
3. Assign the rate policy action to your security policy: `PUT .../security-policies/{policyId}/rate-policies/{ratePolicyId}` with `ipv4Action` and `ipv6Action` (e.g., `"deny"`)
4. Optionally set up an evaluation period on the policy: include the `evaluation` object with separate thresholds to test before enforcing
5. Activate to staging: `POST /activations` with `network: "STAGING"`
6. Monitor results, then apply or discard the evaluation: `PUT .../rate-policies/{ratePolicyId}/evaluation` with `action: "APPLY"` or `"DISCARD"`
7. Activate to production when satisfied

### 5. Onboard a New Hostname End-to-End

1. Start onboarding: `POST /onboardings` with `contractId`, `groupId`, and `hostnames`
2. Configure settings: `PUT /onboardings/{onboardingId}/settings` with certificate, delivery origin, and security policy details
3. Validate the origin: `POST /onboardings/{onboardingId}/origin-validation/validate` (or skip with `.../skip` for known-good origins)
4. Validate the certificate: `POST /onboardings/{onboardingId}/certificate-validation/validate` -- check that all DNS records return valid status
5. Activate to staging: `POST /onboardings/{onboardingId}/activations` with `network: "STAGING"` -- poll `GET .../activations/{activationId}` until `activationStatus` is complete
6. Validate CNAME pointing: `POST /onboardings/{onboardingId}/cname-to-akamai/validate` to confirm DNS is pointing to Akamai
7. Activate to production: repeat the activation step with `network: "PRODUCTION"`
8. Verify coverage: `GET /hostname-coverage` to confirm `hasMatchTarget: true` for your new hostname


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object
- Error responses use types: [Conflict](https, [Forbidden](https, [Invalid](https, [Unauthorized](https

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
