---
name: etsi-gs-mec-010-2-part-2-application-lifecycle-rules-and-requirements-management
description: "ETSI GS MEC 010-2 - Part 2: Application lifecycle, rules and requirements management API skill. Use when working with ETSI GS MEC 010-2 - Part 2: Application lifecycle, rules and requirements management for app_packages, subscriptions, user_defined_notification. Covers 16 endpoints."
version: 1.0.0
generator: lapsh
---

# ETSI GS MEC 010-2 - Part 2: Application lifecycle, rules and requirements management
API version: 2.1.1

## Auth
No authentication required.

## Base URL
https://localhost/app_pkgm/v1

## Setup
1. No auth setup needed
2. GET /app_packages -- verify access
3. POST /app_packages -- create first app_packages

## Endpoints

16 endpoints across 4 groups. See references/api-spec.lap for full details.

### app_packages
| Method | Path | Description |
|--------|------|-------------|
| POST | /app_packages | Create a resource for on-boarding an application package to a MEO |
| GET | /app_packages | Queries information relating to on-boarded application packages in the MEO |
| GET | /app_packages/{appPkgId} | Queries the information related to individual application package resources |
| DELETE | /app_packages/{appPkgId} | Deletes an individual application package resources |
| PATCH | /app_packages/{appPkgId} | Updates the operational state of an individual application package resource |
| GET | /app_packages/{appPkgId}/appd | Reads the content of the AppD of on-boarded individual application package resources. |
| GET | /app_packages/{appPkgId}/package_content | Fetch the onboarded application package content identified by appPkgId or appDId. |
| PUT | /app_packages/{appPkgId}/package_content | Uploads the content of application package. |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| POST | /subscriptions | Subscribe to notifications about on-boarding an application package |
| GET | /subscriptions | used to retrieve the information of subscriptions to individual application package resource in MEO |
| GET | /subscriptions/{subscriptionId} | Used to represent an individual subscription to notifications about application package changes. |
| DELETE | /subscriptions/{subscriptionId} | Deletes the individual subscription to notifications about application package changes in MEO. |

### user_defined_notification
| Method | Path | Description |
|--------|------|-------------|
| POST | /user_defined_notification | Registers a notification endpoint to notify application package operations |

### onboarded_app_packages
| Method | Path | Description |
|--------|------|-------------|
| GET | /onboarded_app_packages/{appDId}/appd | Reads the content of the AppD of on-boarded individual application package resources. |
| GET | /onboarded_app_packages/{appDId}/package_content | Fetch the onboarded application package content identified by appPkgId or appDId. |
| PUT | /onboarded_app_packages/{appDId}/package_content | Uploads the content of application package. |

## Enhanced Skill Content
## Question Mapping

- "How do I onboard a new app package?" -> POST /app_packages
- "List all available app packages" -> GET /app_packages
- "Get details for a specific app package" -> GET /app_packages/{appPkgId}
- "How do I delete an app package?" -> DELETE /app_packages/{appPkgId}
- "How do I disable an app package?" -> PATCH /app_packages/{appPkgId}
- "How do I re-enable a disabled app package?" -> PATCH /app_packages/{appPkgId}
- "Download the package content for an app" -> GET /app_packages/{appPkgId}/package_content
- "Upload package content to an app package" -> PUT /app_packages/{appPkgId}/package_content
- "Retrieve the app descriptor (AppD) for a package" -> GET /app_packages/{appPkgId}/appd
- "Subscribe to notifications when packages are onboarded or deleted" -> POST /subscriptions
- "List all my notification subscriptions" -> GET /subscriptions
- "Unsubscribe from package notifications" -> DELETE /subscriptions/{subscriptionId}
- "Get the AppD for an already-onboarded package by appDId" -> GET /onboarded_app_packages/{appDId}/appd
- "Send a custom notification about a package lifecycle event" -> POST /user_defined_notification
- "Filter app packages by provider or name" -> GET /app_packages (use `filter` query param)

## Response Tips

- **App packages (GET list/detail):** Response includes `onboardingState`, `operationalState`, and `usageState` enums -- always check these before acting on a package. The `_links` object contains HATEOAS URIs for `appD` and `appPkgContent`.
- **Package content (GET):** May return 200 (full content) or 206 (partial/range response) -- handle both; a 416 means your Range header was unsatisfiable.
- **Subscriptions:** The `subscriptionType` field uses specific enum values (`AppPackageOnBoarding`, `AppPacakgeOperationChange`, `AppPackageDeletion`) -- note the typos are in the spec itself, match them exactly.
- **DELETE operations:** Return 204 with no body -- treat any non-204 as failure.
- **POST creates:** Return 201 with the created resource; inspect `_links.self.href` for the canonical URL of the new resource.
- **Errors:** All endpoints share a common error set (400/401/403/404/406/429); 409 appears only on PATCH and PUT when there is a state conflict.

## Anomaly Flags

- **429 Too Many Requests:** All endpoints can return 429. Surface rate-limit headers proactively and recommend backoff before retrying.
- **409 Conflict on PATCH/PUT:** Indicates the package is in a state that prevents the requested change (e.g., trying to upload content to an already-onboarded package, or enabling a package mid-deletion). Surface the current `operationalState`/`onboardingState` to explain why.
- **Subscription typos in spec:** The enum values contain known misspellings (`subsctiptionType`, `AppPacakgeOperationChange`, `AppPacakgeEnabled`, `AppPacakgeDisabled`). Flag if the server rejects a corrected spelling -- the typo may be required.
- **206 Partial Content without Range request:** If a GET on package_content returns 206 unexpectedly, the package may be large. Alert the user they may need to handle chunked downloads.
- **operationalState DISABLED:** When listing packages, proactively flag any that are DISABLED, as they may require attention or re-enablement.
- **onboardingState not terminal:** If a package remains in a non-final onboarding state across multiple polls, surface it as potentially stuck.

## Playbook

### Onboard and Upload a New App Package

1. POST /app_packages with `appPkgName`, `appPkgPath`, `appPkgVersion`, and `checksum` (algorithm + hash)
2. Note the returned `appPkgId` from the 201 response
3. PUT /app_packages/{appPkgId}/package_content to upload the actual package binary
4. GET /app_packages/{appPkgId} to confirm `onboardingState` has progressed
5. PATCH /app_packages/{appPkgId} with `operationState: "ENABLED"` to activate it

### Subscribe to Package Lifecycle Events

1. POST /subscriptions with `callbackUri` (your webhook URL) and `subsctiptionType` set to the desired event type
2. Optionally include `appPkgFilter` to scope notifications to specific packages
3. Note the returned `subscriptionId` for future management
4. GET /subscriptions/{subscriptionId} to verify the subscription is active
5. When done, DELETE /subscriptions/{subscriptionId} to clean up

### Disable and Remove an App Package

1. GET /app_packages/{appPkgId} to check current `usageState` -- must not be IN_USE
2. PATCH /app_packages/{appPkgId} with `operationState: "DISABLED"` to prevent new usage
3. Wait for any active sessions to drain (poll GET /app_packages/{appPkgId} and check `usageState`)
4. DELETE /app_packages/{appPkgId} -- returns 204 on success

### Retrieve App Descriptor via Two Paths

1. If you have the `appPkgId` (pre-onboarding or any state): GET /app_packages/{appPkgId}/appd
2. If you have the `appDId` (post-onboarding): GET /onboarded_app_packages/{appDId}/appd
3. Use `filter`, `fields`, or `exclude_fields` query params to narrow the returned descriptor content

### Audit All Packages and Their States

1. GET /app_packages with no filters to retrieve the full list
2. For each package, inspect `onboardingState`, `operationalState`, and `usageState`
3. Flag any packages where `operationalState` is DISABLED or `onboardingState` is not ONBOARDED
4. For packages needing attention, GET /app_packages/{appPkgId} for full details including `softwareImages` and `checksum`
5. Optionally use `filter` param on subsequent calls to narrow results to specific states


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
