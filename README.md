# Stone, Great Wyrley & Penkridge — Leafletting Map

A canvassing and leafletting tracker for Stone, Great Wyrley and Penkridge. Volunteers can view road-level status, plan routes, and mark progress in real time via a Google Sheets backend.

This repo is a **thin deployment** — it has no local `core.js`/`styles.css` of its own; both load directly from the primary [leaflet-map](https://github.com/Daemeous/leaflet-map) repo (see that repo's README, "Shared assets", for what that means and why).

Live: **https://daemeous.github.io/stone/**

---

## Other live deployments

| Constituency / area | Site |
|---|---|
| Stafford | https://daemeous.github.io/leaflet-map/ |
| Demo | https://daemeous.github.io/leaflet-map-demo/ |
| South Hams | https://daemeous.github.io/south-hams/ |
| Burton & Uttoxeter | https://daemeous.github.io/burton-uttoxeter/ |
| Barnsley, Penistone & Stocksbridge | https://daemeous.github.io/barnsley/ |
| St Helens | https://daemeous.github.io/sthelens/ |

Related project — **[Pothole Watch](https://github.com/Daemeous/stafford-potholes)**, same visual style, separate Sheet/Apps Script backend.

The pipeline that builds this deployment's road/residence data and its Google Sheet + Apps Script backend lives in **[leaflet-pipeline](https://github.com/Daemeous/leaflet-pipeline)**, not in this repo.

---

## How it works

Road data is sourced from OpenStreetMap, clipped to ward boundaries verified against the OS Boundary-Line dataset, and given an estimated residence count per road (OS Open UPRN point-in-buffer matching). Each road is assigned to a ward, given a status (`Not_Started`, `Planned`, `In_Progress`, `Complete`), and stored in a Google Sheet. The app reads that sheet as a published CSV and renders roads as coloured polylines on a Leaflet map.

Authorised users can sign in with Google and update road statuses directly from the map, which writes back to the sheet via a Google Apps Script web app.

---

## Repository contents

| File | Purpose |
|------|---------|
| `index.html` | This deployment's config block (Sheet ID, Apps Script URL, title/subtitle, map centre) — the only thing that differs from any other deployment |
| `sw.js` | Service worker (must stay same-origin, so every deployment keeps its own copy even though `core.js`/`styles.css` are shared) |

`core.js`/`styles.css` are **not** in this repo — see [leaflet-map](https://github.com/Daemeous/leaflet-map)'s README before assuming a bug lives here; most app behaviour comes from that shared file.
