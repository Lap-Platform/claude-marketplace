---
name: geomark-web-service-rest-api
description: "Geomark Web Service REST API skill. Use when working with Geomark Web Service REST for geomarks. Covers 7 endpoints."
version: 1.0.0
generator: lapsh
---

# Geomark Web Service REST API
API version: 4.1.2

## Auth
No authentication required.

## Base URL
https://apps.gov.bc.ca/pub/geomark

## Setup
1. No auth setup needed
2. GET /geomarks/{geomarkId}/boundingBox.{fileFormatExtension} -- verify access
3. POST /geomarks/new -- create first new

## Endpoints

7 endpoints across 1 groups. See references/api-spec.lap for full details.

### geomarks
| Method | Path | Description |
|--------|------|-------------|
| POST | /geomarks/new | Create a new geomark |
| POST | /geomarks/copy | Create a new geomark by copying the geometries from one or more existing geomarks from the current server. |
| GET | /geomarks/{geomarkId}/boundingBox.{fileFormatExtension} | Gets the bounding box of the geomark |
| GET | /geomarks/{geomarkId}/feature.{fileFormatExtension} | Get the feature and attribution of the geomark |
| GET | /geomarks/{geomarkId}.{fileFormatExtension} | Get information about a particular geomark |
| GET | /geomarks/{geomarkId}/parts.{fileFormatExtension} | Get the individual geometries within a multi-part geometry |
| GET | /geomarks/{geomarkId}/point.{fileFormatExtension} | Gets a single spatial point representative of the geomark. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new geomark?" -> POST /geomarks/new
- "How do I copy an existing geomark?" -> POST /geomarks/copy
- "Can I copy a geomark with a buffer zone around it?" -> POST /geomarks/copy (use bufferMetres, bufferCap, bufferJoin params)
- "What is the bounding box of my geomark?" -> GET /geomarks/{geomarkId}/boundingBox.{fileFormatExtension}
- "How do I get the full geometry of a geomark?" -> GET /geomarks/{geomarkId}/feature.{fileFormatExtension}
- "How do I retrieve geomark info as GeoJSON?" -> GET /geomarks/{geomarkId}.geojson
- "How do I download a geomark as a shapefile?" -> GET /geomarks/{geomarkId}.shp
- "How do I get the individual parts of a multi-part geomark?" -> GET /geomarks/{geomarkId}/parts.{fileFormatExtension}
- "What is the centroid or representative point of a geomark?" -> GET /geomarks/{geomarkId}/point.{fileFormatExtension}
- "How do I get geomark data in a specific coordinate system like BC Albers?" -> GET /geomarks/{geomarkId}.{ext}?srid=3005
- "How do I export a geomark as KML for Google Earth?" -> GET /geomarks/{geomarkId}.kml
- "Can I merge overlapping geomarks when copying?" -> POST /geomarks/copy (set allowOverlap=true)
- "How do I get geomark metadata in XML format?" -> GET /geomarks/{geomarkId}.xml
- "How do I create a buffered copy of a geomark with flat end caps?" -> POST /geomarks/copy (bufferMetres + bufferCap=FLAT)

## Response Tips

- **Create/Copy (POST):** Watch for 302 redirects -- the API may redirect to the newly created geomark URL rather than returning the resource directly. Check the Location header. A 400 means invalid input geometry or parameters.
- **Geometry retrieval (GET feature/boundingBox/parts/point):** Response content type matches the requested fileFormatExtension. Binary formats (shp, shpz, kmz, gpkg) return as file downloads -- handle as binary streams, not text. JSON and GeoJSON responses contain standard GeoJSON Feature/FeatureCollection objects.
- **Info retrieval (GET geomarkId.ext):** Returns geomark metadata plus geometry. A 404 means the geomarkId does not exist or has expired. No pagination -- each geomark is a single resource.
- **SRID parameter:** Defaults to 4326 (WGS84). BC-specific projections (3005 for BC Albers, 26909/26910 for UTM zones) change coordinate values but not the geometry structure.

## Anomaly Flags

- **302 on POST responses:** The API uses redirects after creation. If a redirectUrl or failureRedirectUrl is set, the redirect target may be external -- surface this to the user before following.
- **404 on any GET:** Geomarks may expire or be deleted. Proactively warn when a previously valid geomarkId starts returning 404.
- **500 errors:** Likely a server-side geometry processing failure (e.g., invalid buffer parameters creating degenerate geometry). Surface the specific parameter combination that triggered it.
- **Large buffer values:** If bufferMetres is very large relative to the geometry, results may be unexpectedly large or slow. Flag when bufferMetres exceeds 10,000.
- **Binary format requests in automated pipelines:** If the caller requests shp/shpz/kmz/gpkg, warn that the response is binary and cannot be parsed as text.
- **SRID mismatch:** If a user requests srid=3005 (BC Albers) for a geometry outside British Columbia, coordinates will be valid but potentially misleading. Flag when mixing non-BC data with BC-specific projections.

## Playbook

### 1. Create a Geomark and Retrieve Its GeoJSON

1. POST /geomarks/new with your geometry payload
2. Capture the geomarkId from the 302 redirect Location header or the 200 response body
3. GET /geomarks/{geomarkId}.geojson to retrieve the stored geometry
4. Validate the returned GeoJSON structure matches your input

### 2. Copy a Geomark with a Buffer Zone

1. Identify the source geomark URL (full URL to an existing geomark)
2. POST /geomarks/copy with geomarkUrl set to the source, bufferMetres set to your desired buffer distance, and bufferCap/bufferJoin for shape control
3. Capture the new geomarkId from the response
4. GET /geomarks/{geomarkId}/feature.geojson to verify the buffered geometry
5. GET /geomarks/{geomarkId}/boundingBox.json to confirm the expanded extent

### 3. Export a Geomark for GIS Software

1. GET /geomarks/{geomarkId}.json to inspect metadata and confirm it is the right geomark
2. Choose the target format: shp for ArcGIS/QGIS desktop, kml for Google Earth, gpkg for modern GIS
3. Choose the target SRID: 4326 for web mapping, 3005 for BC Albers analysis, 26910 for UTM Zone 10
4. GET /geomarks/{geomarkId}/feature.{format}?srid={srid} and save the binary response to a file

### 4. Analyze a Multi-Part Geomark

1. GET /geomarks/{geomarkId}.geojson to see the full geometry and check if it is a MultiPolygon or GeometryCollection
2. GET /geomarks/{geomarkId}/parts.geojson to retrieve each part as a separate feature
3. GET /geomarks/{geomarkId}/point.geojson to get a representative point (centroid) for labeling or geocoding
4. GET /geomarks/{geomarkId}/boundingBox.geojson to understand the full spatial extent

### 5. Create a Geomark with JSONP Callback for Web Integration

1. POST /geomarks/copy with geomarkUrl, resultFormat=json, and callback set to your JavaScript function name
2. The response wraps the JSON in the callback function for cross-domain script injection
3. Set redirectUrl for success navigation and failureRedirectUrl for error handling in browser workflows
4. Parse the geomarkId from the JSONP response in your client-side handler


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
