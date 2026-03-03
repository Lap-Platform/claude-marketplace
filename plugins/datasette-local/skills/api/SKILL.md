---
name: datasette-api
description: "Datasette API skill. Use when working with Datasette for content.json. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Datasette API
API version: v1

## Auth
No authentication required.

## Base URL
https://datasette.io

## Setup
1. No auth setup needed
2. GET /content.json -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### content.json
| Method | Path | Description |
|--------|------|-------------|
| GET | /content.json | Execute a SQLite SQL query against the content database |

## Enhanced Skill Content
## Question Mapping

- "How do I run a SQL query against the database?" -> GET /content.json
- "How do I get results as an array of objects?" -> GET /content.json (`_shape=objects`)
- "How do I get results as a flat array of arrays?" -> GET /content.json (`_shape=arrays`)
- "How do I get just the raw column values?" -> GET /content.json (`_shape=array`)
- "How do I list all tables in the database?" -> GET /content.json (`sql=select name from sqlite_master where type='table'`)
- "How do I count rows in a specific table?" -> GET /content.json (`sql=select count(*) from [table]`)
- "How do I get the schema of a table?" -> GET /content.json (`sql=pragma table_info([table])`)
- "How do I filter rows matching a condition?" -> GET /content.json (`sql=select * from [table] where [condition]`)
- "How do I limit results to N rows?" -> GET /content.json (`sql=select * from [table] limit N`)
- "How do I sort results by a column?" -> GET /content.json (`sql=select * from [table] order by [col]`)
- "How do I join two tables?" -> GET /content.json (`sql=select * from a join b on a.id=b.a_id`)
- "How do I check if the database is reachable?" -> GET /content.json (`sql=select 1`)
- "How do I get distinct values from a column?" -> GET /content.json (`sql=select distinct [col] from [table]`)
- "How do I paginate through large result sets?" -> GET /content.json (use `limit` and `offset` in the SQL)

## Response Tips

- **Successful queries (200):** Response shape depends on `_shape` param -- `objects` returns `[{col: val}, ...]`, `arrays` returns `[[val, ...], ...]`, `array` returns a flat structure. Always check the `columns` field to understand result structure.
- **Bad requests (400):** Typically malformed SQL or disallowed operations. The error message body describes the specific SQL issue -- surface it directly to the user.
- **Server errors (500):** Database-level failures. Retry once, then report. May indicate the database file is locked or corrupted.

## Anomaly Flags

- **SQL injection risk:** If constructing queries from user input, always flag unparameterized string interpolation in SQL values.
- **Empty result sets:** Proactively note when a query returns zero rows -- the table may be empty, the name may be misspelled, or the filter may be too restrictive.
- **500 errors on simple queries:** May indicate the Datasette instance is misconfigured or the underlying SQLite database is unavailable. Surface immediately.
- **Large unbounded queries:** Flag any `select *` without a `LIMIT` clause -- Datasette instances often enforce a max row cap, and results may be silently truncated.
- **Unknown `_shape` values:** If the shape param is not one of the recognized values (`objects`, `arrays`, `array`, `arrayfirst`), the response format may be unexpected.
- **Slow responses:** Queries over 2s may indicate missing indexes or full table scans on large datasets. Suggest adding `LIMIT` or narrowing the `WHERE` clause.

## Playbook

### 1. Explore an Unknown Database

1. Run `sql=select name from sqlite_master where type='table'&_shape=objects` to list all tables.
2. For each table of interest, run `sql=pragma table_info([table])&_shape=objects` to get column names and types.
3. Run `sql=select * from [table] limit 5&_shape=objects` to preview sample data.
4. Run `sql=select count(*) from [table]&_shape=array` to understand data volume.

### 2. Extract and Filter Data

1. Identify the target table and columns using the exploration playbook above.
2. Build a query: `sql=select [cols] from [table] where [condition] order by [col] limit 100&_shape=objects`.
3. If more than 100 rows are needed, paginate with `offset`: increment by 100 each request.
4. Check the row count in each response -- when fewer rows than the limit are returned, you have reached the end.

### 3. Validate Data Quality

1. Run `sql=select count(*) from [table] where [col] is null&_shape=array` to check for null values in key columns.
2. Run `sql=select [col], count(*) from [table] group by [col] order by count(*) desc limit 20&_shape=objects` to inspect value distributions.
3. Run `sql=select count(distinct [col]) from [table]&_shape=array` to check cardinality.
4. Compare counts across related tables to verify referential integrity.

### 4. Health Check and Diagnostics

1. Run `sql=select 1&_shape=array` to confirm connectivity.
2. If it fails with 500, the Datasette instance or database may be down -- report and do not retry further queries.
3. If it succeeds, run `sql=select name from sqlite_master where type='table'&_shape=array` to confirm the database is populated.

### 5. Export a Full Table

1. Get the row count: `sql=select count(*) from [table]&_shape=array`.
2. Fetch in pages of 1000: `sql=select * from [table] limit 1000 offset 0&_shape=objects`.
3. Increment offset by 1000 on each subsequent request.
4. Stop when the response contains fewer than 1000 rows.
5. Concatenate all response arrays into the final dataset.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
