---
name: okta-admin-management
description: "Okta Admin Management API skill. Use when working with Okta Admin Management for .well-known, api, attack-protection. Covers 705 endpoints."
version: 1.0.0
generator: lapsh
---

# Okta Admin Management
API version: 5.1.0

## Auth
ApiKey Authorization in header | OAuth2

## Base URL
https://{yourOktaDomain}

## Setup
1. Set your API key in the appropriate header
2. GET /.well-known/app-authenticator-configuration -- verify access
3. POST /api/v1/agentPools/{poolId}/updates -- create first updates

## Endpoints

705 endpoints across 10 groups. See references/api-spec.lap for full details.

### .well-known
| Method | Path | Description |
|--------|------|-------------|
| GET | /.well-known/app-authenticator-configuration | Retrieve the well-known app authenticator configuration |
| GET | /.well-known/apple-app-site-association | Retrieve the customized apple-app-site-association URI content |
| GET | /.well-known/assetlinks.json | Retrieve the customized assetlinks.json URI content |
| GET | /.well-known/okta-organization | Retrieve the Org metadata |
| GET | /.well-known/ssf-configuration | Retrieve the SSF transmitter metadata |
| GET | /.well-known/webauthn | Retrieve the customized webauthn URI content |

### api
| Method | Path | Description |
|--------|------|-------------|
| GET | /api/v1/agentPools | List all agent pools |
| GET | /api/v1/agentPools/{poolId}/updates | List all agent pool updates |
| POST | /api/v1/agentPools/{poolId}/updates | Create an agent pool update |
| GET | /api/v1/agentPools/{poolId}/updates/settings | Retrieve an agent pool update's settings |
| POST | /api/v1/agentPools/{poolId}/updates/settings | Update an agent pool update settings |
| GET | /api/v1/agentPools/{poolId}/updates/{updateId} | Retrieve an agent pool update by ID |
| POST | /api/v1/agentPools/{poolId}/updates/{updateId} | Update an agent pool update by ID |
| DELETE | /api/v1/agentPools/{poolId}/updates/{updateId} | Delete an agent pool update |
| POST | /api/v1/agentPools/{poolId}/updates/{updateId}/activate | Activate an agent pool update |
| POST | /api/v1/agentPools/{poolId}/updates/{updateId}/deactivate | Deactivate an agent pool update |
| POST | /api/v1/agentPools/{poolId}/updates/{updateId}/pause | Pause an agent pool update |
| POST | /api/v1/agentPools/{poolId}/updates/{updateId}/resume | Resume an agent pool update |
| POST | /api/v1/agentPools/{poolId}/updates/{updateId}/retry | Retry an agent pool update |
| POST | /api/v1/agentPools/{poolId}/updates/{updateId}/stop | Stop an agent pool update |
| GET | /api/v1/api-tokens | List all API token metadata |
| DELETE | /api/v1/api-tokens/current | Revoke the current API token |
| GET | /api/v1/api-tokens/{apiTokenId} | Retrieve an API token's metadata |
| PUT | /api/v1/api-tokens/{apiTokenId} | Upsert an API token network condition |
| DELETE | /api/v1/api-tokens/{apiTokenId} | Revoke an API token |
| GET | /api/v1/apps | List all applications |
| POST | /api/v1/apps | Create an application |
| GET | /api/v1/apps/{appId} | Retrieve an application |
| PUT | /api/v1/apps/{appId} | Replace an application |
| DELETE | /api/v1/apps/{appId} | Delete an application |
| GET | /api/v1/apps/{appId}/connections/default | Retrieve the default provisioning connection |
| POST | /api/v1/apps/{appId}/connections/default | Update the default provisioning connection |
| GET | /api/v1/apps/{appId}/connections/default/jwks | Retrieve a JSON Web Key Set (JWKS) for the default provisioning connection |
| POST | /api/v1/apps/{appId}/connections/default/lifecycle/activate | Activate the default provisioning connection |
| POST | /api/v1/apps/{appId}/connections/default/lifecycle/deactivate | Deactivate the default provisioning connection |
| GET | /api/v1/apps/{appId}/credentials/csrs | List all certificate signing requests |
| POST | /api/v1/apps/{appId}/credentials/csrs | Generate a certificate signing request |
| GET | /api/v1/apps/{appId}/credentials/csrs/{csrId} | Retrieve a certificate signing request |
| DELETE | /api/v1/apps/{appId}/credentials/csrs/{csrId} | Revoke a certificate signing request |
| POST | /api/v1/apps/{appId}/credentials/csrs/{csrId}/lifecycle/publish | Publish a certificate signing request |
| GET | /api/v1/apps/{appId}/credentials/jwks | List all the OAuth 2.0 client JSON Web Keys |
| POST | /api/v1/apps/{appId}/credentials/jwks | Add a JSON Web Key |
| GET | /api/v1/apps/{appId}/credentials/jwks/{keyId} | Retrieve an OAuth 2.0 client JSON Web Key |
| DELETE | /api/v1/apps/{appId}/credentials/jwks/{keyId} | Delete an OAuth 2.0 client JSON Web Key |
| POST | /api/v1/apps/{appId}/credentials/jwks/{keyId}/lifecycle/activate | Activate an OAuth 2.0 client JSON Web Key |
| POST | /api/v1/apps/{appId}/credentials/jwks/{keyId}/lifecycle/deactivate | Deactivate an OAuth 2.0 client JSON Web Key |
| GET | /api/v1/apps/{appId}/credentials/keys | List all key credentials |
| POST | /api/v1/apps/{appId}/credentials/keys/generate | Generate a key credential |
| GET | /api/v1/apps/{appId}/credentials/keys/{keyId} | Retrieve a key credential |
| POST | /api/v1/apps/{appId}/credentials/keys/{keyId}/clone | Clone a key credential |
| GET | /api/v1/apps/{appId}/credentials/secrets | List all OAuth 2.0 client secrets |
| POST | /api/v1/apps/{appId}/credentials/secrets | Create an OAuth 2.0 client secret |
| GET | /api/v1/apps/{appId}/credentials/secrets/{secretId} | Retrieve an OAuth 2.0 client secret |
| DELETE | /api/v1/apps/{appId}/credentials/secrets/{secretId} | Delete an OAuth 2.0 client secret |
| POST | /api/v1/apps/{appId}/credentials/secrets/{secretId}/lifecycle/activate | Activate an OAuth 2.0 client secret |
| POST | /api/v1/apps/{appId}/credentials/secrets/{secretId}/lifecycle/deactivate | Deactivate an OAuth 2.0 client secret |
| GET | /api/v1/apps/{appId}/cwo/connections | Retrieve all Cross App Access connections |
| POST | /api/v1/apps/{appId}/cwo/connections | Create a Cross App Access connection |
| GET | /api/v1/apps/{appId}/cwo/connections/{connectionId} | Retrieve a Cross App Access connection |
| PATCH | /api/v1/apps/{appId}/cwo/connections/{connectionId} | Update a Cross App Access connection |
| DELETE | /api/v1/apps/{appId}/cwo/connections/{connectionId} | Delete a Cross App Access connection |
| GET | /api/v1/apps/{appId}/features | List all features |
| GET | /api/v1/apps/{appId}/features/{featureName} | Retrieve a feature |
| PUT | /api/v1/apps/{appId}/features/{featureName} | Update a feature |
| GET | /api/v1/apps/{appId}/federated-claims | List all configured federated claims |
| POST | /api/v1/apps/{appId}/federated-claims | Create a federated claim |
| GET | /api/v1/apps/{appId}/federated-claims/{claimId} | Retrieve a federated claim |
| PUT | /api/v1/apps/{appId}/federated-claims/{claimId} | Replace a federated claim |
| DELETE | /api/v1/apps/{appId}/federated-claims/{claimId} | Delete a federated claim |
| GET | /api/v1/apps/{appId}/grants | List all app grants |
| POST | /api/v1/apps/{appId}/grants | Grant consent to scope |
| GET | /api/v1/apps/{appId}/grants/{grantId} | Retrieve an app grant |
| DELETE | /api/v1/apps/{appId}/grants/{grantId} | Revoke an app grant |
| GET | /api/v1/apps/{appId}/group-push/mappings | List all group push mappings |
| POST | /api/v1/apps/{appId}/group-push/mappings | Create a group push mapping |
| GET | /api/v1/apps/{appId}/group-push/mappings/{mappingId} | Retrieve a group push mapping |
| PATCH | /api/v1/apps/{appId}/group-push/mappings/{mappingId} | Update a group push mapping |
| DELETE | /api/v1/apps/{appId}/group-push/mappings/{mappingId} | Delete a group push mapping |
| GET | /api/v1/apps/{appId}/groups | List all application groups |
| GET | /api/v1/apps/{appId}/groups/{groupId} | Retrieve an application group |
| PUT | /api/v1/apps/{appId}/groups/{groupId} | Assign an application group |
| PATCH | /api/v1/apps/{appId}/groups/{groupId} | Update an application group |
| DELETE | /api/v1/apps/{appId}/groups/{groupId} | Unassign an application group |
| POST | /api/v1/apps/{appId}/lifecycle/activate | Activate an application |
| POST | /api/v1/apps/{appId}/lifecycle/deactivate | Deactivate an application |
| POST | /api/v1/apps/{appId}/logo | Upload an application logo |
| PUT | /api/v1/apps/{appId}/policies/{policyId} | Assign an authentication policy |
| GET | /api/v1/apps/{appId}/sso/saml/metadata | Preview the application SAML metadata |
| GET | /api/v1/apps/{appId}/tokens | List all application refresh tokens |
| DELETE | /api/v1/apps/{appId}/tokens | Revoke all application tokens |
| GET | /api/v1/apps/{appId}/tokens/{tokenId} | Retrieve an application token |
| DELETE | /api/v1/apps/{appId}/tokens/{tokenId} | Revoke an application token |
| GET | /api/v1/apps/{appId}/users | List all application users |
| POST | /api/v1/apps/{appId}/users | Assign an application user |
| GET | /api/v1/apps/{appId}/users/{userId} | Retrieve an application user |
| POST | /api/v1/apps/{appId}/users/{userId} | Update an application user |
| DELETE | /api/v1/apps/{appId}/users/{userId} | Unassign an application user |
| POST | /api/v1/apps/{appName}/{appId}/oauth2/callback | Verify the provisioning connection |
| GET | /api/v1/authenticators | List all authenticators |
| POST | /api/v1/authenticators | Create an authenticator |
| GET | /api/v1/authenticators/{authenticatorId} | Retrieve an authenticator |
| PUT | /api/v1/authenticators/{authenticatorId} | Replace an authenticator |
| GET | /api/v1/authenticators/{authenticatorId}/aaguids | List all custom AAGUIDs |
| POST | /api/v1/authenticators/{authenticatorId}/aaguids | Create a custom AAGUID |
| GET | /api/v1/authenticators/{authenticatorId}/aaguids/{aaguid} | Retrieve a custom AAGUID |
| PUT | /api/v1/authenticators/{authenticatorId}/aaguids/{aaguid} | Replace a custom AAGUID |
| PATCH | /api/v1/authenticators/{authenticatorId}/aaguids/{aaguid} | Update a custom AAGUID |
| DELETE | /api/v1/authenticators/{authenticatorId}/aaguids/{aaguid} | Delete a custom AAGUID |
| POST | /api/v1/authenticators/{authenticatorId}/lifecycle/activate | Activate an authenticator |
| POST | /api/v1/authenticators/{authenticatorId}/lifecycle/deactivate | Deactivate an authenticator |
| GET | /api/v1/authenticators/{authenticatorId}/methods | List all methods of an authenticator |
| GET | /api/v1/authenticators/{authenticatorId}/methods/{methodType} | Retrieve an authenticator method |
| PUT | /api/v1/authenticators/{authenticatorId}/methods/{methodType} | Replace an authenticator method |
| POST | /api/v1/authenticators/{authenticatorId}/methods/{methodType}/lifecycle/activate | Activate an authenticator method |
| POST | /api/v1/authenticators/{authenticatorId}/methods/{methodType}/lifecycle/deactivate | Deactivate an authenticator method |
| GET | /api/v1/authorizationServers | List all authorization servers |
| POST | /api/v1/authorizationServers | Create an authorization server |
| GET | /api/v1/authorizationServers/{authServerId} | Retrieve an authorization server |
| PUT | /api/v1/authorizationServers/{authServerId} | Replace an authorization server |
| DELETE | /api/v1/authorizationServers/{authServerId} | Delete an authorization server |
| GET | /api/v1/authorizationServers/{authServerId}/associatedServers | List all associated authorization servers |
| POST | /api/v1/authorizationServers/{authServerId}/associatedServers | Create an associated authorization server |
| DELETE | /api/v1/authorizationServers/{authServerId}/associatedServers/{associatedServerId} | Delete an associated authorization server |
| GET | /api/v1/authorizationServers/{authServerId}/claims | List all custom token claims |
| POST | /api/v1/authorizationServers/{authServerId}/claims | Create a custom token claim |
| GET | /api/v1/authorizationServers/{authServerId}/claims/{claimId} | Retrieve a custom token claim |
| PUT | /api/v1/authorizationServers/{authServerId}/claims/{claimId} | Replace a custom token claim |
| DELETE | /api/v1/authorizationServers/{authServerId}/claims/{claimId} | Delete a custom token claim |
| GET | /api/v1/authorizationServers/{authServerId}/clients | List all client resources for an authorization server |
| GET | /api/v1/authorizationServers/{authServerId}/clients/{clientId}/tokens | List all refresh tokens for a client |
| DELETE | /api/v1/authorizationServers/{authServerId}/clients/{clientId}/tokens | Revoke all refresh tokens for a client |
| GET | /api/v1/authorizationServers/{authServerId}/clients/{clientId}/tokens/{tokenId} | Retrieve a refresh token for a client |
| DELETE | /api/v1/authorizationServers/{authServerId}/clients/{clientId}/tokens/{tokenId} | Revoke a refresh token for a client |
| GET | /api/v1/authorizationServers/{authServerId}/credentials/keys | List all credential keys |
| GET | /api/v1/authorizationServers/{authServerId}/credentials/keys/{keyId} | Retrieve an authorization server key |
| POST | /api/v1/authorizationServers/{authServerId}/credentials/lifecycle/keyRotate | Rotate all credential keys |
| POST | /api/v1/authorizationServers/{authServerId}/lifecycle/activate | Activate an authorization server |
| POST | /api/v1/authorizationServers/{authServerId}/lifecycle/deactivate | Deactivate an authorization server |
| GET | /api/v1/authorizationServers/{authServerId}/policies | List all policies |
| POST | /api/v1/authorizationServers/{authServerId}/policies | Create a policy |
| GET | /api/v1/authorizationServers/{authServerId}/policies/{policyId} | Retrieve a policy |
| PUT | /api/v1/authorizationServers/{authServerId}/policies/{policyId} | Replace a policy |
| DELETE | /api/v1/authorizationServers/{authServerId}/policies/{policyId} | Delete a policy |
| POST | /api/v1/authorizationServers/{authServerId}/policies/{policyId}/lifecycle/activate | Activate a policy |
| POST | /api/v1/authorizationServers/{authServerId}/policies/{policyId}/lifecycle/deactivate | Deactivate a policy |
| GET | /api/v1/authorizationServers/{authServerId}/policies/{policyId}/rules | List all policy rules |
| POST | /api/v1/authorizationServers/{authServerId}/policies/{policyId}/rules | Create a policy rule |
| GET | /api/v1/authorizationServers/{authServerId}/policies/{policyId}/rules/{ruleId} | Retrieve a policy rule |
| PUT | /api/v1/authorizationServers/{authServerId}/policies/{policyId}/rules/{ruleId} | Replace a policy rule |
| DELETE | /api/v1/authorizationServers/{authServerId}/policies/{policyId}/rules/{ruleId} | Delete a policy rule |
| POST | /api/v1/authorizationServers/{authServerId}/policies/{policyId}/rules/{ruleId}/lifecycle/activate | Activate a policy rule |
| POST | /api/v1/authorizationServers/{authServerId}/policies/{policyId}/rules/{ruleId}/lifecycle/deactivate | Deactivate a policy rule |
| GET | /api/v1/authorizationServers/{authServerId}/resourceservercredentials/keys | List all Custom Authorization Server Public JSON Web Keys |
| POST | /api/v1/authorizationServers/{authServerId}/resourceservercredentials/keys | Add a JSON Web Key |
| GET | /api/v1/authorizationServers/{authServerId}/resourceservercredentials/keys/{keyId} | Retrieve a Custom Authorization Server Public JSON Web Key |
| DELETE | /api/v1/authorizationServers/{authServerId}/resourceservercredentials/keys/{keyId} | Delete a Custom Authorization Server Public JSON Web Key |
| POST | /api/v1/authorizationServers/{authServerId}/resourceservercredentials/keys/{keyId}/lifecycle/activate | Activate a Custom Authorization Server Public JSON Web Key |
| POST | /api/v1/authorizationServers/{authServerId}/resourceservercredentials/keys/{keyId}/lifecycle/deactivate | Deactivate a Custom Authorization Server Public JSON Web Key |
| GET | /api/v1/authorizationServers/{authServerId}/scopes | List all custom token scopes |
| POST | /api/v1/authorizationServers/{authServerId}/scopes | Create a custom token scope |
| GET | /api/v1/authorizationServers/{authServerId}/scopes/{scopeId} | Retrieve a custom token scope |
| PUT | /api/v1/authorizationServers/{authServerId}/scopes/{scopeId} | Replace a custom token scope |
| DELETE | /api/v1/authorizationServers/{authServerId}/scopes/{scopeId} | Delete a custom token scope |
| GET | /api/v1/behaviors | List all behavior detection rules |
| POST | /api/v1/behaviors | Create a behavior detection rule |
| GET | /api/v1/behaviors/{behaviorId} | Retrieve a behavior detection rule |
| PUT | /api/v1/behaviors/{behaviorId} | Replace a behavior detection rule |
| DELETE | /api/v1/behaviors/{behaviorId} | Delete a behavior detection rule |
| POST | /api/v1/behaviors/{behaviorId}/lifecycle/activate | Activate a behavior detection rule |
| POST | /api/v1/behaviors/{behaviorId}/lifecycle/deactivate | Deactivate a behavior detection rule |
| GET | /api/v1/brands | List all brands |
| POST | /api/v1/brands | Create a brand |
| GET | /api/v1/brands/{brandId} | Retrieve a brand |
| PUT | /api/v1/brands/{brandId} | Replace a brand |
| DELETE | /api/v1/brands/{brandId} | Delete a brand |
| GET | /api/v1/brands/{brandId}/domains | List all domains associated with a brand |
| GET | /api/v1/brands/{brandId}/pages/error | Retrieve the error page sub-resources |
| GET | /api/v1/brands/{brandId}/pages/error/customized | Retrieve the customized error page |
| PUT | /api/v1/brands/{brandId}/pages/error/customized | Replace the customized error page |
| DELETE | /api/v1/brands/{brandId}/pages/error/customized | Delete the customized error page |
| GET | /api/v1/brands/{brandId}/pages/error/default | Retrieve the default error page |
| GET | /api/v1/brands/{brandId}/pages/error/preview | Retrieve the preview error page preview |
| PUT | /api/v1/brands/{brandId}/pages/error/preview | Replace the preview error page |
| DELETE | /api/v1/brands/{brandId}/pages/error/preview | Delete the preview error page |
| GET | /api/v1/brands/{brandId}/pages/sign-in | Retrieve the sign-in page sub-resources |
| GET | /api/v1/brands/{brandId}/pages/sign-in/customized | Retrieve the customized sign-in page |
| PUT | /api/v1/brands/{brandId}/pages/sign-in/customized | Replace the customized sign-in page |
| DELETE | /api/v1/brands/{brandId}/pages/sign-in/customized | Delete the customized sign-in page |
| GET | /api/v1/brands/{brandId}/pages/sign-in/default | Retrieve the default sign-in page |
| GET | /api/v1/brands/{brandId}/pages/sign-in/preview | Retrieve the preview sign-in page preview |
| PUT | /api/v1/brands/{brandId}/pages/sign-in/preview | Replace the preview sign-in page |
| DELETE | /api/v1/brands/{brandId}/pages/sign-in/preview | Delete the preview sign-in page |
| GET | /api/v1/brands/{brandId}/pages/sign-in/widget-versions | List all Sign-In Widget versions |
| GET | /api/v1/brands/{brandId}/pages/sign-out/customized | Retrieve the sign-out page settings |
| PUT | /api/v1/brands/{brandId}/pages/sign-out/customized | Replace the sign-out page settings |
| GET | /api/v1/brands/{brandId}/templates/email | List all email templates |
| GET | /api/v1/brands/{brandId}/templates/email/{templateName} | Retrieve an email template |
| GET | /api/v1/brands/{brandId}/templates/email/{templateName}/customizations | List all email customizations |
| POST | /api/v1/brands/{brandId}/templates/email/{templateName}/customizations | Create an email customization |
| DELETE | /api/v1/brands/{brandId}/templates/email/{templateName}/customizations | Delete all email customizations |
| GET | /api/v1/brands/{brandId}/templates/email/{templateName}/customizations/{customizationId} | Retrieve an email customization |
| PUT | /api/v1/brands/{brandId}/templates/email/{templateName}/customizations/{customizationId} | Replace an email customization |
| DELETE | /api/v1/brands/{brandId}/templates/email/{templateName}/customizations/{customizationId} | Delete an email customization |
| GET | /api/v1/brands/{brandId}/templates/email/{templateName}/customizations/{customizationId}/preview | Retrieve a preview of an email customization |
| GET | /api/v1/brands/{brandId}/templates/email/{templateName}/default-content | Retrieve an email template default content |
| GET | /api/v1/brands/{brandId}/templates/email/{templateName}/default-content/preview | Retrieve a preview of the email template default content |
| GET | /api/v1/brands/{brandId}/templates/email/{templateName}/settings | Retrieve the email template settings |
| PUT | /api/v1/brands/{brandId}/templates/email/{templateName}/settings | Replace the email template settings |
| POST | /api/v1/brands/{brandId}/templates/email/{templateName}/test | Send a test email |
| GET | /api/v1/brands/{brandId}/themes | List all themes |
| GET | /api/v1/brands/{brandId}/themes/{themeId} | Retrieve a theme |
| PUT | /api/v1/brands/{brandId}/themes/{themeId} | Replace a theme |
| POST | /api/v1/brands/{brandId}/themes/{themeId}/background-image | Upload the background image |
| DELETE | /api/v1/brands/{brandId}/themes/{themeId}/background-image | Delete the background image |
| POST | /api/v1/brands/{brandId}/themes/{themeId}/favicon | Upload the favicon |
| DELETE | /api/v1/brands/{brandId}/themes/{themeId}/favicon | Delete the favicon |
| POST | /api/v1/brands/{brandId}/themes/{themeId}/logo | Upload the logo |
| DELETE | /api/v1/brands/{brandId}/themes/{themeId}/logo | Delete the logo |
| GET | /api/v1/brands/{brandId}/well-known-uris | Retrieve all the well-known URIs |
| GET | /api/v1/brands/{brandId}/well-known-uris/{path} | Retrieve the well-known URI of a specific brand |
| GET | /api/v1/brands/{brandId}/well-known-uris/{path}/customized | Retrieve the customized content of the specified well-known URI |
| PUT | /api/v1/brands/{brandId}/well-known-uris/{path}/customized | Replace the customized well-known URI of the specific path |
| GET | /api/v1/captchas | List all CAPTCHA instances |
| POST | /api/v1/captchas | Create a CAPTCHA instance |
| GET | /api/v1/captchas/{captchaId} | Retrieve a CAPTCHA instance |
| POST | /api/v1/captchas/{captchaId} | Update a CAPTCHA instance |
| PUT | /api/v1/captchas/{captchaId} | Replace a CAPTCHA instance |
| DELETE | /api/v1/captchas/{captchaId} | Delete a CAPTCHA instance |
| GET | /api/v1/device-assurances | List all device assurance policies |
| POST | /api/v1/device-assurances | Create a device assurance policy |
| GET | /api/v1/device-assurances/{deviceAssuranceId} | Retrieve a device assurance policy |
| PUT | /api/v1/device-assurances/{deviceAssuranceId} | Replace a device assurance policy |
| DELETE | /api/v1/device-assurances/{deviceAssuranceId} | Delete a device assurance policy |
| GET | /api/v1/device-integrations | List all device integrations |
| GET | /api/v1/device-integrations/{deviceIntegrationId} | Retrieve a device integration |
| POST | /api/v1/device-integrations/{deviceIntegrationId}/lifecycle/activate | Activate a device integration |
| POST | /api/v1/device-integrations/{deviceIntegrationId}/lifecycle/deactivate | Deactivate a device integration |
| GET | /api/v1/device-posture-checks | List all device posture checks |
| POST | /api/v1/device-posture-checks | Create a device posture check |
| GET | /api/v1/device-posture-checks/default | List all default device posture checks |
| GET | /api/v1/device-posture-checks/{postureCheckId} | Retrieve a device posture check |
| PUT | /api/v1/device-posture-checks/{postureCheckId} | Replace a device posture check |
| DELETE | /api/v1/device-posture-checks/{postureCheckId} | Delete a device posture check |
| GET | /api/v1/devices | List all devices |
| GET | /api/v1/devices/{deviceId} | Retrieve a device |
| DELETE | /api/v1/devices/{deviceId} | Delete a device |
| POST | /api/v1/devices/{deviceId}/lifecycle/activate | Activate a device |
| POST | /api/v1/devices/{deviceId}/lifecycle/deactivate | Deactivate a device |
| POST | /api/v1/devices/{deviceId}/lifecycle/suspend | Suspend a Device |
| POST | /api/v1/devices/{deviceId}/lifecycle/unsuspend | Unsuspend a Device |
| GET | /api/v1/devices/{deviceId}/users | List all users for a device |
| POST | /api/v1/directories/{appInstanceId}/groups/modify | Update an Active Directory group membership |
| GET | /api/v1/domains | List all Custom Domains |
| POST | /api/v1/domains | Create a Custom Domain |
| GET | /api/v1/domains/{domainId} | Retrieve a custom domain |
| PUT | /api/v1/domains/{domainId} | Replace a custom domain's brand |
| DELETE | /api/v1/domains/{domainId} | Delete a custom domain |
| PUT | /api/v1/domains/{domainId}/certificate | Upsert the custom domain's certificate |
| POST | /api/v1/domains/{domainId}/verify | Verify a custom domain |
| GET | /api/v1/email-domains | List all email domains |
| POST | /api/v1/email-domains | Create an email domain |
| GET | /api/v1/email-domains/{emailDomainId} | Retrieve an email domain |
| PUT | /api/v1/email-domains/{emailDomainId} | Replace an email domain |
| DELETE | /api/v1/email-domains/{emailDomainId} | Delete an email domain |
| POST | /api/v1/email-domains/{emailDomainId}/verify | Verify an email domain |
| GET | /api/v1/email-servers | List all enrolled SMTP servers |
| POST | /api/v1/email-servers | Create a custom SMTP server |
| GET | /api/v1/email-servers/{emailServerId} | Retrieve an SMTP server configuration |
| PATCH | /api/v1/email-servers/{emailServerId} | Update an SMTP server configuration |
| DELETE | /api/v1/email-servers/{emailServerId} | Delete an SMTP server configuration |
| POST | /api/v1/email-servers/{emailServerId}/test | Test an SMTP server configuration |
| GET | /api/v1/eventHooks | List all event hooks |
| POST | /api/v1/eventHooks | Create an event hook |
| GET | /api/v1/eventHooks/{eventHookId} | Retrieve an event hook |
| PUT | /api/v1/eventHooks/{eventHookId} | Replace an event hook |
| DELETE | /api/v1/eventHooks/{eventHookId} | Delete an event hook |
| POST | /api/v1/eventHooks/{eventHookId}/lifecycle/activate | Activate an event hook |
| POST | /api/v1/eventHooks/{eventHookId}/lifecycle/deactivate | Deactivate an event hook |
| POST | /api/v1/eventHooks/{eventHookId}/lifecycle/verify | Verify an event hook |
| GET | /api/v1/features | List all features |
| GET | /api/v1/features/{featureId} | Retrieve a feature |
| GET | /api/v1/features/{featureId}/dependencies | List all dependencies |
| GET | /api/v1/features/{featureId}/dependents | List all dependents |
| POST | /api/v1/features/{featureId}/{lifecycle} | Update a feature lifecycle |
| GET | /api/v1/first-party-app-settings/{appName} | Retrieve the Okta application settings |
| PUT | /api/v1/first-party-app-settings/{appName} | Replace the Okta application settings |
| GET | /api/v1/groups | List all groups |
| POST | /api/v1/groups | Add a group |
| GET | /api/v1/groups/rules | List all group rules |
| POST | /api/v1/groups/rules | Create a group rule |
| GET | /api/v1/groups/rules/{groupRuleId} | Retrieve a group rule |
| PUT | /api/v1/groups/rules/{groupRuleId} | Replace a group rule |
| DELETE | /api/v1/groups/rules/{groupRuleId} | Delete a group rule |
| POST | /api/v1/groups/rules/{groupRuleId}/lifecycle/activate | Activate a group rule |
| POST | /api/v1/groups/rules/{groupRuleId}/lifecycle/deactivate | Deactivate a group rule |
| GET | /api/v1/groups/{groupId} | Retrieve a group |
| PUT | /api/v1/groups/{groupId} | Replace a group |
| DELETE | /api/v1/groups/{groupId} | Delete a group |
| GET | /api/v1/groups/{groupId}/apps | List all assigned apps |
| GET | /api/v1/groups/{groupId}/owners | List all group owners |
| POST | /api/v1/groups/{groupId}/owners | Assign a group owner |
| DELETE | /api/v1/groups/{groupId}/owners/{ownerId} | Delete a group owner |
| GET | /api/v1/groups/{groupId}/roles | List all group role assignments |
| POST | /api/v1/groups/{groupId}/roles | Assign a role to a group |
| GET | /api/v1/groups/{groupId}/roles/{roleAssignmentId} | Retrieve a group role assignment |
| DELETE | /api/v1/groups/{groupId}/roles/{roleAssignmentId} | Unassign a group role |
| GET | /api/v1/groups/{groupId}/roles/{roleAssignmentId}/targets/catalog/apps | List all group role app targets |
| PUT | /api/v1/groups/{groupId}/roles/{roleAssignmentId}/targets/catalog/apps/{appName} | Assign a group role app target |
| DELETE | /api/v1/groups/{groupId}/roles/{roleAssignmentId}/targets/catalog/apps/{appName} | Unassign a group role app target |
| PUT | /api/v1/groups/{groupId}/roles/{roleAssignmentId}/targets/catalog/apps/{appName}/{appId} | Assign a group role app instance target |
| DELETE | /api/v1/groups/{groupId}/roles/{roleAssignmentId}/targets/catalog/apps/{appName}/{appId} | Unassign a group role app instance target |
| GET | /api/v1/groups/{groupId}/roles/{roleAssignmentId}/targets/groups | List all group role group targets |
| PUT | /api/v1/groups/{groupId}/roles/{roleAssignmentId}/targets/groups/{targetGroupId} | Assign a group role group target |
| DELETE | /api/v1/groups/{groupId}/roles/{roleAssignmentId}/targets/groups/{targetGroupId} | Unassign a group role group target |
| GET | /api/v1/groups/{groupId}/users | List all member users |
| PUT | /api/v1/groups/{groupId}/users/{userId} | Assign a user to a group |
| DELETE | /api/v1/groups/{groupId}/users/{userId} | Unassign a user from a group |
| GET | /api/v1/hook-keys | List all keys |
| POST | /api/v1/hook-keys | Create a key |
| GET | /api/v1/hook-keys/public/{keyId} | Retrieve a public key |
| GET | /api/v1/hook-keys/{id} | Retrieve a key by ID |
| PUT | /api/v1/hook-keys/{id} | Replace a key |
| DELETE | /api/v1/hook-keys/{id} | Delete a key |
| GET | /api/v1/iam/assignees/users | List all users with role assignments |
| GET | /api/v1/iam/governance/bundles | List all governance bundles for the Admin Console |
| POST | /api/v1/iam/governance/bundles | Create a governance bundle for the Admin Console in RAMP |
| GET | /api/v1/iam/governance/bundles/{bundleId} | Retrieve a governance bundle from RAMP |
| PUT | /api/v1/iam/governance/bundles/{bundleId} | Replace a governance bundle in RAMP |
| DELETE | /api/v1/iam/governance/bundles/{bundleId} | Delete a governance bundle from RAMP |
| GET | /api/v1/iam/governance/bundles/{bundleId}/entitlements | List all entitlements for a governance bundle |
| GET | /api/v1/iam/governance/bundles/{bundleId}/entitlements/{entitlementId}/values | List all entitlement values for a bundle entitlement |
| GET | /api/v1/iam/governance/optIn | Retrieve the opt-in status from RAMP |
| POST | /api/v1/iam/governance/optIn | Opt in the Admin Console to RAMP |
| POST | /api/v1/iam/governance/optOut | Opt out the Admin Console from RAMP |
| GET | /api/v1/iam/resource-sets | List all resource sets |
| POST | /api/v1/iam/resource-sets | Create a resource set |
| GET | /api/v1/iam/resource-sets/{resourceSetIdOrLabel} | Retrieve a resource set |
| PUT | /api/v1/iam/resource-sets/{resourceSetIdOrLabel} | Replace a resource set |
| DELETE | /api/v1/iam/resource-sets/{resourceSetIdOrLabel} | Delete a resource set |
| GET | /api/v1/iam/resource-sets/{resourceSetIdOrLabel}/bindings | List all role resource set bindings |
| POST | /api/v1/iam/resource-sets/{resourceSetIdOrLabel}/bindings | Create a role resource set binding |
| GET | /api/v1/iam/resource-sets/{resourceSetIdOrLabel}/bindings/{roleIdOrLabel} | Retrieve a role resource set binding |
| DELETE | /api/v1/iam/resource-sets/{resourceSetIdOrLabel}/bindings/{roleIdOrLabel} | Delete a role resource set binding |
| GET | /api/v1/iam/resource-sets/{resourceSetIdOrLabel}/bindings/{roleIdOrLabel}/members | List all role resource set binding members |
| PATCH | /api/v1/iam/resource-sets/{resourceSetIdOrLabel}/bindings/{roleIdOrLabel}/members | Add more role resource set binding members |
| GET | /api/v1/iam/resource-sets/{resourceSetIdOrLabel}/bindings/{roleIdOrLabel}/members/{memberId} | Retrieve a role resource set binding member |
| DELETE | /api/v1/iam/resource-sets/{resourceSetIdOrLabel}/bindings/{roleIdOrLabel}/members/{memberId} | Unassign a role resource set binding member |
| GET | /api/v1/iam/resource-sets/{resourceSetIdOrLabel}/resources | List all resource set resources |
| POST | /api/v1/iam/resource-sets/{resourceSetIdOrLabel}/resources | Add a resource set resource with conditions |
| PATCH | /api/v1/iam/resource-sets/{resourceSetIdOrLabel}/resources | Add more resources to a resource set |
| GET | /api/v1/iam/resource-sets/{resourceSetIdOrLabel}/resources/{resourceId} | Retrieve a resource set resource |
| PUT | /api/v1/iam/resource-sets/{resourceSetIdOrLabel}/resources/{resourceId} | Replace the resource set resource conditions |
| DELETE | /api/v1/iam/resource-sets/{resourceSetIdOrLabel}/resources/{resourceId} | Delete a resource set resource |
| GET | /api/v1/iam/roles | List all custom roles |
| POST | /api/v1/iam/roles | Create a custom role |
| GET | /api/v1/iam/roles/{roleIdOrLabel} | Retrieve a role |
| PUT | /api/v1/iam/roles/{roleIdOrLabel} | Replace a custom role |
| DELETE | /api/v1/iam/roles/{roleIdOrLabel} | Delete a custom role |
| GET | /api/v1/iam/roles/{roleIdOrLabel}/permissions | List all custom role permissions |
| GET | /api/v1/iam/roles/{roleIdOrLabel}/permissions/{permissionType} | Retrieve a custom role permission |
| POST | /api/v1/iam/roles/{roleIdOrLabel}/permissions/{permissionType} | Create a custom role permission |
| PUT | /api/v1/iam/roles/{roleIdOrLabel}/permissions/{permissionType} | Replace a custom role permission |
| DELETE | /api/v1/iam/roles/{roleIdOrLabel}/permissions/{permissionType} | Delete a custom role permission |
| GET | /api/v1/identity-sources/{identitySourceId}/sessions | List all identity source sessions |
| POST | /api/v1/identity-sources/{identitySourceId}/sessions | Create an identity source session |
| GET | /api/v1/identity-sources/{identitySourceId}/sessions/{sessionId} | Retrieve an identity source session |
| DELETE | /api/v1/identity-sources/{identitySourceId}/sessions/{sessionId} | Delete an identity source session |
| POST | /api/v1/identity-sources/{identitySourceId}/sessions/{sessionId}/bulk-delete | Upload the data to be deleted in Okta |
| POST | /api/v1/identity-sources/{identitySourceId}/sessions/{sessionId}/bulk-upsert | Upload the data to be upserted in Okta |
| POST | /api/v1/identity-sources/{identitySourceId}/sessions/{sessionId}/start-import | Start the import from the identity source |
| GET | /api/v1/idps | List all IdPs |
| POST | /api/v1/idps | Create an IdP |
| GET | /api/v1/idps/credentials/keys | List all IdP key credentials |
| POST | /api/v1/idps/credentials/keys | Create an IdP key credential |
| GET | /api/v1/idps/credentials/keys/{kid} | Retrieve an IdP key credential |
| PUT | /api/v1/idps/credentials/keys/{kid} | Replace an IdP key credential |
| DELETE | /api/v1/idps/credentials/keys/{kid} | Delete an IdP key credential |
| GET | /api/v1/idps/{idpId} | Retrieve an IdP |
| PUT | /api/v1/idps/{idpId} | Replace an IdP |
| DELETE | /api/v1/idps/{idpId} | Delete an IdP |
| GET | /api/v1/idps/{idpId}/credentials/csrs | List all certificate signing requests |
| POST | /api/v1/idps/{idpId}/credentials/csrs | Generate a certificate signing request |
| GET | /api/v1/idps/{idpId}/credentials/csrs/{idpCsrId} | Retrieve a certificate signing request |
| DELETE | /api/v1/idps/{idpId}/credentials/csrs/{idpCsrId} | Revoke a certificate signing request |
| POST | /api/v1/idps/{idpId}/credentials/csrs/{idpCsrId}/lifecycle/publish | Publish a certificate signing request |
| GET | /api/v1/idps/{idpId}/credentials/keys | List all signing key credentials for IdP |
| GET | /api/v1/idps/{idpId}/credentials/keys/active | List the active signing key credential for IdP |
| POST | /api/v1/idps/{idpId}/credentials/keys/generate | Generate a new signing key credential for IdP |
| GET | /api/v1/idps/{idpId}/credentials/keys/{kid} | Retrieve a signing key credential for IdP |
| POST | /api/v1/idps/{idpId}/credentials/keys/{kid}/clone | Clone a signing key credential for IdP |
| POST | /api/v1/idps/{idpId}/lifecycle/activate | Activate an IdP |
| POST | /api/v1/idps/{idpId}/lifecycle/deactivate | Deactivate an IdP |
| GET | /api/v1/idps/{idpId}/users | List all users for IdP |
| GET | /api/v1/idps/{idpId}/users/{userId} | Retrieve a user for IdP |
| POST | /api/v1/idps/{idpId}/users/{userId} | Link a user to IdP |
| DELETE | /api/v1/idps/{idpId}/users/{userId} | Unlink a user from IdP |
| GET | /api/v1/idps/{idpId}/users/{userId}/credentials/tokens | List all tokens from OIDC IdP |
| GET | /api/v1/inlineHooks | List all inline hooks |
| POST | /api/v1/inlineHooks | Create an inline hook |
| GET | /api/v1/inlineHooks/{inlineHookId} | Retrieve an inline hook |
| POST | /api/v1/inlineHooks/{inlineHookId} | Update an inline hook |
| PUT | /api/v1/inlineHooks/{inlineHookId} | Replace an inline hook |
| DELETE | /api/v1/inlineHooks/{inlineHookId} | Delete an inline hook |
| POST | /api/v1/inlineHooks/{inlineHookId}/execute | Execute an inline hook |
| POST | /api/v1/inlineHooks/{inlineHookId}/lifecycle/activate | Activate an inline hook |
| POST | /api/v1/inlineHooks/{inlineHookId}/lifecycle/deactivate | Deactivate an inline hook |
| GET | /api/v1/logStreams | List all log streams |
| POST | /api/v1/logStreams | Create a log stream |
| GET | /api/v1/logStreams/{logStreamId} | Retrieve a log stream |
| PUT | /api/v1/logStreams/{logStreamId} | Replace a log stream |
| DELETE | /api/v1/logStreams/{logStreamId} | Delete a log stream |
| POST | /api/v1/logStreams/{logStreamId}/lifecycle/activate | Activate a log stream |
| POST | /api/v1/logStreams/{logStreamId}/lifecycle/deactivate | Deactivate a log stream |
| GET | /api/v1/logs | List all System Log events |
| GET | /api/v1/mappings | List all profile mappings |
| GET | /api/v1/mappings/{mappingId} | Retrieve a profile mapping |
| POST | /api/v1/mappings/{mappingId} | Update a profile mapping |
| GET | /api/v1/meta/schemas/apps/{appId}/default | Retrieve the default app user schema for an app |
| POST | /api/v1/meta/schemas/apps/{appId}/default | Update the app user profile schema for an app |
| GET | /api/v1/meta/schemas/group/default | Retrieve the default group schema |
| POST | /api/v1/meta/schemas/group/default | Update the group profile schema |
| GET | /api/v1/meta/schemas/logStream | List the log stream schemas |
| GET | /api/v1/meta/schemas/logStream/{logStreamType} | Retrieve the log stream schema for the schema type |
| GET | /api/v1/meta/schemas/user/linkedObjects | List all linked object definitions |
| POST | /api/v1/meta/schemas/user/linkedObjects | Create a linked object definition |
| GET | /api/v1/meta/schemas/user/linkedObjects/{linkedObjectName} | Retrieve a linked object definition |
| DELETE | /api/v1/meta/schemas/user/linkedObjects/{linkedObjectName} | Delete a linked object definition |
| GET | /api/v1/meta/schemas/user/{schemaId} | Retrieve a user schema |
| POST | /api/v1/meta/schemas/user/{schemaId} | Update a user schema |
| GET | /api/v1/meta/types/user | List all user types |
| POST | /api/v1/meta/types/user | Create a user type |
| GET | /api/v1/meta/types/user/{typeId} | Retrieve a user type |
| POST | /api/v1/meta/types/user/{typeId} | Update a user type |
| PUT | /api/v1/meta/types/user/{typeId} | Replace a user type |
| DELETE | /api/v1/meta/types/user/{typeId} | Delete a user type |
| GET | /api/v1/meta/uischemas | List all UI schemas |
| POST | /api/v1/meta/uischemas | Create a UI schema |
| GET | /api/v1/meta/uischemas/{id} | Retrieve a UI schema |
| PUT | /api/v1/meta/uischemas/{id} | Replace a UI schema |
| DELETE | /api/v1/meta/uischemas/{id} | Delete a UI schema |
| GET | /api/v1/org | Retrieve the Org general settings |
| POST | /api/v1/org | Update the Org general settings |
| PUT | /api/v1/org | Replace the Org general settings |
| GET | /api/v1/org/captcha | Retrieve the org-wide CAPTCHA settings |
| PUT | /api/v1/org/captcha | Replace the org-wide CAPTCHA settings |
| DELETE | /api/v1/org/captcha | Delete the org-wide CAPTCHA settings |
| GET | /api/v1/org/contacts | List all org contact types |
| GET | /api/v1/org/contacts/{contactType} | Retrieve the contact type user |
| PUT | /api/v1/org/contacts/{contactType} | Replace the contact type user |
| POST | /api/v1/org/email/bounces/remove-list | Remove bounced emails |
| GET | /api/v1/org/factors/yubikey_token/tokens | List all YubiKey OTP tokens |
| POST | /api/v1/org/factors/yubikey_token/tokens | Upload a YubiKey OTP seed |
| GET | /api/v1/org/factors/yubikey_token/tokens/{tokenId} | Retrieve a YubiKey OTP token |
| POST | /api/v1/org/logo | Upload the org logo |
| GET | /api/v1/org/orgSettings/thirdPartyAdminSetting | Retrieve the org third-party admin setting |
| POST | /api/v1/org/orgSettings/thirdPartyAdminSetting | Update the org third-party admin setting |
| GET | /api/v1/org/preferences | Retrieve the org preferences |
| POST | /api/v1/org/preferences/hideEndUserFooter | Set the hide dashboard footer preference |
| POST | /api/v1/org/preferences/showEndUserFooter | Set the show dashboard footer preference |
| GET | /api/v1/org/privacy/aerial | Retrieve Okta Aerial consent for your org |
| POST | /api/v1/org/privacy/aerial/grant | Grant Okta Aerial access to your org |
| POST | /api/v1/org/privacy/aerial/revoke | Revoke Okta Aerial access to your org |
| GET | /api/v1/org/privacy/oktaCommunication | Retrieve the Okta communication settings |
| POST | /api/v1/org/privacy/oktaCommunication/optIn | Opt in to Okta user communication emails |
| POST | /api/v1/org/privacy/oktaCommunication/optOut | Opt out of Okta user communication emails |
| GET | /api/v1/org/privacy/oktaSupport | Retrieve the Okta Support settings |
| GET | /api/v1/org/privacy/oktaSupport/cases | List all Okta Support cases |
| PATCH | /api/v1/org/privacy/oktaSupport/cases/{caseNumber} | Update an Okta Support case |
| POST | /api/v1/org/privacy/oktaSupport/extend | Extend Okta Support access |
| POST | /api/v1/org/privacy/oktaSupport/grant | Grant Okta Support access |
| POST | /api/v1/org/privacy/oktaSupport/revoke | Revoke Okta Support access |
| GET | /api/v1/org/settings/autoAssignAdminAppSetting | Retrieve the Okta Admin Console assignment setting |
| POST | /api/v1/org/settings/autoAssignAdminAppSetting | Update the Okta Admin Console assignment setting |
| GET | /api/v1/org/settings/clientPrivilegesSetting | Retrieve the default public client app role setting |
| PUT | /api/v1/org/settings/clientPrivilegesSetting | Assign the default public client app role setting |
| POST | /api/v1/orgs | Create an org |
| GET | /api/v1/policies | List all policies |
| POST | /api/v1/policies | Create a policy |
| POST | /api/v1/policies/simulate | Create a policy simulation |
| GET | /api/v1/policies/{policyId} | Retrieve a policy |
| PUT | /api/v1/policies/{policyId} | Replace a policy |
| DELETE | /api/v1/policies/{policyId} | Delete a policy |
| GET | /api/v1/policies/{policyId}/app | List all apps mapped to a policy |
| POST | /api/v1/policies/{policyId}/clone | Clone an existing policy |
| POST | /api/v1/policies/{policyId}/lifecycle/activate | Activate a policy |
| POST | /api/v1/policies/{policyId}/lifecycle/deactivate | Deactivate a policy |
| GET | /api/v1/policies/{policyId}/mappings | List all resources mapped to a policy |
| POST | /api/v1/policies/{policyId}/mappings | Map a resource to a policy |
| GET | /api/v1/policies/{policyId}/mappings/{mappingId} | Retrieve a policy resource mapping |
| DELETE | /api/v1/policies/{policyId}/mappings/{mappingId} | Delete a policy resource mapping |
| GET | /api/v1/policies/{policyId}/rules | List all policy rules |
| POST | /api/v1/policies/{policyId}/rules | Create a policy rule |
| GET | /api/v1/policies/{policyId}/rules/{ruleId} | Retrieve a policy rule |
| PUT | /api/v1/policies/{policyId}/rules/{ruleId} | Replace a policy rule |
| DELETE | /api/v1/policies/{policyId}/rules/{ruleId} | Delete a policy rule |
| POST | /api/v1/policies/{policyId}/rules/{ruleId}/lifecycle/activate | Activate a policy rule |
| POST | /api/v1/policies/{policyId}/rules/{ruleId}/lifecycle/deactivate | Deactivate a policy rule |
| GET | /api/v1/principal-rate-limits | List all principal rate limits |
| POST | /api/v1/principal-rate-limits | Create a principal rate limit |
| GET | /api/v1/principal-rate-limits/{principalRateLimitId} | Retrieve a principal rate limit |
| PUT | /api/v1/principal-rate-limits/{principalRateLimitId} | Replace a principal rate limit |
| GET | /api/v1/push-providers | List all push providers |
| POST | /api/v1/push-providers | Create a push provider |
| GET | /api/v1/push-providers/{pushProviderId} | Retrieve a push provider |
| PUT | /api/v1/push-providers/{pushProviderId} | Replace a push provider |
| DELETE | /api/v1/push-providers/{pushProviderId} | Delete a push provider |
| GET | /api/v1/rate-limit-settings/admin-notifications | Retrieve the rate limit admin notification settings |
| PUT | /api/v1/rate-limit-settings/admin-notifications | Replace the rate limit admin notification settings |
| GET | /api/v1/rate-limit-settings/per-client | Retrieve the per-client rate limit settings |
| PUT | /api/v1/rate-limit-settings/per-client | Replace the per-client rate limit settings |
| GET | /api/v1/rate-limit-settings/warning-threshold | Retrieve the rate limit warning threshold percentage |
| PUT | /api/v1/rate-limit-settings/warning-threshold | Replace the rate limit warning threshold percentage |
| GET | /api/v1/realm-assignments | List all realm assignments |
| POST | /api/v1/realm-assignments | Create a realm assignment |
| GET | /api/v1/realm-assignments/operations | List all realm assignment operations |
| POST | /api/v1/realm-assignments/operations | Execute a realm assignment |
| GET | /api/v1/realm-assignments/{assignmentId} | Retrieve a realm assignment |
| PUT | /api/v1/realm-assignments/{assignmentId} | Replace a realm assignment |
| DELETE | /api/v1/realm-assignments/{assignmentId} | Delete a realm assignment |
| POST | /api/v1/realm-assignments/{assignmentId}/lifecycle/activate | Activate a realm assignment |
| POST | /api/v1/realm-assignments/{assignmentId}/lifecycle/deactivate | Deactivate a realm assignment |
| GET | /api/v1/realms | List all realms |
| POST | /api/v1/realms | Create a realm |
| GET | /api/v1/realms/{realmId} | Retrieve a realm |
| PUT | /api/v1/realms/{realmId} | Replace the realm profile |
| DELETE | /api/v1/realms/{realmId} | Delete a realm |
| POST | /api/v1/risk/events/ip | Send multiple risk events |
| GET | /api/v1/risk/providers | List all risk providers |
| POST | /api/v1/risk/providers | Create a risk provider |
| GET | /api/v1/risk/providers/{riskProviderId} | Retrieve a risk provider |
| PUT | /api/v1/risk/providers/{riskProviderId} | Replace a risk provider |
| DELETE | /api/v1/risk/providers/{riskProviderId} | Delete a risk provider |
| GET | /api/v1/roles/{roleRef}/subscriptions | List all subscriptions for a role |
| GET | /api/v1/roles/{roleRef}/subscriptions/{notificationType} | Retrieve a subscription for a role |
| POST | /api/v1/roles/{roleRef}/subscriptions/{notificationType}/subscribe | Subscribe a role to a specific notification type |
| POST | /api/v1/roles/{roleRef}/subscriptions/{notificationType}/unsubscribe | Unsubscribe a role from a specific notification type |
| GET | /api/v1/security-events-providers | List all security events providers |
| POST | /api/v1/security-events-providers | Create a security events provider |
| GET | /api/v1/security-events-providers/{securityEventProviderId} | Retrieve the security events provider |
| PUT | /api/v1/security-events-providers/{securityEventProviderId} | Replace a security events provider |
| DELETE | /api/v1/security-events-providers/{securityEventProviderId} | Delete a security events provider |
| POST | /api/v1/security-events-providers/{securityEventProviderId}/lifecycle/activate | Activate a security events provider |
| POST | /api/v1/security-events-providers/{securityEventProviderId}/lifecycle/deactivate | Deactivate a security events provider |
| POST | /api/v1/sessions | Create a session with session token |
| GET | /api/v1/sessions/me | Retrieve the current session |
| DELETE | /api/v1/sessions/me | Close the current session |
| POST | /api/v1/sessions/me/lifecycle/refresh | Refresh the current session |
| GET | /api/v1/sessions/{sessionId} | Retrieve a session |
| DELETE | /api/v1/sessions/{sessionId} | Revoke a session |
| POST | /api/v1/sessions/{sessionId}/lifecycle/refresh | Refresh a session |
| GET | /api/v1/ssf/stream | Retrieve the SSF stream configuration(s) |
| POST | /api/v1/ssf/stream | Create an SSF stream |
| PUT | /api/v1/ssf/stream | Replace an SSF stream |
| PATCH | /api/v1/ssf/stream | Update an SSF stream |
| DELETE | /api/v1/ssf/stream | Delete an SSF stream |
| GET | /api/v1/ssf/stream/status | Retrieve the SSF Stream status |
| POST | /api/v1/ssf/stream/verification | Verify an SSF stream |
| GET | /api/v1/templates/sms | List all SMS templates |
| POST | /api/v1/templates/sms | Create an SMS template |
| GET | /api/v1/templates/sms/{templateId} | Retrieve an SMS template |
| POST | /api/v1/templates/sms/{templateId} | Update an SMS template |
| PUT | /api/v1/templates/sms/{templateId} | Replace an SMS template |
| DELETE | /api/v1/templates/sms/{templateId} | Delete an SMS template |
| GET | /api/v1/threats/configuration | Retrieve the ThreatInsight configuration |
| POST | /api/v1/threats/configuration | Update the ThreatInsight configuration |
| GET | /api/v1/trustedOrigins | List all trusted origins |
| POST | /api/v1/trustedOrigins | Create a trusted origin |
| GET | /api/v1/trustedOrigins/{trustedOriginId} | Retrieve a trusted origin |
| PUT | /api/v1/trustedOrigins/{trustedOriginId} | Replace a trusted origin |
| DELETE | /api/v1/trustedOrigins/{trustedOriginId} | Delete a trusted origin |
| POST | /api/v1/trustedOrigins/{trustedOriginId}/lifecycle/activate | Activate a trusted origin |
| POST | /api/v1/trustedOrigins/{trustedOriginId}/lifecycle/deactivate | Deactivate a trusted origin |
| GET | /api/v1/users | List all users |
| POST | /api/v1/users | Create a user |
| POST | /api/v1/users/me/lifecycle/delete_sessions | End a current user session |
| GET | /api/v1/users/{id} | Retrieve a user |
| POST | /api/v1/users/{id} | Update a user |
| PUT | /api/v1/users/{id} | Replace a user |
| DELETE | /api/v1/users/{id} | Delete a user |
| GET | /api/v1/users/{id}/appLinks | List all assigned app links |
| GET | /api/v1/users/{id}/blocks | List all user blocks |
| GET | /api/v1/users/{id}/groups | List all groups |
| GET | /api/v1/users/{id}/idps | List all IdPs for user |
| POST | /api/v1/users/{id}/lifecycle/activate | Activate a user |
| POST | /api/v1/users/{id}/lifecycle/deactivate | Deactivate a user |
| POST | /api/v1/users/{id}/lifecycle/expire_password | Expire the password |
| POST | /api/v1/users/{id}/lifecycle/expire_password_with_temp_password | Expire the password with a temporary password |
| POST | /api/v1/users/{id}/lifecycle/reactivate | Reactivate a user |
| POST | /api/v1/users/{id}/lifecycle/reset_factors | Reset the factors |
| POST | /api/v1/users/{id}/lifecycle/reset_password | Reset a password |
| POST | /api/v1/users/{id}/lifecycle/suspend | Suspend a user |
| POST | /api/v1/users/{id}/lifecycle/unlock | Unlock a user |
| POST | /api/v1/users/{id}/lifecycle/unsuspend | Unsuspend a user |
| PUT | /api/v1/users/{userIdOrLogin}/linkedObjects/{primaryRelationshipName}/{primaryUserId} | Assign a linked object value for primary |
| GET | /api/v1/users/{userIdOrLogin}/linkedObjects/{relationshipName} | List the primary or all of the associated linked object values |
| DELETE | /api/v1/users/{userIdOrLogin}/linkedObjects/{relationshipName} | Delete a linked object value |
| GET | /api/v1/users/{userId}/authenticator-enrollments | List all authenticator enrollments |
| POST | /api/v1/users/{userId}/authenticator-enrollments/phone | Create an auto-activated Phone authenticator enrollment |
| POST | /api/v1/users/{userId}/authenticator-enrollments/tac | Create an auto-activated TAC authenticator enrollment |
| GET | /api/v1/users/{userId}/authenticator-enrollments/{enrollmentId} | Retrieve an authenticator enrollment |
| DELETE | /api/v1/users/{userId}/authenticator-enrollments/{enrollmentId} | Delete an authenticator enrollment |
| GET | /api/v1/users/{userId}/classification | Retrieve a user's classification |
| PUT | /api/v1/users/{userId}/classification | Replace the user's classification |
| GET | /api/v1/users/{userId}/clients | List all clients |
| GET | /api/v1/users/{userId}/clients/{clientId}/grants | List all grants for a client |
| DELETE | /api/v1/users/{userId}/clients/{clientId}/grants | Revoke all grants for a client |
| GET | /api/v1/users/{userId}/clients/{clientId}/tokens | List all refresh tokens for a client |
| DELETE | /api/v1/users/{userId}/clients/{clientId}/tokens | Revoke all refresh tokens for a client |
| GET | /api/v1/users/{userId}/clients/{clientId}/tokens/{tokenId} | Retrieve a refresh token for a client |
| DELETE | /api/v1/users/{userId}/clients/{clientId}/tokens/{tokenId} | Revoke a token for a client |
| POST | /api/v1/users/{userId}/credentials/change_password | Update password |
| POST | /api/v1/users/{userId}/credentials/change_recovery_question | Update recovery question |
| POST | /api/v1/users/{userId}/credentials/forgot_password | Start forgot password flow |
| POST | /api/v1/users/{userId}/credentials/forgot_password_recovery_question | Reset password with recovery question |
| GET | /api/v1/users/{userId}/devices | List all devices |
| GET | /api/v1/users/{userId}/factors | List all enrolled factors |
| POST | /api/v1/users/{userId}/factors | Enroll a factor |
| GET | /api/v1/users/{userId}/factors/catalog | List all supported factors |
| GET | /api/v1/users/{userId}/factors/questions | List all supported security questions |
| GET | /api/v1/users/{userId}/factors/{factorId} | Retrieve a factor |
| DELETE | /api/v1/users/{userId}/factors/{factorId} | Unenroll a factor |
| POST | /api/v1/users/{userId}/factors/{factorId}/lifecycle/activate | Activate a factor |
| POST | /api/v1/users/{userId}/factors/{factorId}/resend | Resend a factor enrollment |
| GET | /api/v1/users/{userId}/factors/{factorId}/transactions/{transactionId} | Retrieve a factor transaction status |
| POST | /api/v1/users/{userId}/factors/{factorId}/verify | Verify a factor |
| GET | /api/v1/users/{userId}/grants | List all user grants |
| DELETE | /api/v1/users/{userId}/grants | Revoke all user grants |
| GET | /api/v1/users/{userId}/grants/{grantId} | Retrieve a user grant |
| DELETE | /api/v1/users/{userId}/grants/{grantId} | Revoke a user grant |
| GET | /api/v1/users/{userId}/risk | Retrieve the user's risk |
| PUT | /api/v1/users/{userId}/risk | Upsert the user's risk |
| GET | /api/v1/users/{userId}/roles | List all user role assignments |
| POST | /api/v1/users/{userId}/roles | Assign a user role |
| GET | /api/v1/users/{userId}/roles/{roleAssignmentId} | Retrieve a user role assignment |
| DELETE | /api/v1/users/{userId}/roles/{roleAssignmentId} | Unassign a user role |
| GET | /api/v1/users/{userId}/roles/{roleAssignmentId}/governance | Retrieve all user role governance sources |
| GET | /api/v1/users/{userId}/roles/{roleAssignmentId}/governance/{grantId} | Retrieve a user role governance source |
| GET | /api/v1/users/{userId}/roles/{roleAssignmentId}/governance/{grantId}/resources | Retrieve the user role governance source resources |
| GET | /api/v1/users/{userId}/roles/{roleAssignmentId}/targets/catalog/apps | List all admin role app targets |
| PUT | /api/v1/users/{userId}/roles/{roleAssignmentId}/targets/catalog/apps | Assign all apps as target to admin role |
| PUT | /api/v1/users/{userId}/roles/{roleAssignmentId}/targets/catalog/apps/{appName} | Assign an admin role app target |
| DELETE | /api/v1/users/{userId}/roles/{roleAssignmentId}/targets/catalog/apps/{appName} | Unassign an admin role app target |
| PUT | /api/v1/users/{userId}/roles/{roleAssignmentId}/targets/catalog/apps/{appName}/{appId} | Assign an admin role app instance target |
| DELETE | /api/v1/users/{userId}/roles/{roleAssignmentId}/targets/catalog/apps/{appName}/{appId} | Unassign an admin role app instance target |
| GET | /api/v1/users/{userId}/roles/{roleAssignmentId}/targets/groups | List all admin role group targets |
| PUT | /api/v1/users/{userId}/roles/{roleAssignmentId}/targets/groups/{groupId} | Assign an admin role group target |
| DELETE | /api/v1/users/{userId}/roles/{roleAssignmentId}/targets/groups/{groupId} | Unassign an admin role group target |
| GET | /api/v1/users/{userId}/roles/{roleIdOrEncodedRoleId}/targets | Retrieve a role target by assignment type |
| DELETE | /api/v1/users/{userId}/sessions | Revoke all user sessions |
| GET | /api/v1/users/{userId}/subscriptions | List all subscriptions for a user |
| GET | /api/v1/users/{userId}/subscriptions/{notificationType} | Retrieve a subscription for a user |
| POST | /api/v1/users/{userId}/subscriptions/{notificationType}/subscribe | Subscribe a user to a specific notification type |
| POST | /api/v1/users/{userId}/subscriptions/{notificationType}/unsubscribe | Unsubscribe a user from a specific notification type |
| GET | /api/v1/zones | List all network zones |
| POST | /api/v1/zones | Create a network zone |
| GET | /api/v1/zones/{zoneId} | Retrieve a network zone |
| PUT | /api/v1/zones/{zoneId} | Replace a network zone |
| DELETE | /api/v1/zones/{zoneId} | Delete a network zone |
| POST | /api/v1/zones/{zoneId}/lifecycle/activate | Activate a network zone |
| POST | /api/v1/zones/{zoneId}/lifecycle/deactivate | Deactivate a network zone |

### attack-protection
| Method | Path | Description |
|--------|------|-------------|
| GET | /attack-protection/api/v1/authenticator-settings | Retrieve the authenticator settings |
| PUT | /attack-protection/api/v1/authenticator-settings | Replace the authenticator settings |
| GET | /attack-protection/api/v1/user-lockout-settings | Retrieve the user lockout settings |
| PUT | /attack-protection/api/v1/user-lockout-settings | Replace the user lockout settings |

### device-access
| Method | Path | Description |
|--------|------|-------------|
| GET | /device-access/api/v1/desktop-mfa/enforce-number-matching-challenge-settings | Retrieve the Desktop MFA Enforce Number Matching Challenge org setting |
| PUT | /device-access/api/v1/desktop-mfa/enforce-number-matching-challenge-settings | Replace the Desktop MFA Enforce Number Matching Challenge org setting |
| GET | /device-access/api/v1/desktop-mfa/recovery-pin-settings | Retrieve the Desktop MFA Recovery PIN org setting |
| PUT | /device-access/api/v1/desktop-mfa/recovery-pin-settings | Replace the Desktop MFA Recovery PIN org setting |

### integrations
| Method | Path | Description |
|--------|------|-------------|
| GET | /integrations/api/v1/api-services | List all API service integration instances |
| POST | /integrations/api/v1/api-services | Create an API service integration instance |
| GET | /integrations/api/v1/api-services/{apiServiceId} | Retrieve an API service integration instance |
| DELETE | /integrations/api/v1/api-services/{apiServiceId} | Delete an API service integration instance |
| GET | /integrations/api/v1/api-services/{apiServiceId}/credentials/secrets | List all API service integration instance secrets |
| POST | /integrations/api/v1/api-services/{apiServiceId}/credentials/secrets | Create an API service integration instance secret |
| DELETE | /integrations/api/v1/api-services/{apiServiceId}/credentials/secrets/{secretId} | Delete an API service integration instance secret |
| POST | /integrations/api/v1/api-services/{apiServiceId}/credentials/secrets/{secretId}/lifecycle/activate | Activate an API service integration instance secret |
| POST | /integrations/api/v1/api-services/{apiServiceId}/credentials/secrets/{secretId}/lifecycle/deactivate | Deactivate an API service integration instance secret |

### oauth2
| Method | Path | Description |
|--------|------|-------------|
| GET | /oauth2/v1/clients/{clientId}/roles | List all client role assignments |
| POST | /oauth2/v1/clients/{clientId}/roles | Assign a client role |
| GET | /oauth2/v1/clients/{clientId}/roles/{roleAssignmentId} | Retrieve a client role |
| DELETE | /oauth2/v1/clients/{clientId}/roles/{roleAssignmentId} | Unassign a client role |
| GET | /oauth2/v1/clients/{clientId}/roles/{roleAssignmentId}/targets/catalog/apps | List all client role app targets |
| PUT | /oauth2/v1/clients/{clientId}/roles/{roleAssignmentId}/targets/catalog/apps/{appName} | Assign a client role app target |
| DELETE | /oauth2/v1/clients/{clientId}/roles/{roleAssignmentId}/targets/catalog/apps/{appName} | Unassign a client role app target |
| PUT | /oauth2/v1/clients/{clientId}/roles/{roleAssignmentId}/targets/catalog/apps/{appName}/{appId} | Assign a client role app instance target |
| DELETE | /oauth2/v1/clients/{clientId}/roles/{roleAssignmentId}/targets/catalog/apps/{appName}/{appId} | Unassign a client role app instance target |
| GET | /oauth2/v1/clients/{clientId}/roles/{roleAssignmentId}/targets/groups | List all client role group targets |
| PUT | /oauth2/v1/clients/{clientId}/roles/{roleAssignmentId}/targets/groups/{groupId} | Assign a client role group target |
| DELETE | /oauth2/v1/clients/{clientId}/roles/{roleAssignmentId}/targets/groups/{groupId} | Unassign a client role group target |

### okta-personal-settings
| Method | Path | Description |
|--------|------|-------------|
| PUT | /okta-personal-settings/api/v1/edit-feature | Replace the Okta Personal admin settings |
| GET | /okta-personal-settings/api/v1/export-blocklists | List all blocked email domains |
| PUT | /okta-personal-settings/api/v1/export-blocklists | Replace the blocked email domains |

### privileged-access
| Method | Path | Description |
|--------|------|-------------|
| GET | /privileged-access/api/v1/service-accounts | List all app service accounts |
| POST | /privileged-access/api/v1/service-accounts | Create an app service account |
| GET | /privileged-access/api/v1/service-accounts/{id} | Retrieve an app service account |
| PATCH | /privileged-access/api/v1/service-accounts/{id} | Update an existing app service account |
| DELETE | /privileged-access/api/v1/service-accounts/{id} | Delete an app service account |

### security
| Method | Path | Description |
|--------|------|-------------|
| POST | /security/api/v1/security-events | Publish a security event token |

### webauthn-registration
| Method | Path | Description |
|--------|------|-------------|
| POST | /webauthn-registration/api/v1/activate | Activate a preregistered WebAuthn factor |
| POST | /webauthn-registration/api/v1/enroll | Enroll a preregistered WebAuthn factor |
| POST | /webauthn-registration/api/v1/initiate-fulfillment-request | Generate a fulfillment request |
| POST | /webauthn-registration/api/v1/send-pin | Send a PIN to user |
| GET | /webauthn-registration/api/v1/users/{userId}/enrollments | List all WebAuthn preregistration factors |
| DELETE | /webauthn-registration/api/v1/users/{userId}/enrollments/{authenticatorEnrollmentId} | Delete a WebAuthn preregistration factor |
| POST | /webauthn-registration/api/v1/users/{userId}/enrollments/{authenticatorEnrollmentId}/mark-error | Assign the fulfillment error status to a WebAuthn preregistration factor |

## Enhanced Skill Content
## Question Mapping

- "How do I list all users in my Okta org?" -> GET /api/v1/users
- "How do I create a new user with a password?" -> POST /api/v1/users
- "How do I deactivate a user account?" -> POST /api/v1/users/{id}/lifecycle/deactivate
- "How do I reset a user's password?" -> POST /api/v1/users/{id}/lifecycle/reset_password
- "What apps are assigned to a specific group?" -> GET /api/v1/groups/{groupId}/apps
- "How do I add a user to a group?" -> PUT /api/v1/groups/{groupId}/users/{userId}
- "How do I list all applications in my org?" -> GET /api/v1/apps
- "How do I check the system logs for a specific event?" -> GET /api/v1/logs
- "How do I create a custom authorization server?" -> POST /api/v1/authorizationServers
- "How do I add an OAuth scope to an authorization server?" -> POST /api/v1/authorizationServers/{authServerId}/scopes
- "How do I assign an admin role to a user?" -> POST /api/v1/users/{userId}/roles
- "How do I suspend a user without deleting them?" -> POST /api/v1/users/{id}/lifecycle/suspend
- "How do I configure a network zone for IP blocking?" -> POST /api/v1/zones
- "How do I set up an event hook for user creation?" -> POST /api/v1/eventHooks
- "How do I rotate signing keys on an authorization server?" -> POST /api/v1/authorizationServers/{authServerId}/credentials/lifecycle/keyRotate

## Response Tips

- **Users/Groups/Apps (list endpoints):** Results are arrays with cursor-based pagination via `after` param; follow `_links.next.href` to get subsequent pages. Default limits vary (users: 200, groups: 200, apps: unlimited). Always check for a `next` link rather than assuming all results arrived.
- **Lifecycle actions (activate/deactivate/suspend):** Return 200 with the updated object or 204 with no body. A 404 means the resource does not exist or is already in the target state. Check the `status` and `transitioningToStatus` fields to confirm state changes took effect.
- **System logs:** Returns time-ordered entries. Use `since`/`until` (ISO 8601) for time windows and `filter` (SCIM syntax) for event types. Pagination uses opaque `after` tokens, not numeric offsets. The `sortOrder` default is ASCENDING.
- **Authorization server resources (claims/scopes/policies/rules):** Nested under `authServerId`. Responses include `_links` for navigating between parent and child resources. Rules have `priority` fields -- lower numbers evaluate first.
- **Credentials/keys endpoints:** Key responses include `expiresAt`, `kid`, and `x5c` (certificate chain). Always check `status` field (ACTIVE/INACTIVE) -- inactive keys do not participate in signing.
- **Delete operations:** Consistently return 204 with no body on success. A subsequent GET returning 404 confirms deletion. User deletion requires deactivation first or you get a 400.

## Anomaly Flags

- **429 Too Many Requests on every endpoint:** Surface rate limit headers (`X-Rate-Limit-Limit`, `X-Rate-Limit-Remaining`, `X-Rate-Limit-Reset`) proactively when remaining count drops below 20% of limit. All 705 endpoints can return 429.
- **User status transitions:** Flag when `transitioningToStatus` is non-null, as the user is mid-lifecycle change. Also flag if `status` is `LOCKED_OUT` or `PASSWORD_EXPIRED` unexpectedly.
- **Key/certificate expiration:** When `expiresAt` on signing keys or credentials is within 30 days, surface a rotation warning. Check credentials on apps, IdPs, and authorization servers.
- **Deactivated resources still referenced:** Flag when policies, authenticators, or IdPs have `status: INACTIVE` but are still bound to active apps or auth server policies.
- **Event hook verification status:** Surface `verificationStatus: UNVERIFIED` on event hooks -- these will not receive events until verified.
- **Principal rate limit overrides:** When `defaultPercentage` or `defaultConcurrencyPercentage` on principal rate limits are set unusually high (>80%), warn about potential org-wide rate limit starvation.
- **Agent pool update failures:** Flag `status: Failed` on agent pool updates, as these indicate agents that did not successfully upgrade and may be running outdated versions.
- **Log stream status:** Alert when log streams are `INACTIVE`, as security events may not be forwarding to SIEM.

## Playbook

### 1. Onboard a New User with App and Group Assignment

1. Create the user: POST /api/v1/users with `profile` (login, email, firstName, lastName) and `credentials.password`. Set `activate=true`.
2. Assign the user to a group: PUT /api/v1/groups/{groupId}/users/{userId} (returns 204).
3. Verify group membership: GET /api/v1/users/{id}/groups to confirm the group appears.
4. Check app access: GET /api/v1/users/{id}/appLinks to confirm apps inherited from the group are visible.
5. If MFA is required, enroll a factor: POST /api/v1/users/{userId}/factors with the desired `factorType` and `provider`.

### 2. Set Up a Custom Authorization Server with Scopes and Policies

1. Create the authorization server: POST /api/v1/authorizationServers with `name`, `audiences`, and `description`.
2. Add custom scopes: POST /api/v1/authorizationServers/{authServerId}/scopes with `name` for each scope (e.g., `read:data`, `write:data`).
3. Add custom claims: POST /api/v1/authorizationServers/{authServerId}/claims with `name`, `value` (Okta Expression Language), and `claimType` (RESOURCE or IDENTITY).
4. Create an access policy: POST /api/v1/authorizationServers/{authServerId}/policies targeting specific client apps.
5. Add a policy rule: POST /api/v1/authorizationServers/{authServerId}/policies/{policyId}/rules specifying grant types, scopes, and user/group conditions.
6. Activate the server: POST /api/v1/authorizationServers/{authServerId}/lifecycle/activate (returns 204).

### 3. Investigate a Security Incident via System Logs

1. Query recent logs: GET /api/v1/logs with `filter=eventType eq "user.session.start"` and `since` set to the incident window.
2. Narrow by suspect user: Add `&filter=actor.id eq "{userId}"` or `&q=suspect@example.com`.
3. Check for suspicious IPs: Look for `client.ipAddress` in results and cross-reference with network zones: GET /api/v1/zones.
4. Review user sessions: GET /api/v1/users/{userId}/sessions -- revoke if compromised: DELETE /api/v1/users/{userId}/sessions with `oauthTokens=true`.
5. If needed, suspend the user: POST /api/v1/users/{id}/lifecycle/suspend. This preserves the account but blocks access.
6. Revoke all grants: DELETE /api/v1/users/{userId}/grants to invalidate outstanding OAuth tokens.

### 4. Offboard a Departing Employee

1. Deactivate the user: POST /api/v1/users/{id}/lifecycle/deactivate (must happen before deletion).
2. Revoke all active sessions: DELETE /api/v1/users/{userId}/sessions with `oauthTokens=true` and `forgetDevices=true`.
3. Remove app-specific assignments: For each app, DELETE /api/v1/apps/{appId}/users/{userId} with `sendEmail=false`.
4. Remove from groups: For each group, DELETE /api/v1/groups/{groupId}/users/{userId}.
5. Optionally delete the user permanently: DELETE /api/v1/users/{id} with `sendEmail=false`. This is irreversible.

### 5. Rotate Application Credentials

1. List current keys: GET /api/v1/apps/{appId}/credentials/keys to see active signing keys and their `expiresAt` dates.
2. Generate a new key: POST /api/v1/apps/{appId}/credentials/keys/generate with `validityYears` (e.g., 2).
3. Update the app to use the new key: PUT /api/v1/apps/{appId} referencing the new `kid` in the credentials section.
4. For client secrets (OIDC apps): POST /api/v1/apps/{appId}/credentials/secrets to create a new secret, then distribute to the app.
5. Deactivate the old secret: POST /api/v1/apps/{appId}/credentials/secrets/{secretId}/lifecycle/deactivate.
6. After confirming no traffic on the old secret, delete it: DELETE /api/v1/apps/{appId}/credentials/secrets/{secretId}.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
