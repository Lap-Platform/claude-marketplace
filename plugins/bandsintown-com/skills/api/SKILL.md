---
name: bandsintown-api
description: "Bandsintown API skill. Use when working with Bandsintown for artists. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# Bandsintown API
API version: 3.0.0

## Auth
No authentication required.

## Base URL
https://rest.bandsintown.com

## Setup
1. No auth setup needed
2. GET /artists/{artistname}/events -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### artists
| Method | Path | Description |
|--------|------|-------------|
| GET | /artists/{artistname} | Get artist information |
| GET | /artists/{artistname}/events | Get upcoming, past, or all artist events, or events within a date range |

## Enhanced Skill Content
## Question Mapping

- "Who is this artist?" -> GET /artists/{artistname}
- "Get me info about Radiohead" -> GET /artists/{artistname}
- "Does this band exist on Bandsintown?" -> GET /artists/{artistname}
- "What upcoming shows does this artist have?" -> GET /artists/{artistname}/events
- "When is the next concert for Beyonce?" -> GET /artists/{artistname}/events
- "Show me past events for this band" -> GET /artists/{artistname}/events
- "What events are happening on a specific date?" -> GET /artists/{artistname}/events
- "Find concerts between two dates" -> GET /artists/{artistname}/events
- "Is this artist currently touring?" -> GET /artists/{artistname}/events
- "Get the artist image and social links" -> GET /artists/{artistname}
- "How many upcoming events does this artist have?" -> GET /artists/{artistname}/events
- "Are there any shows near me for this artist?" -> GET /artists/{artistname}/events
- "What did the artist's recent tour look like?" -> GET /artists/{artistname}/events

## Response Tips

- **Artist lookup**: Response is a single object with name, image URL, tracker count, and social links. A missing or unknown artist may return an empty object or error -- check that the `name` field is present before proceeding.
- **Events**: Response is an array of event objects. An empty array means no matching events, not an error. Each event contains venue details as a nested object (name, city, country, latitude, longitude). The `date` parameter accepts formats like `upcoming`, `past`, `all`, or a range like `2025-01-01,2025-12-31`.

## Anomaly Flags

- **Empty artist response**: If the artist lookup returns no `name` field, surface that the artist was not found -- suggest checking spelling or trying URL-encoded variants.
- **Zero events returned**: Proactively note whether the query used a date filter that may be too narrow, and suggest broadening the range or using `upcoming`.
- **app_id missing or invalid**: Both endpoints require `app_id` -- if requests fail, flag that this parameter must be set and is not a secret key but an app identifier.
- **Artist name encoding**: Names with spaces, ampersands, or special characters need URL encoding. Flag if a request fails and the name contains unencoded special characters.
- **Rate limiting**: If consecutive requests start returning 429 or slow responses, surface this and recommend adding delays between batch lookups.
- **Stale data**: Event dates in the past appearing in "upcoming" results may indicate API-side caching lag -- flag events with dates before today.

## Playbook

### 1. Look Up an Artist and Their Upcoming Shows

1. Call `GET /artists/{artistname}?app_id={id}` to confirm the artist exists
2. Check that the response contains a valid `name` field
3. Call `GET /artists/{artistname}/events?app_id={id}&date=upcoming` to get future shows
4. Present the event list with venue name, city, country, and date

### 2. Find Events in a Date Range

1. Determine the desired start and end dates (format: `YYYY-MM-DD`)
2. Call `GET /artists/{artistname}/events?app_id={id}&date={start},{end}`
3. Filter or sort results client-side by date if needed
4. If the array is empty, suggest widening the date range

### 3. Check if an Artist is Currently Touring

1. Call `GET /artists/{artistname}?app_id={id}` to verify the artist exists
2. Call `GET /artists/{artistname}/events?app_id={id}&date=upcoming`
3. If the events array is non-empty, the artist is touring -- report the next show date and venue
4. If empty, report that no upcoming tour dates are listed

### 4. Batch Lookup for Multiple Artists

1. Prepare a list of artist names, URL-encoding each
2. For each artist, call `GET /artists/{artistname}?app_id={id}` to validate
3. For valid artists, call `GET /artists/{artistname}/events?app_id={id}&date=upcoming`
4. Aggregate results and present a combined schedule
5. Add a short delay between requests to avoid rate limiting

### 5. Get an Artist's Full Event History

1. Call `GET /artists/{artistname}/events?app_id={id}&date=all` to retrieve past and future events
2. Separate results into past and upcoming based on the event date relative to today
3. Summarize: total events, most frequent cities, date of first and last known show


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
