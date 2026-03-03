---
name: geocoder-rest-api
description: "Geocoder REST API skill. Use when working with Geocoder REST for addresses.{outputFormat}, occupants, sites. Covers 16 endpoints."
version: 1.0.0
generator: lapsh
---

# Geocoder REST API
API version: 2.0.0

## Auth
ApiKey apikey in header

## Base URL
https://geocoder.api.gov.bc.ca/

## Setup
1. Set your API key in the appropriate header
2. GET /addresses.{outputFormat} -- verify access

## Endpoints

16 endpoints across 5 groups. See references/api-spec.lap for full details.

### addresses.{outputFormat}
| Method | Path | Description |
|--------|------|-------------|
| GET | /addresses.{outputFormat} | Geocode an address |

### occupants
| Method | Path | Description |
|--------|------|-------------|
| GET | /occupants/addresses.{outputFormat} | Geocode an address and identify site occupants |
| GET | /occupants/nearest.{outputFormat} | Find occupants of the site nearest to a geographic point |
| GET | /occupants/near.{outputFormat} | Find occupants of sites near to a geographic point |
| GET | /occupants/within.{outputFormat} | Find occupants of sites in a geographic area |
| GET | /occupants/{occupantID}.{outputFormat} | Get an occupant (of a site) by its unique ID |

### sites
| Method | Path | Description |
|--------|------|-------------|
| GET | /sites/nearest.{outputFormat} | Find the site nearest to a geographic point |
| GET | /sites/near.{outputFormat} | Find sites near to a geographic point |
| GET | /sites/within.{outputFormat} | Find sites in a geographic area |
| GET | /sites/{siteID}/subsites.{outputFormat} | Represents all subsites of a given site |
| GET | /sites/{siteID}.{outputFormat} | Get a site by its unique ID |

### intersections
| Method | Path | Description |
|--------|------|-------------|
| GET | /intersections/nearest.{outputFormat} | Find nearest intersection to a geographic point |
| GET | /intersections/near.{outputFormat} | Find intersections near to a geographic point |
| GET | /intersections/within.{outputFormat} | Find intersections in a geographic area |
| GET | /intersections/{intersectionID}.{outputFormat} | Get an intersection by its unique ID |

### parcels
| Method | Path | Description |
|--------|------|-------------|
| GET | /parcels/pids/{siteID}.{outputFormat} | Get a comma-separated string of all pids for a given site |

## Enhanced Skill Content
## Question Mapping

- "What is the address for 525 Superior Street in Victoria?" -> GET /addresses.{outputFormat}
- "Find the nearest site to a GPS coordinate?" -> GET /sites/nearest.{outputFormat}
- "What occupants are at a given address?" -> GET /occupants/addresses.{outputFormat}
- "What intersections are near a specific point?" -> GET /intersections/near.{outputFormat}
- "Find all sites within a bounding box area?" -> GET /sites/within.{outputFormat}
- "What are the subsites of a known site ID?" -> GET /sites/{siteID}/subsites.{outputFormat}
- "Look up a specific site by its ID?" -> GET /sites/{siteID}.{outputFormat}
- "What parcel IDs (PIDs) belong to a site?" -> GET /parcels/pids/{siteID}.{outputFormat}
- "Find businesses or occupants near a location filtered by tag?" -> GET /occupants/near.{outputFormat}
- "Get the closest intersection to my coordinates?" -> GET /intersections/nearest.{outputFormat}
- "Autocomplete a partial address string?" -> GET /addresses.{outputFormat} (with autoComplete=true)
- "Find all occupants within a geographic bounding box matching specific tags?" -> GET /occupants/within.{outputFormat}
- "Get intersection details by intersection ID?" -> GET /intersections/{intersectionID}.{outputFormat}
- "Look up an occupant by their ID?" -> GET /occupants/{occupantID}.{outputFormat}
- "Geocode an address and get the result in a specific coordinate system?" -> GET /addresses.{outputFormat} (with outputSRS parameter)

## Response Tips

- **addresses**: Results are scored by match quality; check `score` field and `matchPrecision` to gauge confidence. Low scores with `fuzzyMatch=true` may return false positives.
- **sites (nearest/near/within)**: Returns location geometry; the `locationDescriptor` in the response indicates which point type (access, rooftop, parcel) was used. `brief=true` strips most fields for lightweight responses.
- **occupants**: Responses nest occupant info inside site/address data; filter by `tags` to narrow results. The `tagCondition` (or/and) changes whether tags are inclusive or exclusive.
- **intersections**: Degree indicates how many roads meet; filter with `minDegree`/`maxDegree` to exclude simple bends (degree 2) or isolate complex junctions.
- **parcels**: Returns PID strings only, not geometries. Use the PID with BC land title systems for ownership data.
- **All endpoints**: Set `outputFormat` in the URL path (json, geojson, csv, kml, gml, shpz, xhtml). Default is json. The `echo=true` parameter mirrors input parameters back in the response for debugging.

## Anomaly Flags

- **Low match scores**: Surface a warning when address geocoding returns results with scores below 50 -- the match is likely unreliable.
- **Empty result sets**: Flag when spatial queries (near/within) return zero results, suggesting the point or bbox may be outside BC or the maxDistance is too small.
- **SRS mismatch**: Alert if the requested `outputSRS` differs from the input coordinate system, as coordinates may be misinterpreted without proper reprojection.
- **maxResults cap**: Warn when results returned equals `maxResults`, as additional matches may exist beyond the limit.
- **Interpolation artifacts**: When `interpolation=adaptive` or `linear` is used, flag that returned coordinates are estimated positions, not surveyed points.
- **autoComplete with exactSpelling**: Surface a conflict warning if both `autoComplete=true` and `exactSpelling=true` are set, as these work against each other.
- **API key missing or invalid**: Proactively note that all requests require an `apikey` header; a 401/403 likely means the key is missing or expired.

## Playbook

### 1. Geocode a Street Address and Retrieve Its Parcel ID

1. Call `GET /addresses.json?addressString=525+Superior+St,+Victoria,+BC&maxResults=1`
2. Extract the `siteID` from the top-scoring result
3. Call `GET /parcels/pids/{siteID}.json` to get associated parcel identifiers
4. Use the returned PIDs for land title or property assessment lookups

### 2. Find Nearby Businesses by Category

1. Determine your point of interest as `lng,lat` (e.g., `-123.3656,48.4284`)
2. Call `GET /occupants/near.json?point=-123.3656,48.4284&maxDistance=500&tags=restaurant&maxResults=10`
3. Review results; adjust `maxDistance` if too few or too many matches
4. For each occupant of interest, call `GET /occupants/{occupantID}.json` for full details

### 3. Bulk Spatial Query Within a Bounding Box

1. Define a bounding box as `minLng,minLat,maxLng,maxLat` (e.g., `-123.40,48.40,-123.30,48.45`)
2. Call `GET /sites/within.json?bbox=-123.40,48.40,-123.30,48.45&maxResults=200&brief=true`
3. If result count equals `maxResults`, subdivide the bbox and repeat to ensure full coverage
4. Optionally switch `outputFormat` to `csv` or `geojson` for GIS ingestion

### 4. Reverse Geocode GPS Coordinates to a Street Address

1. Format coordinates as `lng,lat` (note: longitude first)
2. Call `GET /sites/nearest.json?point=-123.3656,48.4284&maxDistance=100`
3. If no result, increase `maxDistance` incrementally (200, 500, 1000)
4. Use the returned site's `fullAddress` as the human-readable location
5. Optionally call `GET /sites/{siteID}/subsites.json` if the site contains units

### 5. Address Autocomplete for a Search Field

1. As the user types, call `GET /addresses.json?addressString={partial}&autoComplete=true&maxResults=5&brief=true&minScore=50`
2. Display returned `fullAddress` values as suggestions
3. On user selection, call `GET /addresses.json?addressString={selectedAddress}&maxResults=1` with full detail (`brief=false`)
4. Extract coordinates and siteID from the final result for downstream use


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
