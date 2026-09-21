# Cláusulas aseguradoras Colombia

Living archive of **condiciones generales / cláusulas**, **anexos**, and **tarifarios** from Fasecolda-affiliated insurers in Colombia.

Public repo: https://github.com/tekelala/clausulas-aseguradoras-colombia

## Scope

- **In:** condiciones generales, cláusulas de producto, anexos, tarifarios
- **Out:** marketing brochures; sister entities not on the Fasecolda affiliate card (unless added later)
- **Roster:** 39 companies from https://www.fasecolda.com/companias-afiliadas/

## Status (2026-09-21)

- **38 / 39** affiliates have PDFs in `companies/` (PROAGRO blocked — no Colombian library)
- **2212** PDFs, tracked by SHA-256 in `manifest.json`
- Method: [WORKFLOW.md](WORKFLOW.md) · Scoreboard: [ROSTER-SCRAPE.md](ROSTER-SCRAPE.md)

## Layout

```
companias-afiliadas.json
sources.json / sources.md
roster-summary.json
manifest.json              # sha256 + path for every PDF
WORKFLOW.md
ROSTER-SCRAPE.md
companies/<slug>/current/  # PDFs (openable on GitHub)
companies/<slug>/history/  # previous hashes when content changes
```

## Versioning

Each PDF is tracked by content SHA-256. When a re-scrape finds the same logical document with a new hash, the old file moves to `history/` and the new one becomes `current/`.

## How to download / refresh

`GET` with a normal browser User-Agent. Keep only `%PDF` responses larger than 10 KB. Deduplicate by SHA-256. See WORKFLOW.md.

## Monitoring

Weekly re-check of each document-library URL for new or changed PDFs.
