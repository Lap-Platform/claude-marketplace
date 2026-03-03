---
name: deploymentadminclient
description: "DeploymentAdminClient API skill. Use when working with DeploymentAdminClient for subscriptions. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# DeploymentAdminClient
API version: 2019-01-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId}/secrets -- verify access
3. POST /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId}/secrets/{secretName}/import -- create first import

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId}/secrets | Returns an array of product secrets. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId}/secrets/{secretName} | Returns the specific product secret. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId}/secrets/{secretName}/import | Imports a product secret. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId}/secrets/{secretName}/validate | Validates a product secret. |

## Enhanced Skill Content
## Question Mapping

- "What secrets exist for this product package?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId}/secrets
- "List all secrets in a deployment package" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId}/secrets
- "Get details for a specific secret" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId}/secrets/{secretName}
- "What is the value of secret X in package Y?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId}/secrets/{secretName}
- "Import a secret into a product package" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId}/secrets/{secretName}/import
- "Add a new secret to a deployment package" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId}/secrets/{secretName}/import
- "Upload a certificate or key to this package" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId}/secrets/{secretName}/import
- "Is this secret valid?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId}/secrets/{secretName}/validate
- "Validate secret parameters before importing" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId}/secrets/{secretName}/validate
- "Check if a certificate is well-formed and not expired" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId}/secrets/{secretName}/validate
- "Rotate a secret in a product package" -> POST .../secrets/{secretName}/validate then POST .../secrets/{secretName}/import (multi-step)
- "Does this package have any secrets configured?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId}/secrets
- "Verify my secret parameters are correct before deploying" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/productPackages/{packageId}/secrets/{secretName}/validate

## Response Tips

- **Secret listing (GET .../secrets):** Response is typically an Azure `value[]` array with optional `nextLink` for pagination; iterate `nextLink` until null to collect all results.
- **Secret detail (GET .../secrets/{secretName}):** Returns a single resource object with `properties` nested under the top level; check `properties.secretKind` and `properties.expiresAfter` for expiration metadata.
- **Import (POST .../import):** Returns the updated secret resource on 200; a 4xx with an `error.code` and `error.message` body indicates invalid parameters or permission issues.
- **Validate (POST .../validate):** A 200 response means validation passed; failures surface as error responses with structured `error.details[]` describing each validation problem.

## Anomaly Flags

- **Expiring secrets:** Surface proactively when a secret's expiration timestamp is within 30 days or already past.
- **Validation failures before import:** If a validate call returns errors, flag them before the user attempts an import with the same parameters.
- **Throttling (429 responses):** Azure ARM APIs enforce rate limits per subscription; surface `Retry-After` headers and warn when multiple 429s occur in sequence.
- **Missing or empty secrets list:** If a package returns zero secrets, flag this as potentially misconfigured -- most packages expect at least one secret.
- **Long-running operations:** If any response returns a 202 with an `Azure-AsyncOperation` header instead of 200, surface the polling URL and estimated wait.
- **Deprecated API version:** If response headers include `Sunset` or `x-ms-deprecation`, alert the user to migrate to a newer API version.

## Playbook

### 1. Audit All Secrets in a Product Package

1. Call GET `.../productPackages/{packageId}/secrets` to list all secrets.
2. Follow any `nextLink` pagination until the full list is collected.
3. For each secret, call GET `.../secrets/{secretName}` to retrieve full details.
4. Check `properties.expiresAfter` or expiration fields and flag any nearing expiry.
5. Compile results into a summary table of secret names, kinds, and expiration status.

### 2. Safely Import a New Secret (Validate-then-Import)

1. Prepare the `secretParameters` map with the required key material and metadata.
2. Call POST `.../secrets/{secretName}/validate` with the parameters.
3. Inspect the response: if 200, proceed; if errors, fix parameters and re-validate.
4. Call POST `.../secrets/{secretName}/import` with the validated parameters.
5. Confirm the 200 response and verify the returned secret resource matches expectations.

### 3. Rotate an Existing Secret

1. Call GET `.../secrets/{secretName}` to retrieve the current secret and note its properties.
2. Prepare new `secretParameters` with the replacement key material.
3. Call POST `.../secrets/{secretName}/validate` to pre-check the new parameters.
4. On successful validation, call POST `.../secrets/{secretName}/import` to overwrite with the new secret.
5. Call GET `.../secrets/{secretName}` again to confirm the update took effect.

### 4. Troubleshoot a Failed Secret Import

1. Call POST `.../secrets/{secretName}/validate` with the same parameters that failed import.
2. Review `error.details[]` in the response for specific validation failures (wrong format, expired cert, missing fields).
3. If validation passes but import fails, check subscription-level permissions with a GET on the secrets list.
4. Verify the `packageId` and `secretName` path parameters are correct by listing all secrets.
5. Retry the import after correcting identified issues.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
