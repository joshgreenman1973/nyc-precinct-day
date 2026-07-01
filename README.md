# A day on the police radio — NYC precinct explorer

Pick any of New York City's 77 police precincts and any day in 2025, and this tool pulls
every 911 call and radio run the NYPD dispatched there that day — straight from the city's
own records — and rebuilds an interactive map, a 24-hour timeline, a call-type breakdown and
a response-time analysis, live in the browser.

**Live:** https://joshgreenman1973.github.io/nyc-precinct-day/

## Data

- **Source:** [NYPD Calls for Service (Year-to-Date)](https://data.cityofnewyork.us/Public-Safety/NYPD-Calls-for-Service-Year-to-Date-/n2zq-pubd), NYC Open Data, dataset `n2zq-pubd` — the police department's own computer-aided dispatch (CAD) log.
- **Coverage:** January 1 – December 31, 2025.
- Queried live in the browser via the Socrata API for the precinct and date you choose. Nothing is cached or pre-baked.

## 311 overlay

A three-way **Layers** control — **911 calls** (default) / **Both** / **311 only** — shows a
same-day **311 (non-emergency) layer** alongside or instead of the police calls. Both layers
follow the same time controls (hour filter + Live-flow scrubber). 311 requests
([dataset `erm2-nwe9`](https://data.cityofnewyork.us/Social-Services/311-Service-Requests-from-2020-to-Present/erm2-nwe9))
carry no precinct field, so they are clipped to the precinct's official boundary
([`y76i-bdw7`](https://data.cityofnewyork.us/City-Government/Police-Precincts/y76i-bdw7)) by
point-in-polygon. 911 and 311 are separate systems and are **not linked at the record level** —
this is a same-day, same-place comparison, not a matched one. (311 is near-real-time in the source
data, but is shown for the picked 2025 date to stay aligned with the six-month-lagged 911 feed.)

## Method & limits

- **Response time** = job-created to first-unit-arrived, reported only for **dispatched calls**
  (a unit travelled to the scene, arrival logged more than 12 seconds after creation).
- **Officer-initiated and already-on-scene runs** — visibility patrol, inspections, ShotSpotter,
  on-view enforcement — log arrival instantly and carry no real travel time. They are set aside
  from the response medians (the NYPD's own response-time reporting does the same) but remain in
  every count and on the map. The on-view share is disclosed on the page.
- **Medians, not means** — a long tail of low-priority jobs left in queue skews the averages.
- **No outcomes** — this dataset records each job's type, times, location and priority, but carries
  no arrest or disposition, and there is no key to link it to the separate NYPD arrests data.
- **Jobs, not incidents** — one incident can generate several jobs. "Families" are this tool's
  grouping of the raw call descriptions.
- **Source filter (officer-initiated vs. 911 / dispatched)** is an inference — the dataset has no
  field naming who started a job. "Officer-initiated" = proactive patrol/inspections/sweeps, or a
  unit already on scene with no travel; "911 / dispatched" = a complaint a unit was sent to and
  drove to. Labeled as inferred on the page.

A single day is a snapshot, not a precinct's typical pattern.

## Files

- `index.html` — the live explorer (self-contained; loads Leaflet + the Socrata API).
- `snapshot-75th-2025-12-17.html` — a static single-day snapshot (75th Precinct, Dec 17, 2025) using `data.js`.
- `data.js` — the baked data for the static snapshot.

Map tiles © OpenStreetMap contributors © CARTO.
