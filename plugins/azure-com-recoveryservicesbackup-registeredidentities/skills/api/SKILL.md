---
name: recoveryservicesbackupclient
description: "RecoveryServicesBackupClient API skill. Use when working with RecoveryServicesBackupClient for subscriptions. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# RecoveryServicesBackupClient
API version: 2016-06-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.RecoveryServices/vaults/{vaultName}/registeredIdentities/{identityName} | Unregisters the given container from your Recovery Services vault. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Delete a registeredIdentity?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.RecoveryServices/vaults/{vaultName}/registeredIdentities/{identityName}
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
