---
name: twilio-taskrouter
description: "Twilio - Taskrouter API skill. Use when working with Twilio - Taskrouter for Workspaces. Covers 61 endpoints."
version: 1.0.0
generator: lapsh
---

# Twilio - Taskrouter
API version: 1.0.0

## Auth
Bearer basic

## Base URL
https://taskrouter.twilio.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /v1/Workspaces -- verify access
3. POST /v1/Workspaces/{WorkspaceSid}/Activities/{Sid} -- create first Activities

## Endpoints

61 endpoints across 1 groups. See references/api-spec.lap for full details.

### Workspaces
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/Workspaces/{WorkspaceSid}/Activities/{Sid} |  |
| POST | /v1/Workspaces/{WorkspaceSid}/Activities/{Sid} |  |
| DELETE | /v1/Workspaces/{WorkspaceSid}/Activities/{Sid} |  |
| GET | /v1/Workspaces/{WorkspaceSid}/Activities |  |
| POST | /v1/Workspaces/{WorkspaceSid}/Activities |  |
| GET | /v1/Workspaces/{WorkspaceSid}/Events/{Sid} |  |
| GET | /v1/Workspaces/{WorkspaceSid}/Events |  |
| GET | /v1/Workspaces/{WorkspaceSid}/Tasks/{Sid} |  |
| POST | /v1/Workspaces/{WorkspaceSid}/Tasks/{Sid} |  |
| DELETE | /v1/Workspaces/{WorkspaceSid}/Tasks/{Sid} |  |
| GET | /v1/Workspaces/{WorkspaceSid}/Tasks |  |
| POST | /v1/Workspaces/{WorkspaceSid}/Tasks |  |
| GET | /v1/Workspaces/{WorkspaceSid}/TaskChannels/{Sid} |  |
| POST | /v1/Workspaces/{WorkspaceSid}/TaskChannels/{Sid} |  |
| DELETE | /v1/Workspaces/{WorkspaceSid}/TaskChannels/{Sid} |  |
| GET | /v1/Workspaces/{WorkspaceSid}/TaskChannels |  |
| POST | /v1/Workspaces/{WorkspaceSid}/TaskChannels |  |
| GET | /v1/Workspaces/{WorkspaceSid}/TaskQueues/{Sid} |  |
| POST | /v1/Workspaces/{WorkspaceSid}/TaskQueues/{Sid} |  |
| DELETE | /v1/Workspaces/{WorkspaceSid}/TaskQueues/{Sid} |  |
| GET | /v1/Workspaces/{WorkspaceSid}/TaskQueues |  |
| POST | /v1/Workspaces/{WorkspaceSid}/TaskQueues |  |
| POST | /v1/Workspaces/{WorkspaceSid}/TaskQueues/RealTimeStatistics | Fetch a Task Queue Real Time Statistics in bulk for the array of TaskQueue SIDs, support upto 50 in a request. |
| GET | /v1/Workspaces/{WorkspaceSid}/TaskQueues/{TaskQueueSid}/CumulativeStatistics |  |
| GET | /v1/Workspaces/{WorkspaceSid}/TaskQueues/{TaskQueueSid}/RealTimeStatistics |  |
| GET | /v1/Workspaces/{WorkspaceSid}/TaskQueues/{TaskQueueSid}/Statistics |  |
| GET | /v1/Workspaces/{WorkspaceSid}/TaskQueues/Statistics |  |
| GET | /v1/Workspaces/{WorkspaceSid}/Tasks/{TaskSid}/Reservations |  |
| GET | /v1/Workspaces/{WorkspaceSid}/Tasks/{TaskSid}/Reservations/{Sid} |  |
| POST | /v1/Workspaces/{WorkspaceSid}/Tasks/{TaskSid}/Reservations/{Sid} |  |
| GET | /v1/Workspaces/{WorkspaceSid}/Workers |  |
| POST | /v1/Workspaces/{WorkspaceSid}/Workers |  |
| GET | /v1/Workspaces/{WorkspaceSid}/Workers/{Sid} |  |
| POST | /v1/Workspaces/{WorkspaceSid}/Workers/{Sid} |  |
| DELETE | /v1/Workspaces/{WorkspaceSid}/Workers/{Sid} |  |
| GET | /v1/Workspaces/{WorkspaceSid}/Workers/{WorkerSid}/Channels |  |
| GET | /v1/Workspaces/{WorkspaceSid}/Workers/{WorkerSid}/Channels/{Sid} |  |
| POST | /v1/Workspaces/{WorkspaceSid}/Workers/{WorkerSid}/Channels/{Sid} |  |
| GET | /v1/Workspaces/{WorkspaceSid}/Workers/{WorkerSid}/Statistics |  |
| GET | /v1/Workspaces/{WorkspaceSid}/Workers/{WorkerSid}/Reservations |  |
| GET | /v1/Workspaces/{WorkspaceSid}/Workers/{WorkerSid}/Reservations/{Sid} |  |
| POST | /v1/Workspaces/{WorkspaceSid}/Workers/{WorkerSid}/Reservations/{Sid} |  |
| GET | /v1/Workspaces/{WorkspaceSid}/Workers/Statistics |  |
| GET | /v1/Workspaces/{WorkspaceSid}/Workers/CumulativeStatistics |  |
| GET | /v1/Workspaces/{WorkspaceSid}/Workers/RealTimeStatistics |  |
| GET | /v1/Workspaces/{WorkspaceSid}/Workflows/{Sid} |  |
| POST | /v1/Workspaces/{WorkspaceSid}/Workflows/{Sid} |  |
| DELETE | /v1/Workspaces/{WorkspaceSid}/Workflows/{Sid} |  |
| GET | /v1/Workspaces/{WorkspaceSid}/Workflows |  |
| POST | /v1/Workspaces/{WorkspaceSid}/Workflows |  |
| GET | /v1/Workspaces/{WorkspaceSid}/Workflows/{WorkflowSid}/CumulativeStatistics |  |
| GET | /v1/Workspaces/{WorkspaceSid}/Workflows/{WorkflowSid}/RealTimeStatistics |  |
| GET | /v1/Workspaces/{WorkspaceSid}/Workflows/{WorkflowSid}/Statistics |  |
| GET | /v1/Workspaces/{Sid} |  |
| POST | /v1/Workspaces/{Sid} |  |
| DELETE | /v1/Workspaces/{Sid} |  |
| GET | /v1/Workspaces |  |
| POST | /v1/Workspaces |  |
| GET | /v1/Workspaces/{WorkspaceSid}/CumulativeStatistics |  |
| GET | /v1/Workspaces/{WorkspaceSid}/RealTimeStatistics |  |
| GET | /v1/Workspaces/{WorkspaceSid}/Statistics |  |

## Enhanced Skill Content
## Question Mapping

- "What workspaces do I have?" -> GET /v1/Workspaces
- "Show me the details of a specific workspace" -> GET /v1/Workspaces/{Sid}
- "How do I create a new workspace?" -> POST /v1/Workspaces
- "What tasks are currently pending in my workspace?" -> GET /v1/Workspaces/{WorkspaceSid}/Tasks (use AssignmentStatus filter)
- "Which workers are available right now?" -> GET /v1/Workspaces/{WorkspaceSid}/Workers (use Available filter)
- "How long has the oldest task been waiting?" -> GET /v1/Workspaces/{WorkspaceSid}/RealTimeStatistics (check longest_task_waiting_age)
- "What happened in the last hour in my workspace?" -> GET /v1/Workspaces/{WorkspaceSid}/Events (use StartDate/Minutes filters)
- "How many reservations were accepted vs rejected today?" -> GET /v1/Workspaces/{WorkspaceSid}/CumulativeStatistics (use StartDate/EndDate)
- "What is a specific worker's current activity and availability?" -> GET /v1/Workspaces/{WorkspaceSid}/Workers/{Sid}
- "How do I accept or reject a reservation?" -> POST /v1/Workspaces/{WorkspaceSid}/Tasks/{TaskSid}/Reservations/{Sid} (set reservation_status)
- "What task queues exist and how are they configured?" -> GET /v1/Workspaces/{WorkspaceSid}/TaskQueues
- "How many tasks are in each queue right now?" -> POST /v1/Workspaces/{WorkspaceSid}/TaskQueues/RealTimeStatistics
- "What channels does a specific worker handle and what capacity is left?" -> GET /v1/Workspaces/{WorkspaceSid}/Workers/{WorkerSid}/Channels
- "Show me a worker's reservation history" -> GET /v1/Workspaces/{WorkspaceSid}/Workers/{WorkerSid}/Reservations
- "What workflows are configured and what are their timeout settings?" -> GET /v1/Workspaces/{WorkspaceSid}/Workflows

## Response Tips

- **List endpoints** (Tasks, Workers, Activities, etc.): Results are in a named array (e.g., `tasks`, `workers`) with a `meta` object containing pagination; follow `meta.next_page_url` until it is `null` to page through all results. Default `page_size` varies -- set `PageSize` explicitly for predictable batching.
- **Single resource endpoints**: Return flat objects with all fields nullable (`str?`); always null-check before using values. The `links` map contains related sub-resource URLs -- prefer these over constructing URLs manually.
- **Statistics endpoints**: Return `cumulative` and/or `realtime` as opaque `any` objects containing nested counters and duration breakdowns; the combined `/Statistics` endpoint wraps both. Use `SplitByWaitTime` to get wait-time bucket breakdowns.
- **Mutating endpoints** (POST create/update): 201 for creation, 200 for updates; the full updated resource is returned. `If-Match` header on Tasks, Workers, and Reservations enables optimistic concurrency -- a 412 means the resource changed since you last read it.
- **DELETE endpoints**: Return 204 with no body on success; a 404 means the resource was already deleted or never existed.
- **Events**: The `event_data` field is an opaque `any` that varies by `event_type` -- inspect `event_type` first to know the shape. `event_date_ms` is epoch milliseconds for precise ordering.

## Anomaly Flags

- **Longest task waiting age is high**: Surface when `longest_task_waiting_age` from RealTimeStatistics exceeds a reasonable threshold (e.g., 300+ seconds), indicating tasks are stuck without assignment.
- **Zero available workers**: Flag when `total_available_workers` on a TaskQueue or `total_workers` with `Available=true` returns 0 -- no one can accept tasks.
- **High reservation rejection/timeout rate**: When CumulativeStatistics shows `reservations_rejected` or `reservations_timed_out` significantly exceeding `reservations_accepted`, routing or staffing may need attention.
- **Optimistic concurrency conflicts (412)**: If POST updates to Tasks, Workers, or Reservations with `If-Match` return 412, surface the conflict -- another process modified the resource. Re-fetch and retry.
- **Worker capacity exhausted**: When a worker channel shows `available_capacity_percentage` at 0 and `available` is false, that worker cannot take more tasks on that channel.
- **Tasks timing out in workflow**: When `tasks_timed_out_in_workflow` in CumulativeStatistics is non-zero, workflows may have overly aggressive timeouts or no fallback routing.
- **Unbalanced queue depths**: When bulk TaskQueue RealTimeStatistics shows one queue with significantly more `total_tasks` than others, routing expressions or worker targeting may need rebalancing.

## Playbook

### 1. Create a Workspace and Set Up Task Routing

1. POST /v1/Workspaces to create a new workspace (set `friendly_name`, `event_callback_url` if needed)
2. POST /v1/Workspaces/{WorkspaceSid}/Activities to create activities (e.g., "Available", "Offline", "Break") -- note the returned `sid` for each
3. POST /v1/Workspaces/{WorkspaceSid}/TaskQueues to create task queues (set `target_workers` expression, `assignment_activity_sid`, `reservation_activity_sid`)
4. POST /v1/Workspaces/{WorkspaceSid}/Workflows to create a workflow with routing `configuration` JSON referencing the queue SIDs
5. POST /v1/Workspaces/{WorkspaceSid}/Workers to add workers (set `attributes` JSON for skill-based routing)
6. POST /v1/Workspaces/{Sid} to update the workspace `default_activity_sid` and `timeout_activity_sid`

### 2. Submit a Task and Track It Through Assignment

1. POST /v1/Workspaces/{WorkspaceSid}/Tasks to create a task (set `attributes` JSON with routing info, `workflow_sid`, optional `priority` and `timeout`)
2. GET /v1/Workspaces/{WorkspaceSid}/Tasks/{Sid} to poll task status -- watch `assignment_status` transition from `pending` to `reserved`
3. GET /v1/Workspaces/{WorkspaceSid}/Tasks/{TaskSid}/Reservations to find the reservation created for this task
4. POST /v1/Workspaces/{WorkspaceSid}/Tasks/{TaskSid}/Reservations/{Sid} to accept the reservation (set `reservation_status` to `accepted`)
5. POST /v1/Workspaces/{WorkspaceSid}/Tasks/{Sid} to complete the task when done (set `assignment_status` to `completed`)

### 3. Monitor Workspace Health in Real Time

1. GET /v1/Workspaces/{WorkspaceSid}/RealTimeStatistics to get current `total_tasks`, `total_workers`, `longest_task_waiting_age`, and `tasks_by_status`
2. GET /v1/Workspaces/{WorkspaceSid}/Workers/RealTimeStatistics to see worker distribution across activities (`activity_statistics`)
3. POST /v1/Workspaces/{WorkspaceSid}/TaskQueues/RealTimeStatistics to get per-queue task counts and available workers in bulk
4. Flag any queue where `total_available_workers` is 0 but `total_tasks` > 0
5. Check `longest_task_waiting_age` -- if over threshold, investigate the matching `longest_task_waiting_sid` via GET /v1/Workspaces/{WorkspaceSid}/Tasks/{Sid}

### 4. Investigate a Problematic Task or Worker Using Events

1. GET /v1/Workspaces/{WorkspaceSid}/Events with `TaskSid` filter to see all events for a specific task (creation, reservation, acceptance/rejection, completion)
2. Alternatively, filter by `WorkerSid` to trace a worker's activity changes and reservation actions
3. Use `StartDate`/`EndDate` or `Minutes` to narrow the time window
4. Inspect each event's `event_type` and `event_data` to understand what happened and when
5. Cross-reference `actor_sid` to identify which worker, workflow, or system action triggered each event

### 5. Rebalance Worker Capacity Across Channels

1. GET /v1/Workspaces/{WorkspaceSid}/Workers/{WorkerSid}/Channels to see current capacity and assigned tasks per channel
2. Identify channels where `available_capacity_percentage` is 0 (saturated) or 100 (idle)
3. POST /v1/Workspaces/{WorkspaceSid}/Workers/{WorkerSid}/Channels/{Sid} to adjust `capacity` or `available` for overloaded/underused channels
4. GET /v1/Workspaces/{WorkspaceSid}/Workers/{WorkerSid}/Statistics to verify the change improved throughput
5. Repeat across workers as needed, using GET /v1/Workspaces/{WorkspaceSid}/Workers with `TaskQueueSid` filter to find workers assigned to specific queues


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
