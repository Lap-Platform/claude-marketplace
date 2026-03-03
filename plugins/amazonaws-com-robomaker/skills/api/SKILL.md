---
name: aws-robomaker
description: "AWS RoboMaker API skill. Use when working with AWS RoboMaker for batchDeleteWorlds, batchDescribeSimulationJob, cancelDeploymentJob. Covers 57 endpoints."
version: 1.0.0
generator: lapsh
---

# AWS RoboMaker
API version: 2018-06-29

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
2. GET /tags/{resourceArn} -- verify access
3. POST /batchDeleteWorlds -- create first batchDeleteWorlds

## Endpoints

57 endpoints across 55 groups. See references/api-spec.lap for full details.

### batchDeleteWorlds
| Method | Path | Description |
|--------|------|-------------|
| POST | /batchDeleteWorlds | Deletes one or more worlds in a batch operation. |

### batchDescribeSimulationJob
| Method | Path | Description |
|--------|------|-------------|
| POST | /batchDescribeSimulationJob | Describes one or more simulation jobs. |

### cancelDeploymentJob
| Method | Path | Description |
|--------|------|-------------|
| POST | /cancelDeploymentJob | Cancels the specified deployment job.  This API will no longer be supported as of May 2, 2022. Use it to remove resources that were created for Deployment Service. |

### cancelSimulationJob
| Method | Path | Description |
|--------|------|-------------|
| POST | /cancelSimulationJob | Cancels the specified simulation job. |

### cancelSimulationJobBatch
| Method | Path | Description |
|--------|------|-------------|
| POST | /cancelSimulationJobBatch | Cancels a simulation job batch. When you cancel a simulation job batch, you are also cancelling all of the active simulation jobs created as part of the batch. |

### cancelWorldExportJob
| Method | Path | Description |
|--------|------|-------------|
| POST | /cancelWorldExportJob | Cancels the specified export job. |

### cancelWorldGenerationJob
| Method | Path | Description |
|--------|------|-------------|
| POST | /cancelWorldGenerationJob | Cancels the specified world generator job. |

### createDeploymentJob
| Method | Path | Description |
|--------|------|-------------|
| POST | /createDeploymentJob | Deploys a specific version of a robot application to robots in a fleet.  This API is no longer supported and will throw an error if used.  The robot application must have a numbered applicationVersion for consistency reasons. To create a new version, use CreateRobotApplicationVersion or see Creating a Robot Application Version.   After 90 days, deployment jobs expire and will be deleted. They will no longer be accessible. |

### createFleet
| Method | Path | Description |
|--------|------|-------------|
| POST | /createFleet | Creates a fleet, a logical group of robots running the same robot application.  This API is no longer supported and will throw an error if used. |

### createRobot
| Method | Path | Description |
|--------|------|-------------|
| POST | /createRobot | Creates a robot.  This API is no longer supported and will throw an error if used. |

### createRobotApplication
| Method | Path | Description |
|--------|------|-------------|
| POST | /createRobotApplication | Creates a robot application. |

### createRobotApplicationVersion
| Method | Path | Description |
|--------|------|-------------|
| POST | /createRobotApplicationVersion | Creates a version of a robot application. |

### createSimulationApplication
| Method | Path | Description |
|--------|------|-------------|
| POST | /createSimulationApplication | Creates a simulation application. |

### createSimulationApplicationVersion
| Method | Path | Description |
|--------|------|-------------|
| POST | /createSimulationApplicationVersion | Creates a simulation application with a specific revision id. |

### createSimulationJob
| Method | Path | Description |
|--------|------|-------------|
| POST | /createSimulationJob | Creates a simulation job.  After 90 days, simulation jobs expire and will be deleted. They will no longer be accessible. |

### createWorldExportJob
| Method | Path | Description |
|--------|------|-------------|
| POST | /createWorldExportJob | Creates a world export job. |

### createWorldGenerationJob
| Method | Path | Description |
|--------|------|-------------|
| POST | /createWorldGenerationJob | Creates worlds using the specified template. |

### createWorldTemplate
| Method | Path | Description |
|--------|------|-------------|
| POST | /createWorldTemplate | Creates a world template. |

### deleteFleet
| Method | Path | Description |
|--------|------|-------------|
| POST | /deleteFleet | Deletes a fleet.  This API will no longer be supported as of May 2, 2022. Use it to remove resources that were created for Deployment Service. |

### deleteRobot
| Method | Path | Description |
|--------|------|-------------|
| POST | /deleteRobot | Deletes a robot.  This API will no longer be supported as of May 2, 2022. Use it to remove resources that were created for Deployment Service. |

### deleteRobotApplication
| Method | Path | Description |
|--------|------|-------------|
| POST | /deleteRobotApplication | Deletes a robot application. |

### deleteSimulationApplication
| Method | Path | Description |
|--------|------|-------------|
| POST | /deleteSimulationApplication | Deletes a simulation application. |

### deleteWorldTemplate
| Method | Path | Description |
|--------|------|-------------|
| POST | /deleteWorldTemplate | Deletes a world template. |

### deregisterRobot
| Method | Path | Description |
|--------|------|-------------|
| POST | /deregisterRobot | Deregisters a robot.  This API will no longer be supported as of May 2, 2022. Use it to remove resources that were created for Deployment Service. |

### describeDeploymentJob
| Method | Path | Description |
|--------|------|-------------|
| POST | /describeDeploymentJob | Describes a deployment job.  This API will no longer be supported as of May 2, 2022. Use it to remove resources that were created for Deployment Service. |

### describeFleet
| Method | Path | Description |
|--------|------|-------------|
| POST | /describeFleet | Describes a fleet.  This API will no longer be supported as of May 2, 2022. Use it to remove resources that were created for Deployment Service. |

### describeRobot
| Method | Path | Description |
|--------|------|-------------|
| POST | /describeRobot | Describes a robot.  This API will no longer be supported as of May 2, 2022. Use it to remove resources that were created for Deployment Service. |

### describeRobotApplication
| Method | Path | Description |
|--------|------|-------------|
| POST | /describeRobotApplication | Describes a robot application. |

### describeSimulationApplication
| Method | Path | Description |
|--------|------|-------------|
| POST | /describeSimulationApplication | Describes a simulation application. |

### describeSimulationJob
| Method | Path | Description |
|--------|------|-------------|
| POST | /describeSimulationJob | Describes a simulation job. |

### describeSimulationJobBatch
| Method | Path | Description |
|--------|------|-------------|
| POST | /describeSimulationJobBatch | Describes a simulation job batch. |

### describeWorld
| Method | Path | Description |
|--------|------|-------------|
| POST | /describeWorld | Describes a world. |

### describeWorldExportJob
| Method | Path | Description |
|--------|------|-------------|
| POST | /describeWorldExportJob | Describes a world export job. |

### describeWorldGenerationJob
| Method | Path | Description |
|--------|------|-------------|
| POST | /describeWorldGenerationJob | Describes a world generation job. |

### describeWorldTemplate
| Method | Path | Description |
|--------|------|-------------|
| POST | /describeWorldTemplate | Describes a world template. |

### getWorldTemplateBody
| Method | Path | Description |
|--------|------|-------------|
| POST | /getWorldTemplateBody | Gets the world template body. |

### listDeploymentJobs
| Method | Path | Description |
|--------|------|-------------|
| POST | /listDeploymentJobs | Returns a list of deployment jobs for a fleet. You can optionally provide filters to retrieve specific deployment jobs.  This API will no longer be supported as of May 2, 2022. Use it to remove resources that were created for Deployment Service. |

### listFleets
| Method | Path | Description |
|--------|------|-------------|
| POST | /listFleets | Returns a list of fleets. You can optionally provide filters to retrieve specific fleets.  This API will no longer be supported as of May 2, 2022. Use it to remove resources that were created for Deployment Service. |

### listRobotApplications
| Method | Path | Description |
|--------|------|-------------|
| POST | /listRobotApplications | Returns a list of robot application. You can optionally provide filters to retrieve specific robot applications. |

### listRobots
| Method | Path | Description |
|--------|------|-------------|
| POST | /listRobots | Returns a list of robots. You can optionally provide filters to retrieve specific robots.  This API will no longer be supported as of May 2, 2022. Use it to remove resources that were created for Deployment Service. |

### listSimulationApplications
| Method | Path | Description |
|--------|------|-------------|
| POST | /listSimulationApplications | Returns a list of simulation applications. You can optionally provide filters to retrieve specific simulation applications. |

### listSimulationJobBatches
| Method | Path | Description |
|--------|------|-------------|
| POST | /listSimulationJobBatches | Returns a list simulation job batches. You can optionally provide filters to retrieve specific simulation batch jobs. |

### listSimulationJobs
| Method | Path | Description |
|--------|------|-------------|
| POST | /listSimulationJobs | Returns a list of simulation jobs. You can optionally provide filters to retrieve specific simulation jobs. |

### tags
| Method | Path | Description |
|--------|------|-------------|
| GET | /tags/{resourceArn} | Lists all tags on a AWS RoboMaker resource. |
| POST | /tags/{resourceArn} | Adds or edits tags for a AWS RoboMaker resource. Each tag consists of a tag key and a tag value. Tag keys and tag values are both required, but tag values can be empty strings.  For information about the rules that apply to tag keys and tag values, see User-Defined Tag Restrictions in the AWS Billing and Cost Management User Guide. |
| DELETE | /tags/{resourceArn} | Removes the specified tags from the specified AWS RoboMaker resource. To remove a tag, specify the tag key. To change the tag value of an existing tag key, use  TagResource . |

### listWorldExportJobs
| Method | Path | Description |
|--------|------|-------------|
| POST | /listWorldExportJobs | Lists world export jobs. |

### listWorldGenerationJobs
| Method | Path | Description |
|--------|------|-------------|
| POST | /listWorldGenerationJobs | Lists world generator jobs. |

### listWorldTemplates
| Method | Path | Description |
|--------|------|-------------|
| POST | /listWorldTemplates | Lists world templates. |

### listWorlds
| Method | Path | Description |
|--------|------|-------------|
| POST | /listWorlds | Lists worlds. |

### registerRobot
| Method | Path | Description |
|--------|------|-------------|
| POST | /registerRobot | Registers a robot with a fleet.  This API is no longer supported and will throw an error if used. |

### restartSimulationJob
| Method | Path | Description |
|--------|------|-------------|
| POST | /restartSimulationJob | Restarts a running simulation job. |

### startSimulationJobBatch
| Method | Path | Description |
|--------|------|-------------|
| POST | /startSimulationJobBatch | Starts a new simulation job batch. The batch is defined using one or more SimulationJobRequest objects. |

### syncDeploymentJob
| Method | Path | Description |
|--------|------|-------------|
| POST | /syncDeploymentJob | Syncrhonizes robots in a fleet to the latest deployment. This is helpful if robots were added after a deployment.  This API will no longer be supported as of May 2, 2022. Use it to remove resources that were created for Deployment Service. |

### updateRobotApplication
| Method | Path | Description |
|--------|------|-------------|
| POST | /updateRobotApplication | Updates a robot application. |

### updateSimulationApplication
| Method | Path | Description |
|--------|------|-------------|
| POST | /updateSimulationApplication | Updates a simulation application. |

### updateWorldTemplate
| Method | Path | Description |
|--------|------|-------------|
| POST | /updateWorldTemplate | Updates a world template. |

## Enhanced Skill Content
## Question Mapping

- "How do I run a simulation in RoboMaker?" -> POST /createSimulationJob
- "What simulations are currently running?" -> POST /listSimulationJobs
- "Why did my simulation job fail?" -> POST /describeSimulationJob
- "How do I deploy my robot application to a fleet?" -> POST /createDeploymentJob
- "What robots are registered in my fleet?" -> POST /describeFleet
- "How do I create a new robot application from a Docker image?" -> POST /createRobotApplication
- "How do I generate simulated worlds from a template?" -> POST /createWorldGenerationJob
- "What worlds were created by my generation job?" -> POST /describeWorldGenerationJob
- "How do I export generated worlds to S3?" -> POST /createWorldExportJob
- "How do I run multiple simulations in parallel?" -> POST /startSimulationJobBatch
- "What's the status of my simulation batch?" -> POST /describeSimulationJobBatch
- "How do I add a robot to a fleet?" -> POST /registerRobot
- "How do I tag my RoboMaker resources?" -> POST /tags/{resourceArn}
- "How do I cancel a stuck simulation?" -> POST /cancelSimulationJob
- "How do I clean up worlds I no longer need?" -> POST /batchDeleteWorlds

## Response Tips

- **List endpoints** (`list*`): All return `nextToken` for pagination; pass it back to get the next page. Most accept `filters` (array of `Filter` objects) and `maxResults` to limit page size.
- **Describe endpoints** (`describe*`): Return the full resource with all nullable fields; always check `status` and `failureCode`/`failureReason` before reading other fields.
- **Create endpoints** (`create*`): Return the created resource echo; `arn` is the canonical identifier for all subsequent operations. Timestamps are ISO 8601.
- **Cancel/Delete endpoints**: Return empty 200 on success; no response body. Idempotent -- cancelling an already-cancelled job does not error.
- **Batch endpoints** (`batchDescribeSimulationJob`, `batchDeleteWorlds`): Always check `unprocessedJobs`/`unprocessedWorlds` for partial failures.
- **Tags** (`GET /tags/{resourceArn}`): Returns a flat `map<str,str>`; `POST` adds/overwrites, `DELETE` removes by key list.

## Anomaly Flags

- **Job failure codes**: Surface `failureCode` and `failureReason` proactively whenever a describe or create response returns a non-null value -- these indicate infrastructure issues (e.g., `InternalServiceError`, `RobotApplicationCrash`, `SimulationApplicationCrash`).
- **Partial batch failures**: When `batchDeleteWorlds` returns `unprocessedWorlds` or `batchDescribeSimulationJob` returns `unprocessedJobs`, alert the user immediately with the list of failed items.
- **Simulation batch mixed results**: After `startSimulationJobBatch`, flag if `failedRequests` is non-empty alongside `createdRequests` -- partial batch success is easy to miss.
- **World generation shortfalls**: In `describeWorldGenerationJob`, compare `finishedWorldsSummary.succeededWorlds` count against the requested `worldCount` to detect generation failures.
- **Deployment robot-level failures**: In `describeDeploymentJob`, check `robotDeploymentSummary` for individual robot deployment statuses -- fleet-level status may show success while individual robots failed.
- **Stale revision IDs**: When `updateRobotApplication` or `updateSimulationApplication` is called with `currentRevisionId` and the operation fails, flag a concurrent modification conflict.

## Playbook

### 1. Run a Simulation End-to-End

1. Create a robot application: `POST /createRobotApplication` with name, `robotSoftwareSuite`, and either `sources` or `environment` (Docker URI).
2. Create a simulation application: `POST /createSimulationApplication` with name, `simulationSoftwareSuite`, `robotSoftwareSuite`, and optionally `renderingEngine`.
3. Launch the simulation: `POST /createSimulationJob` with `iamRole`, `maxJobDurationInSeconds`, `robotApplications` (referencing step 1 ARN), and `simulationApplications` (referencing step 2 ARN). Set `outputLocation` for S3 logs.
4. Monitor status: `POST /describeSimulationJob` with the returned ARN. Poll until `status` is `Completed`, `Failed`, or `Canceled`.
5. If stuck or no longer needed: `POST /cancelSimulationJob` with the job ARN.

### 2. Deploy a Robot Application to a Fleet

1. Create a fleet: `POST /createFleet` with a name. Note the returned `arn`.
2. Register robots: `POST /registerRobot` for each robot ARN + fleet ARN pair.
3. Verify fleet membership: `POST /describeFleet` to confirm all robots appear in `robots`.
4. Create the deployment: `POST /createDeploymentJob` with `fleet` ARN, `deploymentApplicationConfigs` (app ARN, version, launch config), and optionally `deploymentConfig` for rollout parameters.
5. Monitor: `POST /describeDeploymentJob` -- check `status` and `robotDeploymentSummary` for per-robot results.

### 3. Generate and Export Simulation Worlds

1. Create a world template: `POST /createWorldTemplate` with `name` and either `templateBody` (inline) or `templateLocation` (S3 reference).
2. Launch generation: `POST /createWorldGenerationJob` with `template` ARN and `worldCount` (`floorplanCount`, `interiorCountPerFloorplan`).
3. Monitor generation: `POST /describeWorldGenerationJob` -- check `finishedWorldsSummary` for succeeded/failed counts.
4. Export to S3: `POST /createWorldExportJob` with the world ARNs from `succeededWorlds`, an `outputLocation`, and `iamRole`.
5. Verify export: `POST /describeWorldExportJob` until `status` is `Completed`.

### 4. Run a Batch of Simulations with Concurrency Control

1. Prepare simulation job requests as an array of `SimulationJobRequest` objects (each with its own robot/simulation app configs, IAM role, max duration).
2. Launch the batch: `POST /startSimulationJobBatch` with `createSimulationJobRequests` and `batchPolicy` (`maxConcurrency` to limit parallel runs, `timeoutInSeconds` for the overall batch).
3. Monitor: `POST /describeSimulationJobBatch` -- review `createdRequests`, `pendingRequests`, and `failedRequests`.
4. Cancel if needed: `POST /cancelSimulationJobBatch` stops all pending and running jobs in the batch.

### 5. Version and Update a Robot Application

1. Describe the current application: `POST /describeRobotApplication` to get the current `revisionId` and configuration.
2. Update the application: `POST /updateRobotApplication` with the new `sources` or `environment`, passing `currentRevisionId` to prevent conflicts.
3. Pin a version: `POST /createRobotApplicationVersion` with the `application` ARN to snapshot the current state as an immutable version.
4. Use the versioned ARN in `createSimulationJob` or `createDeploymentJob` to ensure reproducible runs.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
