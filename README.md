# SacredGeoKB

SacredGeoKB is a compact knowledge base for Hajj and sacred geography. It contains an OWL ontology, a JSON-LD source ontology, GeoJSON spatial zones, and documentation explaining how semantic concepts are linked to geospatial features.

## Contents

- `ontology/hajj-ontology.owl`: OWL/RDF ontology export for semantic web tools.
- `ontology/hajj-ontology.jsonld`: source ontology graph with concepts, relations, Quran references, metadata, and spatial links.
- `geojson/spatial-zones.geojson`: GeoJSON FeatureCollection generated from the curated spatial zones file.
- `geojson/openstreetmap/`: raw OpenStreetMap GeoJSON files used for selected locations.
- `docs/hajj-ontology.md`: ontology documentation.
- `docs/ontology-geojson-linking.md`: explanation and mapping table for ontology-to-GeoJSON links.
- `docs/data-dictionary.md`: field definitions and source counts.

## How Ontology and GeoJSON Are Linked

Ontology concepts reference spatial data using `associated_zone_ids`, `outside_zone_ids`, or `source_zone_id`. Each value points to a GeoJSON feature with the same `id` in `geojson/spatial-zones.geojson`.

Example:

```text
SafaMarwa associated_zone_ids: safa, marwah, sai
geojson/spatial-zones.geojson features: safa, marwah, sai
```

## Metadata

Every ontology concept includes: `creator`, `title`, `data_identifier`, `publisher`, `publication_date`, `summary`, and `keywords`.

```text
creator: Ghader Kurdi
publisher: Ghader Kurdi
publication_date: 2026-07-11
```

## Dataset Summary

- Ontology nodes: 124
- GeoJSON spatial features: 50
- Raw OpenStreetMap GeoJSON files: 25

## Coordinate Order

All GeoJSON coordinates use standard GeoJSON order: `[longitude, latitude]`.
