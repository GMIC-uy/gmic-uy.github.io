# GMIC Uruguay

Static website for the **Grupo de Modelación Integrada de Cuencas (GMIC)** to browse SWAT-based catchment models, interactive maps, ongoing projects, and publications/reports metadata for Uruguay.

## Run Locally

From the project root:

```powershell
python -m http.server 8001
```

Open:

`http://127.0.0.1:8001`

## Data Sources (CSV First, JSON Fallback)

The site prefers **CSV exported from Excel**. If a CSV file is missing, it falls back to the corresponding JSON.

Primary (CSV):
- `data/source/models.csv`
- `data/source/resources.csv`
- `data/source/keywords.csv`
- `data/source/institutions.csv`
- `data/projects.csv`

Fallback (JSON):
- `data/models.json`
- `data/resources.json`
- `data/keywords.json`
- `data/institutions.json`

Catchment boundaries (GeoJSON):
- `data/catchments/*.geojson`

## Update Data From Excel

1. Maintain your workbook tables (models, resources, keywords, institutions).
2. Export each sheet as **CSV (UTF-8)** into `data/source/`.
3. Generate the JSON used as fallback:

```powershell
python tools/build_data_from_csv.py
```

Note: `data/projects.csv` is read directly by the website.

## Projects And Multiple Catchments

`data/projects.csv` supports linking a single project to multiple catchments/models.

- Use `proyect_id` (or `project_id`) to group the same project across catchments.
- You may provide multiple values in `model_id` and `cuenca` using `;` or `|` as separators.

Example:

```csv
model_id,cuenca,proyecto,proyect_id,estado,anio,url,resumen
2;6;7,San Salvador;Cebollatí;Arapey Grande,Proyecto Innovagro,4,Planificado,2026,,Short summary...
```

## Repo Layout

- `index.html`: UI + all client-side logic (table, filters, metadata drawer, map, keyword network, histogram).
- `data/`: generated JSON + GeoJSON catchment files.
- `data/source/`: source-of-truth CSV exported from Excel.
- `images/`: site images (logo, banner, etc.).
- `tools/`: helper scripts for CSV↔JSON generation.

## Credits

GMIC Uruguay · Static site maintained with HTML, CSV/JSON, and GeoJSON. Development assisted with **GPT-5.4**.
