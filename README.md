# transmission-distribution-equipment-competitive-map

An interactive map of the U.S. competitive landscape for insulated aerial utility truck equipment, overlaid with upcoming transmission and distribution projects.

**Live site:** _(fill in your GitHub Pages URL once published)_

---

## What this is

A single-page HTML map combining two data layers:

1. **Dealers & manufacturer facilities** — 318 unique locations across five major brands (Altec, Terex, Versalift, Palfinger, Dur-A-Lift). Shows who sells, services, rents, or stocks parts for what.
2. **Transmission projects** — 3,664 U.S. transmission and distribution projects from Yes Energy with in-service years between 2027 and 2040. Filterable by voltage class, status, budget, year, and probability.

The map renders entirely client-side. No backend, no API calls at runtime — Leaflet pulls map tiles from OpenStreetMap, and all dealer and project data is baked into the HTML file.

---

## How to use it

Open `index.html` in any modern browser (Chrome, Edge, Firefox, Safari). It also works fine on mobile.

### Filtering

- **Map Layers** at the top toggles the dealer and project layers on/off independently
- **Manufacturer** filters by brand (Altec, Terex, Versalift, Palfinger, Dur-A-Lift)
- **Offers** filters by what a dealer does (Sales, Used Sales, Service, Rentals, Parts)
- **Major Dealers** lets you isolate one or more specific dealer chains (3+ locations). Selecting any dealer here overrides the manufacturer filter
- **Transmission Projects** has its own sub-filters: voltage, status, budget, year, and minimum probability
- **All Dealers** at the bottom is a scrollable list of every dealer. Click a name to expand; click an address to fly to that pin

### Reset

The **Reset filters** button at the top returns everything to default state (all dealer brands on, all offers on, projects layer off) and snaps the map back to the national view.

### Pins

- **Round circles** = dealers / facilities. Pie-wedge circles indicate a single location carrying multiple brands
- **Diamond shapes** = transmission projects, colored by voltage class
- **Lines** = transmission projects with two known endpoints, drawn from county centroid to county centroid

Click any pin or line for a popup with details.

---

## Data sources

| Layer | Source | Notes |
|---|---|---|
| Dealers | Manufacturer dealer locator pages (Altec, Terex, Versalift, Palfinger, Dur-A-Lift) | Pulled manually; deduplicated by name + city + street |
| Transmission projects | Yes Energy / C-Three transmission project database (paid subscription) | Filtered to U.S. projects with in-service year 2027–2040 |

### Geocoding accuracy

- **Dealers:** placed at the zip-code centroid of their listed address. Where multiple dealers share a zip, they're fanned out into a small ring around the centroid so they're individually clickable
- **Projects:** placed at the county centroid (~3,041 projects) or state centroid (~623 projects) of their Endpoint 1 location. Lines drawn between two county centroids when both endpoints are at county-level accuracy or better

Project pins and lines should be read as **directional indicators**, not actual coordinates. The county-centroid level is appropriate for strategic footprint analysis but not for navigation.

---

## ⚠️ Confidential / internal use only

This map contains data from Yes Energy, a paid subscription service. **Do not share this repository or its URL outside the organization.** The repo is private and the GitHub Pages site requires GitHub authentication to view.

If you need to share insights externally, screenshot the relevant view rather than sharing the link, and confirm with Yes Energy's license terms before doing so.

---

## Updating the map

To update the map with new data or fixes:

1. Get a new `index.html` from whoever maintains the project
2. In this repo on GitHub, click **Add file → Upload files**
3. Drag the new `index.html` in. When prompted, choose "Replace existing file"
4. Click **Commit changes**
5. Wait ~60 seconds for GitHub Pages to rebuild. The URL stays the same

To check the build status, click the **Actions** tab — there'll be a workflow called "pages build and deployment."

After deployment, if the page still looks old, hard-refresh your browser (Ctrl+Shift+R on Windows/Linux, Cmd+Shift+R on Mac).

---

## Tech notes

- **Framework:** plain HTML + Leaflet 1.9.4 (loaded from unpkg CDN)
- **Map tiles:** OpenStreetMap (free, no key required)
- **File size:** ~1.4 MB (data inlined). Loads in 1–3 seconds on broadband
- **Dependencies:** none beyond the CDN-loaded Leaflet. Fully self-contained

---

## Roadmap / open questions

Things we've discussed but haven't built yet:

- More granular project coordinates (substation-level rather than county centroid) via HIFLD substation data
- Proximity scoring: for each dealer, "$ of transmission spend within 100 miles"
- Gap finder: project clusters with no nearby dealer of a given brand
- Export filtered results to CSV
