# Workflow: archiving Colombian insurer clausulados

This is the method used to fill this repo, written so a later pass can improve it without reverse-engineering a scrape.

**Scope:** condiciones generales / cláusulas, anexos, tarifarios from the 39 Fasecolda affiliates. No marketing PDFs. Sister companies (e.g. Seguros de Vida Suramericana) stay out unless added later.

**Repo vs binaries:** GitHub holds roster, source map, and the SHA-256 catalog (`manifest.json`). PDF bytes may live locally when the Contents API is a poor fit. Re-download from `source_url`.

## Pipeline

1. Fasecolda WP API (39 names)
2. Per-company homepage + `document_pages` (see `sources.md`)
3. `.pdf` links matching keep-keywords (see `sample-pdfs.json`)
4. GET with a browser User-Agent; keep only `%PDF` and size over 10 KB
5. SHA-256 dedupe into `companies/<slug>/current/` and `manifest.json`

### 1. Roster

```
GET https://www.fasecolda.com/wp-json/wp/v2/companias-afiliadas?per_page=100
```

Use `X-WP-Total`. HTML pagination on fasecolda.com repeats the same names; do not treat extra pages as extra companies. Profile cards do **not** list official document libraries.

### 2. Map libraries

For each affiliate find the official homepage, then pages named clausulados / condicionados / zona de cliente / SAC / transparencia / product “condiciones generales”.

Keep PDF URLs matching: `condicion`, `clausulad`, `anexo`, `tarifar`, `condiciones-generales`.

Drop: `brochure`, `folleto`, `comercial`, `marketing`, `infografia`, `banner`.

PROAGRO: no Colombian library (Mexican `proagroseguros.mx` only). Status = blocked.

### 3. Download

```
curl -L --max-time 45 \
  -A 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36' \
  -o FILE URL
```

Accept only magic `%PDF` and size >10 KB. Failures (HTML, WAF, empty) go in the scrape report, not the catalog.

Filename = last path segment, URL-decoded, spaces to `-`. Query-only URLs: `{sha256[:12]}.pdf`. Prefer `Content-Disposition` when the server sends it.

### 4. Version

Content SHA-256 is the identity. Two URLs, one hash → one document. New hash for the same product → old file to `history/`, new to `current/`.

Filename often carries the Superintendencia / product version (`VERSION 24`, `Julio 2026`, `F-13-18-0040-281`, `PH-185`). Never trust the filename over the hash.

## Host patterns (first scrape)

| Insurer | URL pattern | Notes |
|---|---|---|
| Allianz | `allianz.co/content/dam/...` | Product code + VERSION in filename |
| AXA Colpatria | `axacolpatria.co/documents/{id}/{id}/...pdf` | Liferay IDs |
| HDI | `hdiseguros.com.co/sites/default/files/YYYY-MM/` | Truncated name returns Drupal HTML |
| Mapfre | `mapfre.com.co/media/*.pdf` | Clean public media |
| Bolívar | WP uploads on `sostenibilidad.segurosbolivar.com` | |
| Sura Generales | `segurossura.com.co/documentos/condicionados/` | Duplicate labels, same or different hashes |
| Solidaria | Azure blob `safilepwebprod.blob.core.windows.net` | Encode accents |
| Asulado | CloudFront `/assets/documentos/` | |
| Confianza | `confianza.com.co/productos/clausulados/...` | One page per ramo |
| SBS | `sbseguros.co/clausulados/...` | Auto, hogar, anexos AP |
| Quálitas | `qualitascolombia.com.co/condiciones-generales-y-coberturas` | Autos only |
| Estado | `segurosdelestado.com/pages/Clausulados` | |
| CESCE | `cesce.co/clausulados-credito` + cumplimiento | |
| Coface | `coface.com.co/sobre-nosotros/clausulados` | |
| Chubb | historico-de-condicionados | |

## Known gaps (improve these)

1. **JS / WAF:** Equidad and Colsanitas often return no PDF to curl. Next step is a real browser session, not a WAF bypass.
2. **Andina:** Oracle Content (`IdcService=GET_FILE`) — filename from `Content-Disposition`.
3. **Liberty:** brand overlap with HDI; record the URL that actually served the bytes.
4. **Tarifarios** are scarce on public libraries; missing tarifario is not a failed scrape.
5. **Fill `source_url`** when a file was found by crawling, not only from the sample list.
6. **Binary push:** catalog first; PDFs later via git/LFS if needed.
7. **Sister entities** (vida vs generales) out of scope until added to the roster.

## Weekly check

Re-fetch `document_pages`, download, compare hashes. Notify only on new or changed hashes. Stay silent otherwise.

## How to extend

- Add a company: put it on the Fasecolda roster (or an explicit allow-list), map `document_pages`, add sample PDFs, run the download step.
- Add a document kind: extend the keep-keywords and `kind` rules; do not loosen the marketing drop-list.
- Improve discovery: parse `document_pages` HTML for `.pdf` hrefs after the sample list; log `needs_browser` when HTML has zero PDF links.
