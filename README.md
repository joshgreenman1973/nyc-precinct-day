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

A single day is a snapshot, not a precinct's typical pattern.

## Files

- `index.html` — the live explorer (self-contained; loads Leaflet + the Socrata API).
- `snapshot-75th-2025-12-17.html` — a static single-day snapshot (75th Precinct, Dec 17, 2025) using `data.js`.
- `data.js` — the baked data for the static snapshot.

Map tiles © OpenStreetMap contributors © CARTO.
