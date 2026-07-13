# Data Dictionary

## Ontology Metadata Fields

- `creator`: Person who created the ontology node metadata. Current value: `Ghader Kurdi`.
- `title`: Human-readable title, usually derived from `label_en` or `label_ar`.
- `data_identifier`: Stable identifier for the concept. This is the same value as `id`.
- `publisher`: Person or entity publishing the node metadata. Current value: `Ghader Kurdi`.
- `publication_date`: Publication date of the metadata record.
- `summary`: Short description derived from `definition`, `definition_ar`, or `comment`.
- `keywords`: Search terms derived from labels, type, id, aliases, spatial type, and Quran references.

## GeoJSON Feature Properties

- `id`: Stable spatial zone identifier used by ontology links.
- `name` / labels if present: Human-readable spatial name.
- `source`: Source of coordinates, such as `OpenStreetMap`, `GoogleMap`, or `GoogleMyMap`.
- `boundary`: Original geometry in `spatial-zones.json`; in GeoJSON this is moved to `geometry`.
- `geometry`: GeoJSON geometry in `[longitude, latitude]` coordinate order.

## Spatial Source Counts

| Source | Zone count |
| --- | ---: |
| GoogleMap | 17 |
| GoogleMyMap | 1 |
| Missing | 6 |
| OpenStreetMap | 26 |
| PendingCoordinates | 5 |
