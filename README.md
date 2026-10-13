# Cláusulas aseguradoras Colombia

Living archive of **condiciones generales / cláusulas**, **anexos**, and **tarifarios** from Fasecolda-affiliated insurers in Colombia.

Public repo: https://github.com/tekelala/clausulas-aseguradoras-colombia

## Scope

- **In:** condiciones generales, cláusulas de producto, anexos, tarifarios
- **Out:** marketing brochures; sister entities not on the Fasecolda affiliate card (unless added later)
- **Roster:** 39 companies from https://www.fasecolda.com/companias-afiliadas/

## Status (2026-10-12)

- **38 / 39** affiliates have PDFs in `companies/` (PROAGRO blocked — no Colombian library)
- **2218** PDFs, tracked by SHA-256 in `manifest.json`
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

## Índice de códigos (búsqueda por código)

Grupo ilao mantiene un índice de **todos los códigos** de cada clausulado como llaves de búsqueda:

- [`INDICE_CODIGOS.md`](INDICE_CODIGOS.md): una sección por aseguradora (nombre oficial Fasecolda) con título, código SFC principal, otros códigos y enlace al PDF.
- [`INDICE_CODIGOS.csv`](INDICE_CODIGOS.csv): una fila por PDF (vigente e histórico) con ruta, SHA-256, código SFC principal y tipo (P/A/NT), todos los códigos SFC, códigos internos (p. ej. Sura `F-13-18-0040-281`, códigos cortos `1308-P-05-…`, códigos de producto en el nombre del archivo, `Código`/`Forma`/`Versión`/`Ref`), clave de grupo (código SFC tipo P sin fecha ni sufijo) y clasificación (`con código SFC`, `solo código interno`, `sin código`). Varios códigos se separan con ` | `.

**Cómo buscar:** abra `INDICE_CODIGOS.md` en GitHub y use Ctrl+F con el código (o parte, p. ej. `1411-P-37`), o use la búsqueda de GitHub del repositorio (`repo:grupo-ilao/clausulado-repositorio-aseguradoras <código>`). Para filtrar, abra el CSV en Excel/Sheets. La clave de grupo permite ver versiones del mismo producto. El código principal prioriza tipo P, luego A, luego NT, en página 1 y con la fecha más reciente. Los códigos se extraen automáticamente de las 3 primeras y 3 últimas páginas; los PDF escaneados sin texto figuran como `sin código`.

## Versioning

Each PDF is tracked by content SHA-256. When a re-scrape finds the same logical document with a new hash, the old file moves to `history/` and the new one becomes `current/`.

## How to download / refresh

`GET` with a normal browser User-Agent. Keep only `%PDF` responses larger than 10 KB. Deduplicate by SHA-256. See WORKFLOW.md.

## Monitoring

Weekly re-check of each document-library URL for new or changed PDFs.
