# Pilot scrape notes (2026-09-11)

First end-to-end download of condiciones/anexos (no marketing) for 6 high-confidence Fasecolda affiliates.

## Result

| Company | PDFs | URL pattern |
|---|---|---|
| Allianz | 5 | `allianz.co/content/dam/...` DAM; filenames include product code + VERSION |
| AXA Colpatria | 5 | `axacolpatria.co/documents/{id}/{id}/...pdf` |
| HDI | 5 | `hdiseguros.com.co/sites/default/files/YYYY-MM/...pdf` — month in filename; URL encoding of spaces matters. A truncated URL returned HTML, not PDF. |
| Mapfre | 5 | `mapfre.com.co/media/*.pdf` |
| Seguros Bolívar | 5 | WordPress uploads under `sostenibilidad.segurosbolivar.com` |
| Seguros Sura | 4 | `segurossura.com.co/documentos/condicionados/...` — two sample URLs hashed identical (same file, two labels) |

Targeted sample URLs with a browser User-Agent returned real `%PDF` files.

## How to get them

1. Start from `sources.json` `document_pages` + `sample_pdfs`.
2. `GET` with a normal browser User-Agent. Verify magic bytes `%PDF` and size >10KB; HTML/WAF pages fail that check.
3. Save `companies/<slug>/current/<safe-name>.pdf`. Track `sha256` in `manifest.json`.
4. Version hint is often in the filename (VERSION 24, Julio 2026, F-13-18-0040-281, PH-185).
5. Deduplicate by hash before storing.

## Failures / caveats

- Wrong or truncated filenames (HDI) return Drupal HTML.
- Some libraries are JS/WAF (Equidad, Colsanitas legacy) — browser fallback later.
- PROAGRO has no Colombian document library (Mexican site only).
- Same-hash files are one document, not two versions.

## Next after this workflow is confirmed

Scrape remaining mapped companies the same way. Weekly routine re-checks `document_pages` and only notifies on new/changed hashes.
