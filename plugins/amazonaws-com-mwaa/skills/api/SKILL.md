---
name: amazonmwaa
description: "AmazonMWAA API skill. Use when working with AmazonMWAA for clitoken, environments, webtoken. Covers 11 endpoints."
version: 1.0.0
generator: lapsh
---

# AmazonMWAA
API version: 2020-07-01

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
2. GET /environments -- verify access
3. POST /clitoken/{Name} -- create first clitoken

## Endpoints

11 endpoints across 5 groups. See references/api-spec.lap for full details.

### clitoken
| Method | Path | Description |
|--------|------|-------------|
| POST | /clitoken/{Name} | Creates a CLI token for the Airflow CLI. To learn more, see Creating an Apache Airflow CLI token. |

### environments
| Method | Path | Description |
|--------|------|-------------|
| PUT | /environments/{Name} | Creates an Amazon Managed Workflows for Apache Airflow (MWAA) environment. |
| DELETE | /environments/{Name} | Deletes an Amazon Managed Workflows for Apache Airflow (MWAA) environment. |
| GET | /environments/{Name} | Describes an Amazon Managed Workflows for Apache Airflow (MWAA) environment. |
| GET | /environments | Lists the Amazon Managed Workflows for Apache Airflow (MWAA) environments. |
| PATCH | /environments/{Name} | Updates an Amazon Managed Workflows for Apache Airflow (MWAA) environment. |

### webtoken
| Method | Path | Description |
|--------|------|-------------|
| POST | /webtoken/{Name} | Creates a web login token for the Airflow Web UI. To learn more, see Creating an Apache Airflow web login token. |

### tags
| Method | Path | Description |
|--------|------|-------------|
| GET | /tags/{ResourceArn} | Lists the key-value tag pairs associated to the Amazon Managed Workflows for Apache Airflow (MWAA) environment. For example, "Environment": "Staging". |
| POST | /tags/{ResourceArn} | Associates key-value tag pairs to your Amazon Managed Workflows for Apache Airflow (MWAA) environment. |
| DELETE | /tags/{ResourceArn} | Removes key-value tag pairs associated to your Amazon Managed Workflows for Apache Airflow (MWAA) environment. For example, "Environment": "Staging". |

### metrics
| Method | Path | Description |
|--------|------|-------------|
| POST | /metrics/environments/{EnvironmentName} | Internal only. Publishes environment health metrics to Amazon CloudWatch. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new MWAA environment?" -> PUT /environments/{Name}
- "List all my Airflow environments" -> GET /environments
- "Get details about a specific environment" -> GET /environments/{Name}
- "What's the status of my environment?" -> GET /environments/{Name}
- "Delete an Airflow environment" -> DELETE /environments/{Name}
- "Update the Airflow version for an environment" -> PATCH /environments/{Name}
- "Scale up the number of workers" -> PATCH /environments/{Name}
- "Get a CLI token to access Airflow" -> POST /clitoken/{Name}
- "Get a web login token for the Airflow UI" -> POST /webtoken/{Name}
- "What tags are on my environment?" -> GET /tags/{ResourceArn}
- "Add tags to an environment" -> POST /tags/{ResourceArn}
- "Remove tags from an environment" -> DELETE /tags/{ResourceArn}
- "Publish custom metrics for my environment" -> POST /metrics/environments/{EnvironmentName}
- "Change the DAG S3 path or plugins path" -> PATCH /environments/{Name}
- "Check if an environment update failed and why" -> GET /environments/{Name}

## Response Tips

- **Environments list:** Returns environment names as plain strings, not full objects. Call GET /environments/{Name} per entry for details. Paginate with `NextToken`/`MaxResults`.
- **Environment detail:** Deeply nested. Check `Environment.Status` for state, `Environment.LastUpdate.Error` for failure reasons. Timestamps are ISO format.
- **Create/Update:** Returns only the `Arn`. Poll GET /environments/{Name} and watch `Status` to track progress.
- **Tokens:** `CliToken` and `WebToken` are short-lived. Use `WebServerHostname` to construct the target URL.
- **Tags:** Returned as a flat string-to-string map. DELETE requires `tagKeys` as a list of key names, not key-value pairs.
- **Metrics:** Fire-and-forget. No meaningful response body on success.

## Anomaly Flags

- **Environment stuck in transitional status:** Surface when `Status` is `CREATING`, `UPDATING`, or `DELETING` for an extended period -- compare against `LastUpdate.CreatedAt`.
- **Update errors:** Proactively surface `LastUpdate.Error.ErrorCode` and `ErrorMessage` when `LastUpdate.Status` is `FAILED`.
- **Airflow version drift:** Flag when `AirflowVersion` is significantly behind the latest supported version.
- **Worker scaling limits:** Alert when `MaxWorkers` equals `MinWorkers` (no autoscaling headroom) or when values seem misconfigured (min > max).
- **Missing logging configuration:** Flag when any log module (`DagProcessingLogs`, `SchedulerLogs`, `WorkerLogs`, `TaskLogs`, `WebserverLogs`) has `Enabled: false` -- likely unintentional in production.
- **Public webserver access:** Surface when `WebserverAccessMode` is not set to private, as this exposes the Airflow UI publicly.

## Playbook

### Create and Verify a New Environment

1. Call PUT /environments/{Name} with required fields: `ExecutionRoleArn`, `SourceBucketArn`, `DagS3Path`, and `NetworkConfiguration` (subnets + security groups).
2. Note the returned `Arn`.
3. Poll GET /environments/{Name} until `Environment.Status` changes from `CREATING` to `AVAILABLE`.
4. If status becomes `CREATE_FAILED`, inspect `Environment.LastUpdate.Error` for the cause.
5. Call POST /webtoken/{Name} to get a web token and open the Airflow UI at `WebServerHostname`.

### Update Airflow Version or Configuration

1. Call GET /environments/{Name} to confirm current `Status` is `AVAILABLE` (updates fail on transitional states).
2. Call PATCH /environments/{Name} with the fields to change (e.g., `AirflowVersion`, `AirflowConfigurationOptions`).
3. Poll GET /environments/{Name} until `Environment.Status` returns to `AVAILABLE`.
4. Check `LastUpdate.Status` -- if `FAILED`, read `LastUpdate.Error` and retry after fixing.

### Scale Workers and Webservers

1. Call GET /environments/{Name} to check current `MinWorkers`, `MaxWorkers`, `MinWebservers`, `MaxWebservers`.
2. Call PATCH /environments/{Name} with updated scaling values.
3. Poll GET /environments/{Name} to confirm the update completes successfully.

### Access the Airflow CLI Remotely

1. Call POST /clitoken/{Name} to obtain a short-lived `CliToken` and the `WebServerHostname`.
2. Use the token to authenticate CLI commands against `https://{WebServerHostname}/aws_mwaa/cli`.
3. If the token expires, request a new one -- tokens are not refreshable.

### Tag Management for Cost Tracking

1. Call GET /tags/{ResourceArn} to list existing tags on the environment.
2. Call POST /tags/{ResourceArn} with a map of new or updated key-value pairs to add tags.
3. Call DELETE /tags/{ResourceArn} with `tagKeys` listing the key names to remove.
4. Verify changes by calling GET /tags/{ResourceArn} again.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
