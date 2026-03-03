---
name: adobe-experience-manager-aem-api
description: "Adobe Experience Manager (AEM) API skill. Use when working with Adobe Experience Manager (AEM) for system, libs, .cqactions.html. Covers 48 endpoints."
version: 1.0.0
generator: lapsh
---

# Adobe Experience Manager (AEM) API
API version: 3.7.1-pre.0

## Auth
Bearer basic

## Base URL
/

## Setup
1. Set Authorization header with your Bearer token
2. GET /system/console/configMgr -- verify access
3. POST /.cqactions.html -- create first .cqactions.html

## Endpoints

48 endpoints across 9 groups. See references/api-spec.lap for full details.

### system
| Method | Path | Description |
|--------|------|-------------|
| GET | /system/console/configMgr |  |
| GET | /system/console/bundles/{name}.json |  |
| POST | /system/console/bundles/{name} |  |
| POST | /system/console/jmx/com.adobe.granite:type=Repository/op/{action} |  |
| GET | /system/health |  |
| POST | /system/console/configMgr/com.adobe.granite.auth.saml.SamlAuthenticationHandler |  |
| GET | /system/console/status-productinfo.json |  |

### libs
| Method | Path | Description |
|--------|------|-------------|
| GET | /libs/granite/core/content/login.html |  |
| POST | /libs/replication/treeactivation.html |  |
| POST | /libs/granite/security/post/authorizables |  |
| POST | /libs/granite/security/post/truststore |  |
| GET | /libs/granite/security/truststore.json |  |
| POST | /libs/granite/security/post/sslSetup.html |  |

### .cqactions.html
| Method | Path | Description |
|--------|------|-------------|
| POST | /.cqactions.html |  |

### {path}
| Method | Path | Description |
|--------|------|-------------|
| POST | /{path}/ |  |
| GET | /{path}/{name} |  |
| POST | /{path}/{name} |  |
| DELETE | /{path}/{name} |  |
| POST | /{path}/{name}.rw.html |  |

### apps
| Method | Path | Description |
|--------|------|-------------|
| POST | /apps/system/config/{configNodeName} |  |
| POST | /apps/system/config/org.apache.felix.http |  |
| POST | /apps/system/config/org.apache.sling.servlets.get.DefaultGetServlet |  |
| POST | /apps/system/config/org.apache.sling.security.impl.ReferrerFilter |  |
| POST | /apps/system/config/org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet |  |
| POST | /apps/system/config/com.shinesolutions.aem.passwordreset.Activator |  |
| POST | /apps/system/config/com.shinesolutions.healthcheck.hc.impl.ActiveBundleHealthCheck |  |
| POST | /apps/system/config/com.adobe.granite.auth.saml.SamlAuthenticationHandler.config |  |
| POST | /apps/system/config/org.apache.http.proxyconfigurator.config |  |

### bin
| Method | Path | Description |
|--------|------|-------------|
| GET | /bin/querybuilder.json |  |
| POST | /bin/querybuilder.json |  |

### etc
| Method | Path | Description |
|--------|------|-------------|
| GET | /etc/packages/{group}/{name}-{version}.zip |  |
| GET | /etc/packages/{group}/{name}-{version}.zip/jcr:content/vlt:definition/filter.tidy.2.json |  |
| GET | /etc/replication/agents.{runmode}.-1.json |  |
| GET | /etc/replication/agents.{runmode}/{name} |  |
| DELETE | /etc/replication/agents.{runmode}/{name} |  |
| POST | /etc/replication/agents.{runmode}/{name} |  |
| GET | /etc/truststore/truststore.p12 |  |
| POST | /etc/truststore |  |

### crx
| Method | Path | Description |
|--------|------|-------------|
| POST | /crx/explorer/ui/setpassword.jsp |  |
| GET | /crx/packmgr/installstatus.jsp |  |
| POST | /crx/packmgr/service.jsp |  |
| POST | /crx/packmgr/update.jsp |  |
| POST | /crx/packmgr/service/.json/{path} |  |
| GET | /crx/packmgr/service/script.html |  |
| GET | /crx/server/crx.default/jcr:root/.1.json |  |

### {intermediatePath}
| Method | Path | Description |
|--------|------|-------------|
| POST | /{intermediatePath}/{authorizableId}.ks.html |  |
| GET | /{intermediatePath}/{authorizableId}.ks.json |  |
| GET | /{intermediatePath}/{authorizableId}/keystore/store.p12 |  |

## Enhanced Skill Content
## Question Mapping

- "How do I check if AEM is running and healthy?" -> GET /system/health
- "How do I query content nodes by property value?" -> GET /bin/querybuilder.json
- "How do I create a new user or group?" -> POST /libs/granite/security/post/authorizables
- "How do I change a user's password?" -> POST /crx/explorer/ui/setpassword.jsp
- "How do I download a content package?" -> GET /etc/packages/{group}/{name}-{version}.zip
- "How do I install or build a package?" -> POST /crx/packmgr/service/.json/{path}
- "How do I check package installation progress?" -> GET /crx/packmgr/installstatus.jsp
- "How do I list replication agents for author or publish?" -> GET /etc/replication/agents.{runmode}.-1.json
- "How do I create or update a replication agent?" -> POST /etc/replication/agents.{runmode}/{name}
- "How do I configure SAML SSO authentication?" -> POST /apps/system/config/com.adobe.granite.auth.saml.SamlAuthenticationHandler.config
- "How do I enable HTTPS/SSL on AEM?" -> POST /libs/granite/security/post/sslSetup.html
- "How do I activate a content tree for replication?" -> POST /libs/replication/treeactivation.html
- "How do I manage a user's keystore?" -> POST /{intermediatePath}/{authorizableId}.ks.html
- "How do I get the current OSGi configuration?" -> GET /system/console/configMgr
- "How do I delete a node or authorizable?" -> DELETE /{path}/{name}

## Response Tips

- **System/health endpoints**: `GET /system/health` returns health check results; use `tags` to filter checks and `combineTagsOr` to broaden matching. Product info returns a JSON array.
- **Package manager**: `GET /crx/packmgr/installstatus.jsp` returns `{status: {finished, itemCount}}`; poll until `finished` is true. Service endpoints return command output as HTML or JSON depending on path.
- **Query builder**: Results are JSON with `hits` array; `p.limit` controls page size (-1 for unlimited). Property predicates use numbered prefixes (`1_property`, `2_property`).
- **Bundles**: `GET /system/console/bundles/{name}.json` returns `{s: [int]}` summary array (total, active, fragment, resolved, installed) and `data` array with bundle details.
- **Replication agents**: List endpoint returns all agents as a JSON object keyed by agent name; individual agent GET returns full JCR properties.
- **Security/truststore**: `GET /libs/granite/security/truststore.json` returns `{aliases, exists}`; check `exists` before operations. Binary endpoints (`.p12`) return raw PKCS12 downloads.
- **Node operations**: POST to `/{path}/` creates nodes; POST to `/{path}/{name}` updates. DELETE returns 204 on success. All require valid JCR paths.
- **Error patterns**: 5XX on system endpoints indicates server issues. 302 on SAML config means redirect (not failure). 404/405 on CRX script endpoint is expected when unavailable.

## Anomaly Flags

- **Package install stuck**: If `GET /crx/packmgr/installstatus.jsp` shows `finished: false` for an extended period, flag that installation may be hanging and suggest checking error logs.
- **Bundle not active**: When `GET /system/console/bundles/{name}.json` returns a bundle in resolved or installed state instead of active, proactively warn that the bundle may have unresolved dependencies.
- **Health check failures**: Any non-200 or negative health result from `GET /system/health` should be surfaced immediately with the failing tag names.
- **Replication agent disabled**: When creating or updating an agent via POST, flag if `jcr:content/enabled` is set to false, as the agent will not process the replication queue.
- **SAML misconfiguration risk**: When configuring SAML, flag if `assertionConsumerServiceURL` or `idpUrl` is missing, or if `useEncryption` is true but `spPrivateKeyAlias` is empty.
- **SSL setup with mismatched passwords**: If `keystorePassword` and `keystorePasswordConfirm` differ in the SSL setup call, surface before sending.
- **Deprecated CRX endpoints**: `GET /crx/packmgr/service/script.html` returns 404/405; flag that this endpoint is unavailable and suggest using `/crx/packmgr/service.jsp` instead.
- **5XX responses on any system console endpoint**: Surface immediately as this likely indicates the OSGi container is unhealthy.

## Playbook

### 1. Install a Content Package End-to-End

1. Upload the package: `POST /crx/packmgr/service.jsp` with `cmd=upload` and the package file.
2. Build the package if needed: `POST /crx/packmgr/service/.json/{path}` with `cmd=build`.
3. Install the package: `POST /crx/packmgr/service/.json/{path}` with `cmd=install`. Set `recursive=true` if the package contains sub-packages.
4. Poll installation status: `GET /crx/packmgr/installstatus.jsp` until `status.finished` is `true`.
5. Verify the package filter: `GET /etc/packages/{group}/{name}-{version}.zip/jcr:content/vlt:definition/filter.tidy.2.json` to confirm correct content paths.

### 2. Set Up a New Replication Agent

1. List existing agents to avoid conflicts: `GET /etc/replication/agents.{runmode}.-1.json` (use `author` or `publish` as runmode).
2. Create the agent: `POST /etc/replication/agents.{runmode}/{name}` with required properties including `jcr:content/transportUri`, `jcr:content/transportUser`, `jcr:content/transportPassword`, and `jcr:content/serializationType`.
3. Enable the agent: set `jcr:content/enabled=true` in the same or a follow-up POST.
4. Verify: `GET /etc/replication/agents.{runmode}/{name}` to confirm all properties were saved correctly.
5. Test by triggering tree activation: `POST /libs/replication/treeactivation.html` with a target `path` and `cmd=activate`.

### 3. Create a User and Configure Their Keystore

1. Create the user: `POST /libs/granite/security/post/authorizables` with `authorizableId`, `intermediatePath`, `createUser=true`, and `rep:password`.
2. Set group memberships if needed: `POST /{path}/{name}.rw.html` with `addMembers` pointing to the new user.
3. Create/initialize the keystore: `POST /{intermediatePath}/{authorizableId}.ks.html` with `newPassword` and `rePassword`.
4. Verify keystore: `GET /{intermediatePath}/{authorizableId}.ks.json` to confirm it exists and check aliases.
5. Download the keystore backup: `GET /{intermediatePath}/{authorizableId}/keystore/store.p12`.

### 4. Configure SAML Authentication

1. Set up the truststore first: `POST /libs/granite/security/post/truststore` with a new password and the IDP certificate.
2. Verify truststore: `GET /libs/granite/security/truststore.json` and confirm `exists: true` with the IDP cert alias in `aliases`.
3. Configure the SAML handler: `POST /apps/system/config/com.adobe.granite.auth.saml.SamlAuthenticationHandler.config` with `idpUrl`, `idpCertAlias`, `serviceProviderEntityId`, `assertionConsumerServiceURL`, `path`, and `defaultRedirectUrl`.
4. Enable user auto-creation if desired: set `createUser=true` and `userIntermediatePath` in the same config call.
5. Verify via OSGi console: `POST /system/console/configMgr/com.adobe.granite.auth.saml.SamlAuthenticationHandler` with `apply=true` to confirm the configuration is active.

### 5. Enable SSL/HTTPS on AEM

1. Configure the Felix HTTPS settings: `POST /apps/system/config/org.apache.felix.http` with `org.apache.felix.https.enable=true`, keystore paths, passwords, and the secure port (`org.osgi.service.http.port.secure`).
2. Set up SSL certificates: `POST /libs/granite/security/post/sslSetup.html` with `keystorePassword`, `truststorePassword`, `httpsHostname`, and `httpsPort`.
3. Upload the truststore if not already done: `POST /etc/truststore` with the certificate file.
4. Verify truststore contents: `GET /libs/granite/security/truststore.json`.
5. Confirm AEM is responding on HTTPS: `GET /system/health` over the new HTTPS port.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
