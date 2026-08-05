# BOOK VERSION INVENTORY — V23/V51/V52/PERFECTED
**Datum:** 2026-05-20
**Phase:** D — Buchversionen inventarisiert (nicht gelesen)
**Status:** INVENTARISIERT — Keine Inhalte gelesen

---

## Buch-Build-Ordnern in book-full/05_OUTPUT

| Ordner | Enthält | Status |
|--------|---------|--------|
| **FINAL_BOOKS** | PDF, MD, TEX — SSZ_BOOK_DE.pdf | Kanonisch? |
| **FINAL_CANONICAL** | TEX — DE, EN, IT (FINAL_CANONICAL_DE.tex) | Kanonisch? |
| **SSZ_CANONICAL_REBUILD_V52** | de/en/it (nach V52 rebuild) | V52 Struktur |
| **PERFECTION_BUILD_V55** | 00_input, 01_inventories, 02_repair, 03_repaired, 04_registries, 08_pdf_build | V55 Perfektion |
| **SSZ_BOOK_PERFECTION_WORKSPACE** | SSZ_BOOK_DE_PERFECTED.md, SSZ_BOOK_EN_PERFECTED.md | Perfected MDs |
| **V7_BUILD** | 00_originals bis 04_build | Ältere V7 |
| **BOOK_REBUILD / BOOK_REBUILD_V2** | Canon-Registry, Conflict-Report | Rebuild-Logs |
| **chapters/** | TEX-Kapitel | Rohkapitel |
| **FORENSIC_SOURCE_OF_TRUTH** | CANONICAL_THEORY_MAP.md, LOCKED/ | Forensik |

---

## Versionen-Suche

| Version | Gefunden? | Pfad(e) |
|---------|-----------|---------|
| V23 | ❌ Nicht gefunden | Keine Datei/Ordner mit "V23" oder "v23" |
| V51 | ❌ Nicht gefunden | Keine Datei/Ordner mit "V51" oder "v51" |
| V52 | ✅ Gefunden (3 Skripte) | check_v52_content.py, copy_v52_to_v47.py, restore_it_from_v52.py |
| V53 | ✅ Erwähnt (2 Mypy-Caches) | build_it_v53_final |
| V54 | ❌ Nicht gefunden | — |
| V55 | ✅ Gefunden (Ordner) | PERFECTION_BUILD_V55 |
| PERFECTED | ✅ Gefunden | SSZ_BOOK_DE_PERFECTED.md, SSZ_BOOK_EN_PERFECTED.md |

---

## Wichtige Erkenntnis

```
V23 und V51 wurden NICHT als explizite Dateien/Ordner gefunden.
Die Versionierung scheint über Build-Ordner zu laufen:
  V7_BUILD → SSZ_CANONICAL_REBUILD_V52 → PERFECTION_BUILD_V55

Die "perfected" MDs liegen in SSZ_BOOK_PERFECTION_WORKSPACE:
  SSZ_BOOK_DE_PERFECTED.md
  SSZ_BOOK_EN_PERFECTED.md

Die finalen PDFs liegen in FINAL_BOOKS:
  SSZ_BOOK_DE.pdf (mit TEX-Quelle)

Kanonische TEX-Versionen in FINAL_CANONICAL:
  FINAL_CANONICAL_DE.tex, _EN.tex, _IT.tex
```

---

## Nächster Schritt

INHALTE LESEN (nicht nur inventarisieren):
1. FINAL_BOOKS/SSZ_BOOK_DE.pdf — Hauptbuch
2. SSZ_BOOK_PERFECTION_WORKSPACE/SSZ_BOOK_DE_PERFECTED.md
3. FINAL_CANONICAL/FINAL_CANONICAL_DE.tex
4. Auf formelrelevante Kapitel durchsuchen (insb. Ch.31, Inspiral, Phase)
