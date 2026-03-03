---
name: transport-for-london-unified-api
description: "Transport for London Unified API skill. Use when working with Transport for London Unified for AccidentStats, AirQuality, BikePoint. Covers 84 endpoints."
version: 1.0.0
generator: lapsh
---

# Transport for London Unified API
API version: v1

## Auth
ApiKey app_key in query | ApiKey app_id in query

## Base URL
https://api.digital.tfl.gov.uk

## Setup
1. Set your API key in the appropriate header
2. GET /AirQuality -- verify access

## Endpoints

84 endpoints across 14 groups. See references/api-spec.lap for full details.

### AccidentStats
| Method | Path | Description |
|--------|------|-------------|
| GET | /AccidentStats/{year} | Gets all accident details for accidents occuring in the specified year |

### AirQuality
| Method | Path | Description |
|--------|------|-------------|
| GET | /AirQuality | Gets air quality data feed |

### BikePoint
| Method | Path | Description |
|--------|------|-------------|
| GET | /BikePoint | Gets all bike point locations. The Place object has an addtionalProperties array which contains the nbBikes, nbDocks and nbSpaces |
| GET | /BikePoint/{id} | Gets the bike point with the given id. |
| GET | /BikePoint/Search | Search for bike stations by their name, a bike point's name often contains information about the name of the street |

### Cabwise
| Method | Path | Description |
|--------|------|-------------|
| GET | /Cabwise/search | Gets taxis and minicabs contact information |

### Journey
| Method | Path | Description |
|--------|------|-------------|
| GET | /Journey/Meta/Modes | Gets a list of all of the available journey planner modes |
| GET | /Journey/JourneyResults/{from}/to/{to} | Perform a Journey Planner search from the parameters specified in simple types |

### Line
| Method | Path | Description |
|--------|------|-------------|
| GET | /Line/Meta/Modes | Gets a list of valid modes |
| GET | /Line/Meta/Severity | Gets a list of valid severity codes |
| GET | /Line/Meta/DisruptionCategories | Gets a list of valid disruption categories |
| GET | /Line/Meta/ServiceTypes | Gets a list of valid ServiceTypes to filter on |
| GET | /Line/{ids} | Gets lines that match the specified line ids. |
| GET | /Line/Mode/{modes} | Gets lines that serve the given modes. |
| GET | /Line/Route | Get all valid routes for all lines, including the name and id of the originating and terminating stops for each route. |
| GET | /Line/{ids}/Route | Get all valid routes for given line ids, including the name and id of the originating and terminating stops for each route. |
| GET | /Line/Mode/{modes}/Route | Gets all lines and their valid routes for given modes, including the name and id of the originating and terminating stops for each route |
| GET | /Line/{id}/Route/Sequence/{direction} | Gets all valid routes for given line id, including the sequence of stops on each route. |
| GET | /Line/{ids}/Status/{StartDate}/to/{EndDate} | Gets the line status for given line ids during the provided dates e.g Minor Delays |
| GET | /Line/{ids}/Status | Gets the line status of for given line ids e.g Minor Delays |
| GET | /Line/Search/{query} | Search for lines or routes matching the query string |
| GET | /Line/Status/{severity} | Gets the line status for all lines with a given severity |
| GET | /Line/Mode/{modes}/Status | Gets the line status of for all lines for the given modes |
| GET | /Line/{id}/StopPoints | Gets a list of the stations that serve the given line id |
| GET | /Line/{id}/Timetable/{fromStopPointId} | Gets the timetable for a specified station on the give line |
| GET | /Line/{id}/Timetable/{fromStopPointId}/to/{toStopPointId} | Gets the timetable for a specified station on the give line with specified destination |
| GET | /Line/{ids}/Disruption | Get disruptions for the given line ids |
| GET | /Line/Mode/{modes}/Disruption | Get disruptions for all lines of the given modes. |
| GET | /Line/{ids}/Arrivals/{stopPointId} | Get the list of arrival predictions for given line ids based at the given stop |

### Mode
| Method | Path | Description |
|--------|------|-------------|
| GET | /Mode/ActiveServiceTypes | Returns the service type active for a mode. |
| GET | /Mode/{mode}/Arrivals | Gets the next arrival predictions for all stops of a given mode |

### Occupancy
| Method | Path | Description |
|--------|------|-------------|
| GET | /Occupancy/CarPark/{id} | Gets the occupancy for a car park with a given id |
| GET | /Occupancy/CarPark | Gets the occupancy for all car parks that have occupancy data |
| GET | /Occupancy/ChargeConnector/{ids} | Gets the occupancy for a charge connectors with a given id (sourceSystemPlaceId) |
| GET | /Occupancy/ChargeConnector | Gets the occupancy for all charge connectors |
| GET | /Occupancy/BikePoints/{ids} | Get the occupancy for bike points. |

### Place
| Method | Path | Description |
|--------|------|-------------|
| GET | /Place/Meta/Categories | Gets a list of all of the available place property categories and keys. |
| GET | /Place/Meta/PlaceTypes | Gets a list of the available types of Place. |
| GET | /Place/Address/Streets/{Postcode} | Gets the set of streets associated with a post code. |
| GET | /Place/Type/{types} | Gets all places of a given type |
| GET | /Place/{id} | Gets the place with the given id. |
| GET | /Place | Gets the places that lie within a geographic region. The geographic region of interest can either be specified |
| GET | /Place/{type}/At/{Lat}/{Lon} | Gets any places of the given type whose geography intersects the given latitude and longitude. In practice this means the Place |
| GET | /Place/{type}/overlay/{z}/{Lat}/{Lon}/{width}/{height} | Gets the place overlay for a given set of co-ordinates and a given width/height. |
| GET | /Place/Search | Gets all places that matches the given query |

### Road
| Method | Path | Description |
|--------|------|-------------|
| GET | /Road | Gets all roads managed by TfL |
| GET | /Road/{ids} | Gets the road with the specified id (e.g. A1) |
| GET | /Road/{ids}/Status | Gets the specified roads with the status aggregated over the date range specified, or now until the end of today if no dates are passed. |
| GET | /Road/{ids}/Disruption | Get active disruptions, filtered by road ids |
| GET | /Road/all/Street/Disruption | Gets a list of disrupted streets. If no date filters are provided, current disruptions are returned. |
| GET | /Road/all/Disruption/{disruptionIds} | Gets a list of active disruptions filtered by disruption Ids. |
| GET | /Road/Meta/Categories | Gets a list of valid RoadDisruption categories |
| GET | /Road/Meta/Severities | Gets a list of valid RoadDisruption severity codes |

### Search
| Method | Path | Description |
|--------|------|-------------|
| GET | /Search | Search the site for occurrences of the query string. The maximum number of results returned is equal to the maximum page size |
| GET | /Search/BusSchedules | Searches the bus schedules folder on S3 for a given bus number. |
| GET | /Search/Meta/SearchProviders | Gets the available searchProvider names. |
| GET | /Search/Meta/Categories | Gets the available search categories. |
| GET | /Search/Meta/Sorts | Gets the available sorting options. |

### StopPoint
| Method | Path | Description |
|--------|------|-------------|
| GET | /StopPoint/Meta/Categories | Gets the list of available StopPoint additional information categories |
| GET | /StopPoint/Meta/StopTypes | Gets the list of available StopPoint types |
| GET | /StopPoint/Meta/Modes | Gets the list of available StopPoint modes |
| GET | /StopPoint/{ids} | Gets a list of StopPoints corresponding to the given list of stop ids. |
| GET | /StopPoint/{id}/placeTypes | Get a list of places corresponding to a given id and place types. |
| GET | /StopPoint/{id}/Crowding/{line} | Gets all the Crowding data (static) for the StopPointId, plus crowding data for a given line and optionally a particular direction. |
| GET | /StopPoint/Type/{types} | Gets all stop points of a given type |
| GET | /StopPoint/Type/{types}/page/{page} | Gets all the stop points of given type(s) with a page number |
| GET | /StopPoint/ServiceTypes | Gets the service types for a given stoppoint |
| GET | /StopPoint/{id}/Arrivals | Gets the list of arrival predictions for the given stop point id |
| GET | /StopPoint/{id}/ArrivalDepartures | Gets the list of arrival and departure predictions for the given stop point id (overground, Elizabeth line and thameslink only) |
| GET | /StopPoint/{id}/CanReachOnLine/{lineId} | Gets Stopoints that are reachable from a station/line combination. |
| GET | /StopPoint/{id}/Route | Returns the route sections for all the lines that service the given stop point ids |
| GET | /StopPoint/Mode/{modes}/Disruption | Gets a distinct list of disrupted stop points for the given modes |
| GET | /StopPoint/{ids}/Disruption | Gets all disruptions for the specified StopPointId, plus disruptions for any child Naptan records it may have. |
| GET | /StopPoint/{id}/DirectionTo/{toStopPointId} | Returns the canonical direction, "inbound" or "outbound", for a given pair of stop point Ids in the direction from -&gt; to. |
| GET | /StopPoint | Gets a list of StopPoints within {radius} by the specified criteria |
| GET | /StopPoint/Mode/{modes} | Gets a list of StopPoints filtered by the modes available at that StopPoint. |
| GET | /StopPoint/Search/{query} | Search StopPoints by their common name, or their 5-digit Countdown Bus Stop Code. |
| GET | /StopPoint/Search | Search StopPoints by their common name, or their 5-digit Countdown Bus Stop Code. |
| GET | /StopPoint/Sms/{id} | Gets a StopPoint for a given sms code. |
| GET | /StopPoint/{stopPointId}/TaxiRanks | Gets a list of taxi ranks corresponding to the given stop point id. |
| GET | /StopPoint/{stopPointId}/CarParks | Get car parks corresponding to the given stop point id. |

### TravelTimes
| Method | Path | Description |
|--------|------|-------------|
| GET | /TravelTimes/overlay/{z}/mapcenter/{mapCenterLat}/{mapCenterLon}/pinlocation/{pinLat}/{pinLon}/dimensions/{width}/{height} | Gets the TravelTime overlay. |
| GET | /TravelTimes/compareOverlay/{z}/mapcenter/{mapCenterLat}/{mapCenterLon}/pinlocation/{pinLat}/{pinLon}/dimensions/{width}/{height} | Gets the TravelTime overlay. |

### Vehicle
| Method | Path | Description |
|--------|------|-------------|
| GET | /Vehicle/{ids}/Arrivals | Gets the predictions for a given list of vehicle Id's. |

## Enhanced Skill Content
## Question Mapping

- "What accidents happened in London in 2023?" -> GET /AccidentStats/{year}
- "What is the current air quality in London?" -> GET /AirQuality
- "Where are the nearest bike docking stations?" -> GET /BikePoint/Search
- "How many bikes are available at this docking station?" -> GET /Occupancy/BikePoints/{ids}
- "How do I get from King's Cross to Heathrow?" -> GET /Journey/JourneyResults/{from}/to/{to}
- "Is the Northern line running normally?" -> GET /Line/{ids}/Status
- "What disruptions are on the District line right now?" -> GET /Line/{ids}/Disruption
- "When is the next train arriving at Paddington?" -> GET /StopPoint/{id}/Arrivals
- "What are the stop points on the Jubilee line?" -> GET /Line/{id}/StopPoints
- "Find a licensed cab near Covent Garden." -> GET /Cabwise/search
- "Are there any road disruptions on the A40?" -> GET /Road/{ids}/Disruption
- "What types of transport modes are available?" -> GET /Line/Meta/Modes
- "Show me the timetable from Baker Street to Wembley Park on the Metropolitan line." -> GET /Line/{id}/Timetable/{fromStopPointId}/to/{toStopPointId}
- "Which car parks have spaces available right now?" -> GET /Occupancy/CarPark
- "What street disruptions are planned for next week?" -> GET /Road/all/Street/Disruption

## Response Tips

- **AccidentStats / AirQuality**: Returns flat arrays or single objects; no pagination. Air quality includes `forecastBand` and `forecastSummary` -- parse these for human-readable output.
- **BikePoint / Occupancy**: BikePoint responses contain `additionalProperties` arrays with key-value pairs for dock count, bikes available, and empty docks -- iterate these rather than expecting top-level fields.
- **Journey**: Results nest deeply: `journeys[] -> legs[] -> instruction/disruptions`. Always check `journeys` array length; zero results means no viable route. The `duration` is in minutes.
- **Line Status / Disruption**: Status responses include `lineStatuses[]` with `statusSeverity` (10 = Good Service). Disruption objects include `categoryDescription` and `closureText` which may contain HTML markup if `applyHtmlMarkup` was set.
- **StopPoint**: Paginated via `/Type/{types}/page/{page}` -- pages are 1-indexed. Single stop lookups return nested `children` and `lineModeGroups`. Search results wrap matches in a `matches[]` array.
- **Road**: Road status includes `statusSeverity` and `statusSeverityDescription`. Disruption responses may be large; use `stripContent=true` to reduce payload size.
- **Cabwise**: Returns XML by default unless `legacyFormat=false`. Set `forceXml=false` for JSON. Results are capped by `maxResults` (default varies).
- **Search**: General search returns `searchMatches[]` with mixed types (stops, lines, places) -- filter by the `type` field on each match.

## Anomaly Flags

- **Rate limiting**: TfL enforces per-key rate limits. Surface HTTP 429 responses immediately and recommend backing off or registering for a higher-tier app_key.
- **Stale data**: If `$modified` or timestamp fields on arrivals/predictions are more than 5 minutes old, flag that real-time data may be delayed or the feed may be down.
- **Empty arrivals**: If `/StopPoint/{id}/Arrivals` returns an empty array during operating hours, proactively note that the station may be closed, suspended, or the line may have no service.
- **Severity 0 or unusual codes**: Line status severity below 1 or unrecognized severity values should be flagged -- they may indicate API changes or data quality issues.
- **Disruption volume**: If a line or mode disruption query returns more than 5 active disruptions, summarize and highlight this as an abnormally high disruption count.
- **Missing auth keys**: If responses return 401 or 403 errors, remind the user to include `app_key` and optionally `app_id` as query parameters. Unauthenticated requests have severely reduced rate limits.
- **HTML in responses**: Some endpoints inject HTML markup into text fields (especially journey instructions). Flag when raw HTML appears so the user can strip or render it appropriately.

## Playbook

### 1. Plan a Journey with Accessibility Needs

1. Call `GET /Journey/Meta/Modes` to list available travel modes and confirm accessibility options.
2. Call `GET /Journey/JourneyResults/{from}/to/{to}` with `accessibilityPreference=NoSolidStairs,NoEscalators` and desired `mode` filters.
3. Review the `journeys[]` array. For each journey, inspect `legs[].disruptions` for active issues.
4. If no results, retry with relaxed preferences (remove mode filters or accessibility constraints) and compare options.
5. Present the top 2-3 journeys with duration, number of changes, and any disruption warnings.

### 2. Monitor Line Status and Surface Disruptions

1. Call `GET /Line/Mode/{modes}/Status` (e.g., modes=`tube,dlr,overground`) to get current status for all lines in those modes.
2. Filter results where `lineStatuses[0].statusSeverity` is not 10 (Good Service).
3. For any disrupted lines, call `GET /Line/{ids}/Disruption` to get detailed disruption descriptions.
4. Optionally call `GET /StopPoint/Mode/{modes}/Disruption` to identify which specific stations are affected.
5. Summarize: list affected lines, severity, affected stations, and expected resolution if provided.

### 3. Find and Check Bike Availability

1. Call `GET /BikePoint/Search?query={location}` to find docking stations near a landmark or area name.
2. From results, extract the `id` values (e.g., `BikePoints_123`).
3. Call `GET /Occupancy/BikePoints/{ids}` with a comma-separated list of station IDs.
4. Parse each station's occupancy: `bikesCount` for available bikes, `emptyDocks` for return spaces.
5. Recommend the nearest station with both available bikes and empty docks (for return trips).

### 4. Investigate Road Conditions Before Driving

1. Call `GET /Road` to list all managed road corridors and their current `statusSeverity`.
2. For roads with poor status, call `GET /Road/{ids}/Disruption` to get disruption details.
3. To check a specific date range (e.g., planned works), call `GET /Road/all/Street/Disruption?startDate={date}&endDate={date}`.
4. Use `GET /Road/Meta/Severities` to decode severity codes into human-readable labels.
5. Present a summary: road name, severity, disruption category, and whether closures are in effect.

### 5. Look Up Stop Information and Live Arrivals

1. Call `GET /StopPoint/Search/{query}` to find a station by name (e.g., "Victoria").
2. From the results, pick the correct stop using `name` and `modes` fields to disambiguate (e.g., tube vs. bus).
3. Call `GET /StopPoint/{id}/Arrivals` to get real-time arrival predictions.
4. Sort arrivals by `timeToStation` (seconds) and group by `lineName` and `platformName`.
5. If the user needs onward travel, call `GET /StopPoint/{id}/Route` to see which lines and directions serve that stop.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
