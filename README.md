# Cláusulas aseguradoras Colombia

Living archive of **condiciones generales / cláusulas**, **anexos**, and **tarifarios** from Fasecolda-affiliated insurers in Colombia.

Public repo (for now): https://github.com/tekelala/clausulas-aseguradoras-colombia

## Scope

- **In:** condiciones generales, cláusulas de producto, anexos, tarifarios
- **Out:** marketing brochures; sister entities not on the Fasecolda affiliate card (unless added later)
- **Roster:** 39 companies from https://www.fasecolda.com/companias-afiliadas/ (snapshot in `companias-afiliadas.json`)

## Layout

```
companias-afiliadas.json   # Fasecolda roster + ramos
sources.yaml               # per-company homepage + document library URLs
manifest.json              # catalog of downloaded PDFs (hash, version, source URL)
companies/<slug>/          # PDFs and per-company notes
  current/                 # latest known version of each document
  history/                 # previous versions when content hash changes
```

## Versioning

Each PDF is tracked by content SHA-256. When a re-scrape finds the same logical document with a new hash, the old file moves to `history/` and the new one becomes `current/`. `manifest.json` records source URL, first seen, last seen, and version hints from filenames / Superintendencia codes.

## Monitoring

Weekly re-check of each `document_pages` URL for new or changed PDFs.
