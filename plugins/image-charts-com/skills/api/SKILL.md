---
name: image-charts
description: "Image-Charts API skill. Use when working with Image-Charts for chart, chart.js. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# Image-Charts
API version: 6.1.19

## Auth
No authentication required.

## Base URL
https://image-charts.com/

## Setup
1. No auth setup needed
2. GET /chart -- verify access

## Endpoints

2 endpoints across 2 groups. See references/api-spec.lap for full details.

### chart
| Method | Path | Description |
|--------|------|-------------|
| GET | /chart | Image-Charts API |

### chart.js
| Method | Path | Description |
|--------|------|-------------|
| GET | /chart.js/2.8.0 | Chart.js as image API |

## Enhanced Skill Content
## Question Mapping

- "How do I generate a pie chart?" -> GET /chart
- "How do I create a bar chart with custom colors?" -> GET /chart
- "Can I generate a QR code?" -> GET /chart
- "How do I create a chart using Chart.js configuration?" -> GET /chart.js/2.8.0
- "How do I add a title to my chart?" -> GET /chart
- "How do I set the chart size/dimensions?" -> GET /chart
- "How do I customize axis labels?" -> GET /chart
- "How do I add a legend to the chart?" -> GET /chart
- "Can I get the chart as a PNG or SVG?" -> GET /chart
- "How do I animate a chart as a GIF?" -> GET /chart
- "How do I add grid lines to my chart?" -> GET /chart
- "How do I set a background color on a Chart.js chart?" -> GET /chart.js/2.8.0
- "How do I generate a retina/high-DPI chart?" -> GET /chart
- "How do I sign a chart URL with my account credentials?" -> GET /chart

## Response Tips

- **Chart generation (GET /chart):** Returns binary image data (PNG by default, or SVG/GIF via `chof`). Non-200 responses typically mean invalid parameter combinations -- check `cht` (chart type) and `chl` (labels) are both present. The URL itself is the chart; embed it directly in `<img>` tags.
- **Chart.js rendering (GET /chart.js/2.8.0):** Returns a rendered image from a Chart.js config object passed via `c` or `chart`. Errors usually stem from malformed JSON in the config parameter. Set `encoding=url` if the config contains special characters.

## Anomaly Flags

- **Missing required params:** Requests to `/chart` without both `cht` and `chl` will fail -- surface this before the call is made.
- **Unsigned requests:** If `icac` (account ID) is set but `ichm` (HMAC signature) is missing, the request may be rejected or watermarked -- warn the user.
- **Oversized charts:** Very large `chs` (size) values may hit server limits or degrade performance -- flag dimensions above 999x999.
- **Deprecated Chart.js version:** The endpoint is pinned to Chart.js 2.8.0 -- surface this if the user passes Chart.js v3+ config syntax.
- **GIF animation without `chan`:** If `chof=.gif` is set but `chan` (animation params) is missing, the result is a static GIF -- flag the likely oversight.

## Playbook

### 1. Generate a Simple Pie Chart

1. Set `cht=p` for a pie chart type.
2. Set `chl` to pipe-delimited labels: `chl=Apples|Oranges|Bananas`.
3. Set `chd=t:` with comma-separated data values: `chd=t:30,45,25`.
4. Optionally set `chs=400x300` for dimensions.
5. Call `GET /chart?cht=p&chl=Apples|Oranges|Bananas&chd=t:30,45,25&chs=400x300`.

### 2. Create a Branded Bar Chart with Custom Colors

1. Set `cht=bvg` for a vertical grouped bar chart.
2. Set `chd=t:` with your data series.
3. Set `chl` with bar labels.
4. Set `chco` with pipe-delimited hex colors: `chco=4285F4|EA4335|FBBC05`.
5. Add a title with `chtt=Sales+by+Quarter` and style it with `chts=333333,16`.
6. Add a legend with `chdl=Q1|Q2|Q3`.
7. Call `GET /chart` with all parameters combined.

### 3. Render a Chart.js Configuration as an Image

1. Build a valid Chart.js 2.8.0 config object as JSON.
2. URL-encode the JSON and pass it as the `c` parameter.
3. Set `width=600&height=400` for desired output size.
4. Optionally set `backgroundColor=white` (default is transparent).
5. Call `GET /chart.js/2.8.0?c={encoded_config}&width=600&height=400`.

### 4. Generate a Signed Chart for Production Use

1. Obtain your `icac` (account ID) from Image-Charts.
2. Build the full chart URL with all desired parameters.
3. Compute the HMAC-SHA256 signature of the query string using your secret key.
4. Append `icac=YOUR_ACCOUNT&ichm=COMPUTED_SIGNATURE` to the URL.
5. Optionally add `icretina=1` for high-DPI output.
6. Call the signed `GET /chart` URL.

### 5. Create an Animated GIF Chart

1. Set `cht` to your desired chart type (e.g., `cht=bvg`).
2. Set `chof=.gif` to request GIF output format.
3. Set `chan=1200` for animation duration in milliseconds.
4. Set `chd`, `chl`, and other data/styling parameters as needed.
5. Call `GET /chart` -- the response is an animated GIF suitable for embedding.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
