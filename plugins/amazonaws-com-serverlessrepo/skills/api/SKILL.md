---
name: awsserverlessapplicationrepository
description: "AWSServerlessApplicationRepository API skill. Use when working with AWSServerlessApplicationRepository for applications. Covers 14 endpoints."
version: 1.0.0
generator: lapsh
---

# AWSServerlessApplicationRepository
API version: 2017-09-08

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
2. GET /applications -- verify access
3. POST /applications -- create first applications

## Endpoints

14 endpoints across 1 groups. See references/api-spec.lap for full details.

### applications
| Method | Path | Description |
|--------|------|-------------|
| POST | /applications | Creates an application, optionally including an AWS SAM file to create the first application version in the same call. |
| PUT | /applications/{applicationId}/versions/{semanticVersion} | Creates an application version. |
| POST | /applications/{applicationId}/changesets | Creates an AWS CloudFormation change set for the given application. |
| POST | /applications/{applicationId}/templates | Creates an AWS CloudFormation template. |
| DELETE | /applications/{applicationId} | Deletes the specified application. |
| GET | /applications/{applicationId} | Gets the specified application. |
| GET | /applications/{applicationId}/policy | Retrieves the policy for the application. |
| GET | /applications/{applicationId}/templates/{templateId} | Gets the specified AWS CloudFormation template. |
| GET | /applications/{applicationId}/dependencies | Retrieves the list of applications nested in the containing application. |
| GET | /applications/{applicationId}/versions | Lists versions for the specified application. |
| GET | /applications | Lists applications owned by the requester. |
| PUT | /applications/{applicationId}/policy | Sets the permission policy for an application. For the list of actions supported for this operation, see |
| POST | /applications/{applicationId}/unshare | Unshares an application from an AWS Organization.This operation can be called only from the organization's master account. |
| PATCH | /applications/{applicationId} | Updates the specified application. |

## Enhanced Skill Content
## Question Mapping

- "How do I publish a new serverless application?" -> POST /applications
- "How do I deploy an application to my AWS account?" -> POST /applications/{applicationId}/changesets
- "What applications are available in the repository?" -> GET /applications
- "How do I get details about a specific application?" -> GET /applications/{applicationId}
- "How do I update my application's description or labels?" -> PATCH /applications/{applicationId}
- "How do I delete an application I no longer need?" -> DELETE /applications/{applicationId}
- "How do I create a new version of my application?" -> PUT /applications/{applicationId}/versions/{semanticVersion}
- "What versions exist for this application?" -> GET /applications/{applicationId}/versions
- "Who can access my application and what are the sharing policies?" -> GET /applications/{applicationId}/policy
- "How do I share or restrict access to my application?" -> PUT /applications/{applicationId}/policy
- "How do I stop sharing an application with an organization?" -> POST /applications/{applicationId}/unshare
- "What nested applications does this app depend on?" -> GET /applications/{applicationId}/dependencies
- "How do I get a CloudFormation template for an application?" -> POST /applications/{applicationId}/templates
- "What is the status of my template creation request?" -> GET /applications/{applicationId}/templates/{templateId}
- "How do I deploy a specific older version of an application?" -> POST /applications/{applicationId}/changesets (with SemanticVersion parameter)

## Response Tips

- **Application listings** (GET /applications, GET .../versions, GET .../dependencies): Paginated via `NextToken` -- keep calling with the returned `NextToken` until it is absent or empty. Use `maxItems` to control page size.
- **Application detail** (GET/POST/PATCH .../applications): The nested `Version` object contains `ParameterDefinitions` and `RequiredCapabilities` -- inspect these before deploying to understand what inputs and IAM capabilities are needed.
- **Changeset creation** (POST .../changesets): Returns IDs only (`ChangeSetId`, `StackId`) -- use AWS CloudFormation APIs to monitor the actual deployment progress.
- **Template creation** (POST/GET .../templates): The `Status` field progresses through states (PREPARING, ACTIVE, EXPIRED) -- poll GET .../templates/{templateId} until `Status` is ACTIVE, then use the `TemplateUrl`.
- **Policy endpoints** (GET/PUT .../policy): `Statements` is an array of policy statements -- an empty array means the application is private.
- **Delete and unshare** (DELETE, POST .../unshare): Return no body on success -- a 204 or empty 200 indicates the operation succeeded.

## Anomaly Flags

- **Template stuck in PREPARING**: If GET .../templates/{templateId} returns `Status: PREPARING` for more than 60 seconds, surface a warning -- template generation may have failed silently.
- **ExpirationTime approaching**: Template URLs expire. If `ExpirationTime` is within 15 minutes of the current time, warn the user to download or use the template immediately.
- **RequiredCapabilities non-empty**: When deploying via changesets, if the application version lists `RequiredCapabilities` (e.g., CAPABILITY_IAM, CAPABILITY_RESOURCE_POLICY), the user must explicitly acknowledge these -- flag them before creating the changeset.
- **IsVerifiedAuthor is false**: When retrieving third-party applications, surface that the author is unverified so the user can assess trustworthiness.
- **Empty Statements in policy**: If GET .../policy returns an empty `Statements` array, note that the application is currently private and not shared with anyone.
- **Pagination truncation**: If a list response includes `NextToken` but the user did not request all pages, flag that results are incomplete.
- **ResourcesSupported is false**: If a version reports `ResourcesSupported: false`, warn that the template contains resources not yet supported by the service and deployment may fail.

## Playbook

### 1. Publish and share a new serverless application

1. POST /applications with `Name`, `Author`, `Description`, and either `TemplateBody`/`TemplateUrl` plus `ReadmeBody`/`ReadmeUrl`.
2. Note the returned `ApplicationId`.
3. PUT /applications/{applicationId}/policy with `Statements` granting access (use principal `*` for public, or specific account IDs for private sharing).
4. Verify with GET /applications/{applicationId}/policy to confirm the policy is set correctly.

### 2. Deploy an application from the repository

1. GET /applications to browse available applications (paginate with `nextToken` if needed).
2. GET /applications/{applicationId} to review details, checking `Version.ParameterDefinitions` for required inputs and `Version.RequiredCapabilities` for IAM acknowledgments.
3. POST /applications/{applicationId}/changesets with `StackName`, any `ParameterOverrides`, and the required `Capabilities`.
4. Use the returned `ChangeSetId` and `StackId` with AWS CloudFormation APIs to monitor and execute the deployment.

### 3. Release a new version of an existing application

1. GET /applications/{applicationId} to confirm the current version and application state.
2. PUT /applications/{applicationId}/versions/{semanticVersion} with the new `SemanticVersion` and either `TemplateBody`/`TemplateUrl`.
3. Verify the new version appears with GET /applications/{applicationId}/versions.
4. Optionally PATCH /applications/{applicationId} to update the description or labels to reflect the new release.

### 4. Audit dependencies before deploying a nested application

1. GET /applications/{applicationId}/dependencies (paginate with `nextToken` until all dependencies are retrieved).
2. For each dependency, GET /applications/{dependencyApplicationId} to review its author, verification status, and required capabilities.
3. Check `IsVerifiedAuthor` and `RequiredCapabilities` for each dependency to assess risk.
4. Once satisfied, proceed with POST /applications/{applicationId}/changesets, ensuring all nested capabilities are included in `Capabilities`.

### 5. Generate and retrieve a CloudFormation template

1. POST /applications/{applicationId}/templates, optionally specifying `SemanticVersion` to target a specific version.
2. Note the returned `TemplateId` and `Status`.
3. Poll GET /applications/{applicationId}/templates/{templateId} until `Status` is `ACTIVE`.
4. Use the `TemplateUrl` from the response to download or reference the template -- act before `ExpirationTime` passes.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
