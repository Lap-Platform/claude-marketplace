---
name: bc-route-planner-rest-api
description: "BC Route Planner REST API skill. Use when working with BC Route Planner REST for distance.{outputFormat}, distance, route.{outputFormat}. Covers 22 endpoints."
version: 1.0.0
generator: lapsh
---

# BC Route Planner REST API
API version: 2.0.0

## Auth
ApiKey apikey in header

## Base URL
https://router.api.gov.bc.ca/

## Setup
1. Set your API key in the appropriate header
2. GET /distance.{outputFormat} -- verify access
3. POST /distance.{outputFormat} -- create first distance.{outputFormat}

## Endpoints

22 endpoints across 7 groups. See references/api-spec.lap for full details.

### distance.{outputFormat}
| Method | Path | Description |
|--------|------|-------------|
| GET | /distance.{outputFormat} | Get distance and travel time between two geographic points |
| POST | /distance.{outputFormat} | Get distance and travel time between two geographic points |

### distance
| Method | Path | Description |
|--------|------|-------------|
| GET | /distance/betweenPairs.{outputFormat} | Get distance and travel time between each pair of geographic points |
| POST | /distance/betweenPairs.{outputFormat} | Get distance and travel time between each pair of geographic points |

### route.{outputFormat}
| Method | Path | Description |
|--------|------|-------------|
| GET | /route.{outputFormat} | Get the path, distance and travel time between a series of geographic points |
| POST | /route.{outputFormat} | Get the path, distance and travel time between a series of geographic points |

### directions.{outputFormat}
| Method | Path | Description |
|--------|------|-------------|
| GET | /directions.{outputFormat} | Get the directions, path, distance and travel time between a series of geographic points |
| POST | /directions.{outputFormat} | Get the directions, path, distance and travel time between a series of geographic points |

### optimalRoute.{outputFormat}
| Method | Path | Description |
|--------|------|-------------|
| GET | /optimalRoute.{outputFormat} | Get the optimal path, distance and travel time between a start point and a series of end points which are reordered to minimize total distance or time. |
| POST | /optimalRoute.{outputFormat} | Get the path, distance and travel time between a start point and a series of end points which are reordered to minimize total distance or time. |

### optimalDirections.{outputFormat}
| Method | Path | Description |
|--------|------|-------------|
| GET | /optimalDirections.{outputFormat} | Get the directions, optimal path, distance and travel time between a start point and a series of end points which are reordered to minimize total distance or time. |
| POST | /optimalDirections.{outputFormat} | Get the directions, optimal path, distance and travel time between a start point and one or more end points which are reordered to minimize total distance or time. |

### truck
| Method | Path | Description |
|--------|------|-------------|
| GET | /truck/distance.{outputFormat} | Get distance and travel time between two geographic points for a commercial vehicle |
| POST | /truck/distance.{outputFormat} | Get distance and travel time between two geographic points |
| GET | /truck/route.{outputFormat} | Get the path, distance and travel time between a series of geographic points for a commercial vehicle |
| POST | /truck/route.{outputFormat} | Get the path, distance and travel time between a series of geographic points |
| GET | /truck/directions.{outputFormat} | Get the directions, path, distance and travel time between a series of geographic points for a commercial vehicle |
| POST | /truck/directions.{outputFormat} | Get the directions, path, distance and travel time between a series of geographic points |
| GET | /truck/optimalRoute.{outputFormat} | Get the optimal path, distance and travel time between a start point and a series of end points which are reordered to minimize total distance or time for a commercial vehicle |
| POST | /truck/optimalRoute.{outputFormat} | Get the path, distance and travel time between a start point and a series of end points which are reordered to minimize total distance or time. |
| GET | /truck/optimalDirections.{outputFormat} | Get the directions, optimal path, distance and travel time between a start point and a series of end points which are reordered to minimize total distance or time for a commercial vehicle |
| POST | /truck/optimalDirections.{outputFormat} | Get the directions, optimal path, distance and travel time between a start point and one or more end points which are reordered to minimize total distance or time. |

## Enhanced Skill Content
## Question Mapping

- "How far is it between two cities in BC?" -> GET /distance.json
- "What is the driving distance for a round trip through multiple stops?" -> GET /distance.json (with roundTrip=True)
- "Find the shortest route between two points in kilometers" -> GET /route.json (with criteria=shortest)
- "Give me turn-by-turn directions from Vancouver to Kamloops" -> GET /directions.json
- "What is the optimal order to visit these five locations?" -> GET /optimalRoute.json
- "Get optimized turn-by-turn directions for a multi-stop delivery route" -> GET /optimalDirections.json
- "Can a truck with height 4.2m travel between these points?" -> GET /truck/route.json (with height=4.2)
- "What is the distance matrix between a set of origins and destinations?" -> GET /distance/betweenPairs.json
- "Find the closest destination from multiple options to my origin" -> GET /distance/betweenPairs.json (with maxPairs=1)
- "Plan a truck route that avoids weight-restricted roads" -> GET /truck/route.json (with weight param, listRestrictions=True)
- "Get simplified directions suitable for display on a small screen" -> GET /directions.json (with simplifyDirections=True)
- "What restrictions apply along a truck route?" -> GET /truck/route.json (with listRestrictions=True)
- "Export a route as KML for Google Earth" -> GET /route.kml
- "Calculate fastest vs shortest route and compare distances" -> GET /distance.json (call twice: criteria=fastest then criteria=shortest)
- "Route a heavy vehicle with specific dimensions through BC" -> GET /truck/directions.json (with height, width, length, weight)

## Response Tips

- **Distance endpoints**: Return numeric distance and travel time; check `distanceUnit` in request to interpret whether values are km or mi.
- **Route endpoints**: Return geometry (coordinate arrays in the requested `outputSRS`); when using KML output, response is XML not JSON.
- **Directions endpoints**: Return ordered instruction segments; `simplifyDirections=True` reduces step count -- compare `notifications` or `warnings` fields for road events.
- **Optimal endpoints**: Return reordered waypoints; compare input vs output point order to determine the optimized sequence.
- **BetweenPairs endpoints**: Return a matrix of origin-destination pairs; `maxPairs` limits results per origin -- default 1 returns only the nearest match.
- **Truck endpoints**: May include restriction information when `listRestrictions=True`; check for `restrictions` array in response for route-specific constraints.
- **All endpoints**: `outputFormat` controls response shape (json/kml/html); errors return descriptive messages -- watch for coordinate parsing failures.

## Anomaly Flags

- **Invalid coordinate format**: Points must be comma-separated `lon,lat` pairs; longitude/latitude reversal is a common mistake in BC (longitude is negative, roughly -114 to -139).
- **SRS mismatch**: If `outputSRS` differs from the coordinate system used in `points`, results will be in an unexpected projection -- flag when non-default SRS is requested.
- **Snap distance failures**: If points are far from any road, routing may fail or produce unexpected detours; surface when `snapDistance` is set unusually high (>2000) or when errors mention snapping.
- **Truck restriction warnings**: Flag when a truck route encounters restrictions that overlap with the vehicle's declared dimensions or weight.
- **Round trip with two points**: `roundTrip=True` with only two waypoints doubles the route -- confirm this is intentional.
- **Optimal route with two points**: Using `/optimalRoute` with only two points provides no optimization benefit -- suggest `/route` instead.
- **Large point sets via GET**: Very long coordinate strings in GET requests may exceed URL length limits -- recommend POST for 10+ waypoints.
- **Deprecated or unusual outputFormat**: Flag if `html` format is requested in an automated pipeline, as it is designed for human viewing.

## Playbook

### 1. Plan a Multi-Stop Delivery Route

1. Collect all delivery addresses and geocode them to `lon,lat` coordinates.
2. Call `GET /optimalRoute.json?points=-123.1,49.2,-122.8,49.1,-123.0,49.3` to find the best visit order.
3. Note the reordered waypoint sequence from the response.
4. Call `GET /optimalDirections.json` with the same points to get turn-by-turn instructions in optimized order.
5. If vehicles are trucks, use `GET /truck/optimalDirections.json` with appropriate `height`, `width`, `length`, and `weight` parameters.
6. Set `simplifyDirections=True` if directions will be displayed on a mobile device.

### 2. Compare Route Options (Fastest vs Shortest)

1. Call `GET /distance.json?points=-123.3,49.2,-120.3,49.9&criteria=fastest` and record distance and time.
2. Call `GET /distance.json?points=-123.3,49.2,-120.3,49.9&criteria=shortest` and record distance and time.
3. Present both options with distance and estimated travel time.
4. Once the user selects a preference, call `GET /directions.json` with the chosen `criteria` for full turn-by-turn navigation.

### 3. Find the Nearest Warehouse from Multiple Customer Locations

1. Format origin points (customers) as `fromPoints` and warehouse locations as `toPoints`.
2. Call `GET /distance/betweenPairs.json?fromPoints=-123.1,49.2,-122.9,49.1&toPoints=-123.0,49.3,-122.7,49.0&maxPairs=1`.
3. Each origin returns its closest destination with distance -- use this to assign customers to warehouses.
4. Increase `maxPairs` to get second-nearest options for load balancing.

### 4. Plan a Truck Route with Dimension Constraints

1. Gather vehicle specs: height (m), width (m), length (m), weight (kg).
2. Call `GET /truck/route.json?points=-123.1,49.2,-121.5,49.8&height=4.2&width=2.6&length=12.5&weight=25000&listRestrictions=True`.
3. Review the `restrictions` in the response for any flagged road segments.
4. If restrictions are problematic, adjust by setting `excludeRestrictions` to bypass specific restriction types, or try an alternate route with intermediate waypoints.
5. Call `GET /truck/directions.json` with the same parameters to get navigation-ready instructions.

### 5. Export a Route for External Use

1. Call `GET /route.kml?points=-123.3,49.2,-120.3,49.9` to get a KML file for Google Earth or GIS tools.
2. For web mapping applications, call `GET /route.json?outputSRS=4326` to get GeoJSON-compatible coordinates in WGS84.
3. For BC provincial mapping systems, set `outputSRS=3005` (BC Albers) to get coordinates in the provincial standard projection.
4. Save the response body directly as `.kml` or parse the JSON geometry into your application's format.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
