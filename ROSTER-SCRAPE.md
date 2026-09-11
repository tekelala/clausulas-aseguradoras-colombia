# Full-roster scrape (2026-09-11)

- Companies with ≥1 PDF: **38 / 39**
- PDFs kept (`%PDF`, >10 KB, hash-deduped): **1511**
- Size: **959.8 MB**
- Blocked: PROAGRO (no Colombian library)
- Binaries stay local; this file is the scoreboard. Method: [WORKFLOW.md](WORKFLOW.md).

## Per company

| PDFs | MB | Company | Status |
|---:|---:|---|---|
| 722 | 331.9 | Cardif Colombia Seguros Generales S.A. | ok |
| 198 | 51.8 | CHUBB Seguros Colombia S.A. | ok |
| 118 | 121.6 | Colmena Seguros S.A. | ok |
| 108 | 82.9 | MetLife Colombia Seguros de Vida S.A. | ok |
| 58 | 35.9 | Seguros del Estado | ok |
| 43 | 54.3 | Global Seguros | ok |
| 35 | 63.9 | BBVA Seguros Colombia S.A. | ok |
| 32 | 37.3 | Positiva Compañía de Seguros S.A. | ok |
| 27 | 33.7 | Seguros Mundial | ok |
| 19 | 16.5 | Cesce Colombia S.A. Compañía de seguros | ok |
| 15 | 8.5 | Liberty Colombia Compañía de Seguros S.A. | ok |
| 10 | 4.5 | Compañía Aseguradora de Fianzas S.A. Confianza | ok |
| 10 | 3.0 | Nacional de seguros S.A. | ok |
| 9 | 2.5 | Solunion Colombia Seguros de crédito S.A. | ok |
| 7 | 32.9 | La Equidad Seguros Generales Organismo Cooperativo | ok |
| 6 | 2.6 | La Previsora S.A. Compañía de Seguros | ok |
| 5 | 2.3 | Allianz Colombia | ok |
| 5 | 4.5 | Aseguradora Solidaria de Colombia Entidad Cooperativa | ok |
| 5 | 11.7 | Axa Colpatria Seguros S.A. | ok |
| 5 | 2.2 | BMI Colombia Compañía de Seguros de Vida S.A. | ok |
| 5 | 2.3 | Berkley Internacional Seguros Colombia S.A. | ok |
| 5 | 1.8 | Coface Colombia Seguros de Crédito S.A. | ok |
| 5 | 5.5 | Compañía de Seguros de Vida Aurora S.A. | ok |
| 5 | 3.8 | EKG Compañía de Seguros de Vida S.A. | ok |
| 5 | 5.5 | Everest Compañía de Seguros Generales Colombia S.A. | ok |
| 5 | 2.8 | HDI Seguros Colombia S.A. | ok |
| 5 | 2.7 | Mapfre Seguros Generales de Colombia S.A. | ok |
| 5 | 2.4 | Pan American Life de Colombia Compañía de Seguros S.A. | ok |
| 5 | 2.2 | SBS Seguros Colombia S.A | ok |
| 5 | 3.3 | Seguros Bolívar S.A. | ok |
| 4 | 2.8 | Colsanitas Seguros | ok |
| 4 | 5.6 | Seguros Generales Suramericana S.A. | ok |
| 4 | 1.5 | Skandia Seguros de Vida S.A. | ok |
| 3 | 10.3 | Quálitas Compañía de Seguros Colombia S.A. | ok |
| 3 | 0.7 | Seguros Alfa | ok |
| 2 | 0.6 | Andina Compañía de Seguros de Vida S.A. | ok |
| 2 | 0.8 | Asulado Seguros de Vida S.A. | ok |
| 2 | 0.8 | Zurich Colombia Seguros S.A. | ok |
| 0 | 0.0 | PROAGRO | blocked |

## Notes

- **Cardif (722)** are CSFC-coded condiciones (bancassurance variants), not brochures. Sample: *Póliza seguro de desempleo… CONDICIONES*.
- **Chubb (198)** is `historico-de-condicionados` (Superintendencia codes).
- **MetLife (108)** is mostly disease anexos.
- **Colmena (118)** all filenames match keep-keywords.
- **Equidad** files came from `sftp.laequidadseguros.coop` (curl worked; earlier WAF note was the HTML site).
- **Estado** URLs need percent-encoding of spaces/accents.
- **Liberty** mix of Liberty API samples and HDI condicionados (brand overlap); keep the URL that served the bytes.

## Needs a browser next

Curl got samples but listing pages had zero PDF hrefs:

- Colsanitas product pages (JS/WAF)
- Everest policies pages (JS)
- Liberty cumplimiento / RC landings (JS)
- Zurich homepage / hogar (JS/bot)
- Andina homepage SPA + Oracle UCM
- SBS Modyo listing pages (CDN samples still downloaded)
- Solidaria biblioteca (Next.js; Azure blob samples OK)
- PALIG resource center
- Previsora `/vida-y-ap` and autos pages
- Confianza some ramo pages

Do not treat missing tarifarios as a scrape failure. Do not restage the public bot share until the workflow is confirmed.
