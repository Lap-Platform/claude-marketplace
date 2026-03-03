---
name: aws-signer
description: "AWS Signer API skill. Use when working with AWS Signer for signing-profiles, signing-jobs, revocations. Covers 19 endpoints."
version: 1.0.0
generator: lapsh
---

# AWS Signer
API version: 2017-08-25

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
2. GET /revocations -- verify access
3. POST /signing-profiles/{profileName}/permissions -- create first permissions

## Endpoints

19 endpoints across 5 groups. See references/api-spec.lap for full details.

### signing-profiles
| Method | Path | Description |
|--------|------|-------------|
| POST | /signing-profiles/{profileName}/permissions | Adds cross-account permissions to a signing profile. |
| DELETE | /signing-profiles/{profileName} | Changes the state of an ACTIVE signing profile to CANCELED. A canceled profile is still viewable with the ListSigningProfiles operation, but it cannot perform new signing jobs, and is deleted two years after cancelation. |
| GET | /signing-profiles/{profileName} | Returns information on a specific signing profile. |
| GET | /signing-profiles/{profileName}/permissions | Lists the cross-account permissions associated with a signing profile. |
| GET | /signing-profiles | Lists all available signing profiles in your AWS account. Returns only profiles with an ACTIVE status unless the includeCanceled request field is set to true. If additional jobs remain to be listed, AWS Signer returns a nextToken value. Use this value in subsequent calls to ListSigningJobs to fetch the remaining values. You can continue calling ListSigningJobs with your maxResults parameter and with new values that Signer returns in the nextToken parameter until all of your signing jobs have been returned. |
| PUT | /signing-profiles/{profileName} | Creates a signing profile. A signing profile is a code-signing template that can be used to carry out a pre-defined signing job. |
| DELETE | /signing-profiles/{profileName}/permissions/{statementId} | Removes cross-account permissions from a signing profile. |
| PUT | /signing-profiles/{profileName}/revoke | Changes the state of a signing profile to REVOKED. This indicates that signatures generated using the signing profile after an effective start date are no longer valid. |

### signing-jobs
| Method | Path | Description |
|--------|------|-------------|
| GET | /signing-jobs/{jobId} | Returns information about a specific code signing job. You specify the job by using the jobId value that is returned by the StartSigningJob operation. |
| GET | /signing-jobs | Lists all your signing jobs. You can use the maxResults parameter to limit the number of signing jobs that are returned in the response. If additional jobs remain to be listed, AWS Signer returns a nextToken value. Use this value in subsequent calls to ListSigningJobs to fetch the remaining values. You can continue calling ListSigningJobs with your maxResults parameter and with new values that Signer returns in the nextToken parameter until all of your signing jobs have been returned. |
| PUT | /signing-jobs/{jobId}/revoke | Changes the state of a signing job to REVOKED. This indicates that the signature is no longer valid. |
| POST | /signing-jobs/with-payload | Signs a binary payload and returns a signature envelope. |
| POST | /signing-jobs | Initiates a signing job to be performed on the code provided. Signing jobs are viewable by the ListSigningJobs operation for two years after they are performed. Note the following requirements:     You must create an Amazon S3 source bucket. For more information, see Creating a Bucket in the Amazon S3 Getting Started Guide.    Your S3 source bucket must be version enabled.   You must create an S3 destination bucket. AWS Signer uses your S3 destination bucket to write your signed code.   You specify the name of the source and destination buckets when calling the StartSigningJob operation.   You must ensure the S3 buckets are from the same Region as the signing profile. Cross-Region signing isn't supported.   You must also specify a request token that identifies your request to Signer.   You can call the DescribeSigningJob and the ListSigningJobs actions after you call StartSigningJob. For a Java example that shows how to use this action, see StartSigningJob. |

### revocations
| Method | Path | Description |
|--------|------|-------------|
| GET | /revocations | Retrieves the revocation status of one or more of the signing profile, signing job, and signing certificate. |

### signing-platforms
| Method | Path | Description |
|--------|------|-------------|
| GET | /signing-platforms/{platformId} | Returns information on a specific signing platform. |
| GET | /signing-platforms | Lists all signing platforms available in AWS Signer that match the request parameters. If additional jobs remain to be listed, Signer returns a nextToken value. Use this value in subsequent calls to ListSigningJobs to fetch the remaining values. You can continue calling ListSigningJobs with your maxResults parameter and with new values that Signer returns in the nextToken parameter until all of your signing jobs have been returned. |

### tags
| Method | Path | Description |
|--------|------|-------------|
| GET | /tags/{resourceArn} | Returns a list of the tags associated with a signing profile resource. |
| POST | /tags/{resourceArn} | Adds one or more tags to a signing profile. Tags are labels that you can use to identify and organize your AWS resources. Each tag consists of a key and an optional value. To specify the signing profile, use its Amazon Resource Name (ARN). To specify the tag, use a key-value pair. |
| DELETE | /tags/{resourceArn} | Removes one or more tags from a signing profile. To remove the tags, specify a list of tag keys. |

## Enhanced Skill Content
## Question Mapping

- "How do I sign an S3 object?" -> POST /signing-jobs
- "Can I sign a payload directly without uploading to S3?" -> POST /signing-jobs/with-payload
- "What signing jobs have I run?" -> GET /signing-jobs
- "What is the status of my signing job?" -> GET /signing-jobs/{jobId}
- "Which signing profiles exist in my account?" -> GET /signing-profiles
- "What configuration does a specific signing profile use?" -> GET /signing-profiles/{profileName}
- "How do I create a new signing profile?" -> PUT /signing-profiles/{profileName}
- "How do I revoke a signing job?" -> PUT /signing-jobs/{jobId}/revoke
- "How do I revoke a signing profile version?" -> PUT /signing-profiles/{profileName}/revoke
- "What signing platforms are available for my use case?" -> GET /signing-platforms
- "What encryption and hash algorithms does a platform support?" -> GET /signing-platforms/{platformId}
- "How do I grant cross-account access to a signing profile?" -> POST /signing-profiles/{profileName}/permissions
- "Who has permissions on my signing profile?" -> GET /signing-profiles/{profileName}/permissions
- "How do I remove a permission from a signing profile?" -> DELETE /signing-profiles/{profileName}/permissions/{statementId}
- "Has a specific certificate or profile version been revoked?" -> GET /revocations

## Response Tips

- **Signing jobs**: List responses use `jobs` array with `nextToken` for pagination; pass `maxResults` (default varies) and loop on `nextToken`. Individual job responses nest `source.s3`, `signedObject.s3`, and `revocationRecord` -- always check `status` before reading `signedObject`.
- **Signing profiles**: List responses use `profiles` array with `nextToken`; detail responses nest `revocationRecord`, `signingMaterial`, `overrides.signingConfiguration`, and `signatureValidityPeriod`. A `status` of `Canceled` means the profile was deleted.
- **Signing platforms**: List responses use `platforms` array with `nextToken`; detail responses nest `signingConfiguration.encryptionAlgorithmOptions` and `hashAlgorithmOptions` with `allowedValues`/`defaultValue` pairs.
- **Permissions**: Returns a `permissions` array with `nextToken`; track `revisionId` -- it changes on every mutation and must be passed to delete calls.
- **Tags**: Returned as flat `map<str,str>` -- no pagination needed.
- **Revocations**: Returns `revokedEntities` as a flat string array; an empty array means nothing is revoked.

## Anomaly Flags

- **Job stuck in `InProgress`**: Surface if a signing job has been in `InProgress` status for more than a few minutes -- may indicate a source object access issue.
- **Profile status `Canceled`**: Warn if a profile referenced in a workflow has `status: Canceled` -- it cannot be used for new signing jobs.
- **Revoked profile or job**: Proactively flag when `revocationRecord` is present on a profile or job being inspected.
- **Signature expiration approaching**: When `signatureExpiresAt` is within 30 days, alert the user to re-sign affected artifacts.
- **Permission revision mismatch**: If a `DELETE /permissions` call fails, the `revisionId` is likely stale -- re-fetch permissions and retry.
- **Max size exceeded**: When preparing a signing job, check `maxSizeInMB` from the platform details against the source object size before submitting.
- **Pagination truncation**: If a list response includes `nextToken` but the caller did not paginate, warn that results are incomplete.

## Playbook

### 1. Sign an S3 Object End-to-End

1. List available platforms with `GET /signing-platforms` filtered by `target` and `category` to find the right `platformId`.
2. Create a signing profile with `PUT /signing-profiles/{profileName}` specifying the chosen `platformId` and `signingMaterial.certificateArn`.
3. Start the signing job with `POST /signing-jobs` providing `source.s3` (bucket, key, version), `destination.s3` (output bucket/prefix), `profileName`, and a unique `clientRequestToken`.
4. Poll `GET /signing-jobs/{jobId}` until `status` is `Succeeded` or `Failed`.
5. Retrieve the signed artifact from the `signedObject.s3.bucketName` and `key` in the response.

### 2. Grant Cross-Account Signing Access

1. Get the current profile details with `GET /signing-profiles/{profileName}` and note the `profileVersion`.
2. Add a permission with `POST /signing-profiles/{profileName}/permissions` specifying `action` (e.g., `signer:StartSigningJob`), `principal` (the target account ARN), `statementId` (a unique label), and optionally `profileVersion`.
3. Verify the permission was applied with `GET /signing-profiles/{profileName}/permissions`.
4. Share the `profileName` and `profileVersion` with the target account.

### 3. Revoke a Compromised Signing Profile

1. Identify the profile version to revoke via `GET /signing-profiles/{profileName}` -- note the `profileVersion`.
2. Revoke the profile version with `PUT /signing-profiles/{profileName}/revoke` specifying `profileVersion`, `reason`, and `effectiveTime` (the timestamp from which signatures should be considered invalid).
3. Confirm revocation by re-fetching the profile with `GET /signing-profiles/{profileName}` and checking that `revocationRecord` is populated.
4. Optionally, list affected signing jobs with `GET /signing-jobs?isRevoked=true&platformId=...` to assess blast radius.

### 4. Audit Signing Activity

1. List all signing jobs with `GET /signing-jobs`, paginating with `nextToken` and filtering by `status`, `requestedBy`, or time window (`signatureExpiresBefore`/`signatureExpiresAfter`).
2. For each job of interest, fetch full details with `GET /signing-jobs/{jobId}` to inspect `source`, `signingParameters`, `requestedBy`, and `jobInvoker`.
3. Check revocation status of specific artifacts by calling `GET /revocations` with the job's `signatureTimestamp`, `platformId`, `profileVersionArn`, `jobArn`, and `certificateHashes`.
4. Review tags on profiles or jobs with `GET /tags/{resourceArn}` for organizational metadata.

### 5. Clean Up Unused Signing Profiles

1. List all profiles with `GET /signing-profiles?includeCanceled=false` to find active profiles.
2. For each candidate profile, list recent signing jobs with `GET /signing-jobs?profileName=...` (filter by `requestedBy` or date range) to confirm the profile is unused.
3. Review and remove any cross-account permissions with `GET /signing-profiles/{profileName}/permissions`, then `DELETE /signing-profiles/{profileName}/permissions/{statementId}` for each, passing the current `revisionId`.
4. Delete the profile with `DELETE /signing-profiles/{profileName}`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
