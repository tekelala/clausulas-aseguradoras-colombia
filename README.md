# Cláusulas aseguradoras Colombia

Living archive of **condiciones generales / cláusulas**, **anexos**, and **tarifarios** from Fasecolda-affiliated insurers in Colombia.

Public repo (for now): https://github.com/tekelala/clausulas-aseguradoras-colombia

## Scope

- **In:** condiciones generales, cláusulas de producto, anexos, tarifarios
- **Out:** marketing brochures; sister entities not on the Fasecolda affiliate card (unless added later)
- **Roster:** 39 companies from https://www.fasecolda.com/companias-afiliadas/ (snapshot in `companias-afiliadas.json`)

## Status (2026-09-11)

- Source map: 38 mapped, 1 blocked (PROAGRO, Mexican site only). See `sources.md`.
- First scrape: 29 PDFs from Allianz, AXA Colpatria, HDI, Mapfre, Bolívar, Sura Generales. Catalog with SHA-256 + source URLs is in `manifest.json`. Method notes: `pilot/NOTES.md`.
- PDF binaries are kept locally for now (not committed). Re-download from `source_url` in the catalog, or wait for a later binary push.

## Layout

```
companias-afiliadas.json   # Fasecolda roster + ramos
sources.md                 # per-company homepage + document library URLs
manifest.json              # catalog of downloaded PDFs (hash, source URL)
companies/<slug>/          # PDFs and per-company notes (binaries local for now)
  current/                 # latest known version of each document
  history/                 # previous versions when content hash changes
```

## Versioning

Each PDF is tracked by content SHA-256. When a re-scrape finds the same logical document with a new hash, the old file moves to `history/` and the new one becomes `current/`. `manifest.json` records source URL and version hints from filenames / Superintendencia codes.

## How to download

`GET` with a normal browser User-Agent. Keep only `%PDF` responses larger than 10 KB. Deduplicate by SHA-256.

## Monitoring

Weekly re-check of each document-library URL for new or changed PDFs.
