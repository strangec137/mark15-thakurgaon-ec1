---
title: "EC1 — Thakurgaon Location Context Map"
project: "Mark 15 (Mark 15X)"
author: "GIS Researcher, Bangladesh"
study_area: "Thakurgaon District, Bangladesh"
output: "EC1_Thakurgaon_Location_Context.png"
crs: "EPSG:4326"
last_updated: "2026-09-14"
---

# EC1 — Thakurgaon Location Context Map

Part of the **Mark 15** open-source geospatial mapping portfolio.

This notebook produces a 3-panel location context map showing:

- **(a)** Bangladesh, with Thakurgaon District highlighted
- **(b)** Thakurgaon District, with all upazilas outlined and Thakurgaon Sadar highlighted
- **(c)** Thakurgaon Sadar upazila on its own, zoomed in

---

## ⚠️ Before You Run This Notebook

**Prepare your shapefiles or geopackages first.**

This notebook does not create or clean boundary data — it expects the geopackages listed below to already exist, in the CRS/format described, before you run any cell. If you're reproducing this for a different study area, prepare your own equivalent files first (e.g. in QGIS) and update the file paths in Cell 1 accordingly.

---

## Required Input Files

| Path | Layer(s) | Notes |
|---|---|---|
| `data/boundaries/Bangladesh_Country_Boundary.gpkg` | default layer | District-level polygons (`NAME_2`) covering all of Bangladesh |
| `data/boundaries/thakurgaon_district.gpkg` | `thakurgaon_district`, `thakurgaon_upazilas` | District outline + all 5 upazilas (`NAME_3`) |
| `data/boundaries/thakurgaon_sadar.gpkg` | `thakurgaon_district__thakurgaon_sadar` | Standalone Thakurgaon Sadar upazila polygon |
| `assets/north_arrow.png` | — | North arrow image used in all 3 panels |

All layers should be in, or convertible to, **EPSG:4326**. Source: GADM administrative boundaries (or equivalent), dissolved/clipped in QGIS.

> **Note for GitHub users:** paths above use relative folder names (`data/`, `assets/`) for portability. If you clone this repo, either recreate this folder structure locally, or edit the path variables at the top of Cell 1 to match your own layout.

---

## Reproducing This Map

### 1. Clone the repository
```bash
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>
```

### 2. Set up the environment
```bash
conda create -n mark15 python=3.11
conda activate mark15
pip install -r requirements.txt
```

### 3. Add the input data
Place your boundary geopackages and north arrow image in the folder structure shown above (`data/boundaries/`, `assets/`). Sample/reduced versions of the boundary files can be included directly in the repo since they're small (see file sizes below); large raster datasets used elsewhere in Mark 15 are excluded via `.gitignore` and documented separately per notebook.

| File | Approx. size |
|---|---|
| `Bangladesh_Country_Boundary.gpkg` | ~1–5 MB (district-level) |
| `thakurgaon_district.gpkg` | ~1 MB |
| `thakurgaon_sadar.gpkg` | <1 MB |

### 4. Launch Jupyter and run the notebook
```bash
jupyter notebook
```
Open `EC1_Thakurgaon_Location_Context.ipynb` and run all 3 cells in order.

### 5. Output
The final map is saved as:
```
outputs/EC1_Thakurgaon_Location_Context.png
```
at 300 DPI.

---

## Notebook Structure

| Cell | Purpose |
|---|---|
| 1 | Imports, file paths, and loading all geopackages |
| 2 | Style setup (fonts, legend styling) and helper functions (basemap, axis styling, north arrow, scale bar, zoom connector lines) |
| 3 | Builds the 3-panel figure, draws all layers, adds annotations, saves the final PNG |

---

## Known Limitations

- **Scale bar distances are approximate**, not calculated from true geodesic distance — the `(0, 100)`, `(0, 10, 20)`, and `(0, 1, 2)` km values are visual estimates per panel and will need adjustment if reused for a different extent. A geodesic-based scale bar calculation is planned for a future revision.
- **Basemap tiles require an internet connection** at render time (Esri World Street Map by default — no API key required, unlike some Carto tile styles).
- The north arrow image must exist at the configured path, or that panel's compass is silently skipped with a printed warning (does not stop the script).

---

## Style Reference

This notebook targets the **academic/journal map style** used across the Mark 15 project: light background, classified/highlighted zones, graticule with degree labels, proper legends, scale bar, and north arrow — following published cartographic conventions.

---

## License

Specify a license before publishing (e.g. MIT for code, CC-BY 4.0 for maps/figures). Add a `LICENSE` file at the repo root — GitHub can generate one for you when creating the repo, or add it after the fact via **Add file → Create new file → LICENSE**.

## Citation / Attribution

If this map or data derives from GADM or another boundary source, credit it here, e.g.:

> Administrative boundaries: GADM (https://gadm.org), version X.X.
> Basemap: Esri World Street Map, via `contextily`.

---

_Part of Mark 15 — Open Source Mapping Portfolio_
_Study area: Thakurgaon District, Bangladesh_
