---
name: servicenow-table-api
description: "ServiceNow Table API skill. Use when working with ServiceNow Table for now. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# ServiceNow Table API
API version: 1.0.0

## Auth
ApiKey JSESSIONID in cookie | ApiKey X-UserToken in header

## Base URL
Not specified.

## Setup
1. Set your API key in the appropriate header
2. GET /now/table/{tableName} -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### now
| Method | Path | Description |
|--------|------|-------------|
| GET | /now/table/{tableName} | Retrieves multiple records for the specified table. |

## Enhanced Skill Content
## Question Mapping

- "How do I list all incidents?" -> GET /now/table/incident
- "How do I get a specific record by sys_id?" -> GET /now/table/{tableName}?sysparm_query=sys_id={id}
- "How do I filter records by field value?" -> GET /now/table/{tableName}?sysparm_query={field}={value}
- "How do I return only certain fields from a table?" -> GET /now/table/{tableName}?sysparm_fields={field1},{field2}
- "How do I query open incidents assigned to a user?" -> GET /now/table/incident?sysparm_query=state=1^assigned_to={user_sys_id}
- "How do I get all users in a specific group?" -> GET /now/table/sys_user_grmember?sysparm_query=group={group_sys_id}&sysparm_fields=user
- "How do I search for a record by name?" -> GET /now/table/{tableName}?sysparm_query=nameLIKE{value}
- "How do I get change requests created this week?" -> GET /now/table/change_request?sysparm_query=sys_created_onONThis week@javascript:gs.beginningOfThisWeek()@javascript:gs.endOfThisWeek()
- "How do I check if a table exists?" -> GET /now/table/{tableName} (404 indicates table not found)
- "How do I get records sorted by a field?" -> GET /now/table/{tableName}?sysparm_query=ORDERBYDESCsys_created_on
- "How do I get the schema or columns of a table?" -> GET /now/table/{tableName}?sysparm_fields=sys_id&sysparm_query=sys_id=invalid (inspect response structure)
- "How do I combine multiple query conditions?" -> GET /now/table/{tableName}?sysparm_query={cond1}^{cond2} (^ is AND, ^OR is OR)
- "How do I get XML instead of JSON?" -> GET /now/table/{tableName} with Accept: application/xml

## Response Tips

- **Successful queries**: Response body contains a `result` array of maps; an empty `result: []` means no matching records, not an error.
- **Single record lookups**: Still returns `result` as an array -- expect one element, not a bare object.
- **Reference fields**: Values like `assigned_to` return as `{"link": "...", "value": "sys_id"}` objects, not display names; use `sysparm_display_value=true` or dot-walk fields in `sysparm_fields` to resolve them.
- **Error responses**: 401 means auth cookie/token expired; 403 means ACL restriction on the table; 404 means the table name is invalid.

## Anomaly Flags

- **401 or 403 on previously working requests**: Auth session likely expired -- surface immediately and suggest re-authentication.
- **Empty result set on broad queries**: May indicate ACL restrictions silently filtering rows rather than genuinely empty tables -- flag if the table is expected to have data (e.g., `incident`, `sys_user`).
- **Response contains `error` key**: ServiceNow sometimes returns 200 with an error object inside the body -- always check for `error.message` even on 2xx.
- **Extremely large result sets**: If `result` contains hundreds of records, warn that the response may be truncated by server-side row limits (default 10,000) and suggest adding `sysparm_limit` and `sysparm_offset` for pagination.
- **Deprecated or renamed tables**: If a 404 is returned for well-known tables (e.g., `u_*` prefixed custom tables), flag that the instance may have renamed or removed them.
- **Slow responses (>5s)**: Complex `sysparm_query` with deep dot-walking or unindexed fields can cause performance issues -- suggest simplifying the query or adding table indexes.

## Playbook

### 1. Retrieve and Filter Incident Records

1. Authenticate and set `X-UserToken` header or `JSESSIONID` cookie.
2. `GET /now/table/incident?sysparm_query=state=1&sysparm_fields=number,short_description,assigned_to,priority` to fetch open incidents with key fields.
3. If results are large, add `sysparm_limit=50&sysparm_offset=0` and paginate by incrementing `sysparm_offset`.
4. To resolve reference fields, re-query with `sysparm_display_value=true` or dot-walk: `sysparm_fields=assigned_to.name`.

### 2. Search for a Record Across Tables

1. Start with the most likely table: `GET /now/table/incident?sysparm_query=numberSTARTSWITH{prefix}`.
2. If no results, try `change_request`, `problem`, or `sc_request` with the same query pattern.
3. For free-text search, use `LIKE` operator: `sysparm_query=short_descriptionLIKE{keyword}`.
4. Narrow with additional conditions using `^` (AND): `short_descriptionLIKE{keyword}^state!=7`.

### 3. Export Specific Fields from Any Table

1. Identify the target table name (e.g., `cmdb_ci_server` for servers).
2. `GET /now/table/{tableName}?sysparm_fields=name,sys_id,sys_class_name&sysparm_query=active=true` to fetch only needed columns.
3. Page through all records with `sysparm_limit=100&sysparm_offset=0`, incrementing offset by 100 each call.
4. Stop when `result` returns fewer records than the limit.

### 4. Validate Table Access and Permissions

1. `GET /now/table/{tableName}?sysparm_limit=1` to test access with minimal data transfer.
2. If 200 with `result`, the table is accessible -- inspect the returned map keys to understand available fields.
3. If 403, the authenticated user lacks ACL permissions for this table -- escalate or use an admin token.
4. If 404, the table name is incorrect -- check spelling or query `sys_db_object` for valid table names: `GET /now/table/sys_db_object?sysparm_query=nameLIKE{guess}&sysparm_fields=name,label`.

### 5. Build Complex Encoded Queries

1. Start simple: `sysparm_query=priority=1` (Critical priority).
2. Chain AND conditions with `^`: `priority=1^state=1` (Critical AND open).
3. Add OR groups with `^OR`: `priority=1^state=1^ORpriority=2^state=1`.
4. Add sorting: append `^ORDERBYDESCsys_updated_on` to the end of the query string.
5. Test incrementally -- add one condition at a time and verify results before building the full query.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
