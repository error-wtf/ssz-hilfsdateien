# Export-Pfade Inventar - Alle SSZ Scripts
**Erstellt:** 2025-10-27 03:00 UTC+01  
**Zweck:** Übersicht aller Output-Verzeichnisse für systematisches Aufräumen

---

## 🎯 SOLL-Zustand (Ziel)

Alle Scripts sollen exportieren nach:
```
D:\SSZ_Render\
├── audio\           # WAV-Dateien (TTS)
├── video\           # MP4-Dateien (final)
├── timelines\       # YAML-Dateien (config)
├── data\            # CSV/JSON (results)
├── plots\           # PNG/SVG (visualizations)
├── logs\            # TXT (errors)
└── final\           # GIF-Previews, manifests
```

---

## 🔴 IST-Zustand (Aktuell)

### D:\ Root-Verzeichnis (CHAOS!)

**Animation-Scripts → Output:**
| Script | Output | Aktueller Pfad | Problem |
|--------|--------|----------------|---------|
| `ssz_animation_master.py` | MP4, WAV, YAML | `D:\SSZ_Render\` | ✅ Korrekt |
| `ssz_bigbang_vs_ssz_anim.py` | GIF, MP4 | `/mnt/data` | ❌ Linux-Pfad! |
| `ssz_animation_perfect.py` | GIF | `D:\` | ⚠️ Root (Unordnung) |
| `ssz_animation_scientific.py` | GIF | `D:\` | ⚠️ Root (Unordnung) |
| `create_all_language_versions.py` | GIF (3×) | `D:\` | ⚠️ Root (Unordnung) |
| `make_ssz_anim.py` | GIF, MP4 | `/mnt/data` | ❌ Linux-Pfad! |
| `blackhole_animation.py` | GIF, PNG | `D:\` | ⚠️ Root (Unordnung) |
| `ssz_simple_render.py` | GIF | `D:\` | ⚠️ Root (Unordnung) |

**Black-Hole Scripts → Output:**
| Script | Output | Aktueller Pfad | Problem |
|--------|--------|----------------|---------|
| `ssz_blackhole_bomb_complete.py` | CSV, JSON | `D:\` | ⚠️ Root (Unordnung) |
| `ssz_bomb_animation.py` | GIF, PNG | `D:\` | ⚠️ Root (Unordnung) |
| `ssz_gr_bridge.py` | JSON, MD | `D:\` | ⚠️ Root (Unordnung) |
| `ssz_parameter_scan.py` | CSV | `D:\` | ⚠️ Root (Unordnung) |
| `ssz_resonance_explorer.py` | CSV | `D:\` | ⚠️ Root (Unordnung) |
| `ssz_live_visualizer.py` | Plots | `D:\` | ⚠️ Root (Unordnung) |
| `ssz_plot_packager.py` | ZIP | `D:\` | ⚠️ Root (Unordnung) |

**Proof/LIGO Scripts → Output:**
| Script | Output | Aktueller Pfad | Problem |
|--------|--------|----------------|---------|
| `ssz_proof_sweep_v5.py` | CSV, Plots | `/mnt/data` | ❌ Linux-Pfad! |
| `ssz_proof_sweep_v6.py` | CSV, Plots | `/mnt/data` | ❌ Linux-Pfad! |
| `ssz_proof_check_v6.py` | JSON | `D:\` | ⚠️ Root (Unordnung) |
| `ssz_viz_v6.py` | PNG, GIF | `D:\` | ⚠️ Root (Unordnung) |
| `segmented_ligo_compare*.py` | CSV | `D:\` | ⚠️ Root (Unordnung) |
| `segmented_mass*.py` | CSV | `D:\` | ⚠️ Root (Unordnung) |
| `fetch_ligo.py` | CSV | `D:\data\` | ⚠️ Unklar |

**Sonstige Scripts → Output:**
| Script | Output | Aktueller Pfad | Problem |
|--------|--------|----------------|---------|
| `researchgate_weinberg_response.py` | PNG, TXT | `D:\` | ⚠️ Root (Unordnung) |
| `data-csv.py` | CSV | `D:\` | ⚠️ Root (Unordnung) |
| `diag-csv.py` | CSV | `D:\` | ⚠️ Root (Unordnung) |
| `icd-csv.py` | CSV | `D:\` | ⚠️ Root (Unordnung) |
| `train.py` | Modelle | `D:\` | ⚠️ Root (Unordnung) |

---

### G:\Black_Hole_Bomb\ (OK, aber isoliert)

**Scripts → Output:**
| Script | Output | Aktueller Pfad | Problem |
|--------|--------|----------------|---------|
| `ssz_blackhole_bomb.py` | CSV, JSON | `G:\Black_Hole_Bomb\` | ✅ OK (isoliert) |
| `ssz_blackhole_bomb_complete.py` | CSV, JSON | `G:\Black_Hole_Bomb\` | ✅ OK (isoliert) |
| `ssz_bomb_animation.py` | GIF, PNG | `G:\Black_Hole_Bomb\` | ✅ OK (isoliert) |
| `ssz_gr_bridge.py` | JSON, MD | `G:\Black_Hole_Bomb\` | ✅ OK (isoliert) |

**Bestehende Outputs:**
- `spectrum_results.csv` (6 KB)
- `growth_best_mode.csv` (160 bytes)
- `run_config.json` (494 bytes)
- `summary.json` (492 bytes)
- `SSZ_BLACKHOLE_BOMB_RESULTS.md` (12 KB)
- `extended_results/` (Verzeichnis)

**Status:** ✅ Gut organisiert, aber nicht im Haupt-Repository

---

### G:\UNSORTED\ (CHAOS!)

**Scripts → Output:**
| Script | Output | Aktueller Pfad | Problem |
|--------|--------|----------------|---------|
| `ssz_blackhole_bomb*.py` | CSV, JSON | `G:\UNSORTED\` | ⚠️ Duplikat zu G:\Black_Hole_Bomb |
| `ssz_proof_sweep*.py` | CSV | `G:\UNSORTED\` | ⚠️ Duplikat zu D:\ |
| `blackhole_animation.py` | GIF | `G:\UNSORTED\` | ⚠️ Duplikat zu D:\ |
| `segmented_space_time_full_proof.py` | CSV | `G:\UNSORTED\` | ⚠️ Unklare Version |

**Bestehende Outputs:**
- `parameter_scan_results.csv` (24 KB)
- `gr_bridge_summary.json` (2.5 KB)
- `scan_summary.json` (1.5 KB)
- `weinberg_response.png` (183 KB)
- Diverse GIFs und PNGs

**Status:** ❌ Komplett unorganisiert, viele Duplikate

---

## 📊 ZUSAMMENFASSUNG

### Pfad-Verteilung:

| Pfad | Anzahl Scripts | Anzahl Outputs | Status |
|------|----------------|----------------|--------|
| `D:\` | ~105 | ~50+ | ❌ CHAOS |
| `D:\SSZ_Render\` | 1 | ~10 | ✅ OK |
| `/mnt/data` | ~10 | 0 (nicht vorhanden) | ❌ FEHLER |
| `G:\Black_Hole_Bomb\` | 9 | 7 | ✅ OK |
| `G:\UNSORTED\` | 25 | ~20 | ❌ CHAOS |

### Problem-Kategorien:

| Problem | Anzahl betroffene Scripts | Schweregrad |
|---------|---------------------------|-------------|
| Linux-Pfad `/mnt/data` | ~10 | 🔴 KRITISCH |
| D:\ Root (Unordnung) | ~95 | 🟡 WICHTIG |
| Duplikate | ~20 | 🟡 WICHTIG |
| Unbekannte Pfade | ~10 | 🟠 MITTEL |

---

## 🔧 LÖSUNGSPLAN

### Schritt 1: Pfade-Mapping erstellen

Für jedes Script:
1. Öffnen
2. Nach `Path(`, `outdir`, `output`, `export` suchen
3. Aktuellen Pfad notieren
4. Neuen Pfad zuweisen

### Schritt 2: Zentrale Config

**Erstelle:** `D:\ssz_paths_config.py`

```python
from pathlib import Path

# Base directory
BASE_DIR = Path(r"D:\SSZ_Render")

# Subdirectories
PATHS = {
    'audio': BASE_DIR / 'audio',
    'video': BASE_DIR / 'video',
    'timelines': BASE_DIR / 'timelines',
    'data': BASE_DIR / 'data',
    'plots': BASE_DIR / 'plots',
    'logs': BASE_DIR / 'logs',
    'final': BASE_DIR / 'final',
}

# Ensure all directories exist
def ensure_paths():
    for path in PATHS.values():
        path.mkdir(parents=True, exist_ok=True)
```

**In jedem Script importieren:**
```python
from ssz_paths_config import PATHS, ensure_paths

ensure_paths()
output_file = PATHS['video'] / 'ssz_output.mp4'
```

### Schritt 3: Scripts migrieren

**Priorität 1 (SOFORT):**
- `ssz_bigbang_vs_ssz_anim.py` → Pfad von `/mnt/data` auf `D:\SSZ_Render\video\`
- `make_ssz_anim.py` → Pfad von `/mnt/data` auf `D:\SSZ_Render\video\`
- `ssz_proof_sweep_v5.py` → Pfad von `/mnt/data` auf `D:\SSZ_Render\data\`

**Priorität 2 (HEUTE):**
- Alle Animation-Scripts → `D:\SSZ_Render\video\`
- Alle Proof-Scripts → `D:\SSZ_Render\data\`
- Alle Bomb-Scripts → `D:\SSZ_Render\data\`

**Priorität 3 (MORGEN):**
- Bestehende Outputs von `D:\` nach `D:\SSZ_Render\` verschieben
- Duplikate in G:\ bereinigen

### Schritt 4: Git-Vorbereitung

**Zu committen:**
```
H:\WINDSURF\Segmented-Spacetime-...\
├── scripts/
│   ├── animations/
│   │   ├── ssz_animation_master.py
│   │   ├── ssz_bigbang_vs_ssz_anim.py
│   │   └── ... (alle Animation-Scripts)
│   ├── proof/
│   │   ├── ssz_proof_sweep_v6.py
│   │   └── ... (alle Proof-Scripts)
│   ├── blackhole/
│   │   ├── ssz_blackhole_bomb_complete.py
│   │   └── ... (alle Bomb-Scripts)
│   └── utils/
│       └── ssz_paths_config.py
├── outputs/
│   └── previews/
│       ├── ssz_scientific_de.gif (< 10 MB)
│       └── ... (nur kleine Previews)
└── docs/
    ├── EXPORT_PATHS_INVENTORY.md (diese Datei)
    └── FEHLERANALYSE_ERGEBNIS.md
```

**NICHT zu committen (zu groß):**
- `D:\SSZ_Render\` (komplett)
- `G:\Black_Hole_Bomb\` (komplett)
- `G:\UNSORTED\` (komplett)
- Alle MP4-Dateien > 50 MB
- Alle WAV-Dateien

---

## 📋 CHECKLISTE

### Vor der Migration:

- [ ] Backup von `D:\` erstellen
- [ ] Backup von `G:\Black_Hole_Bomb\` erstellen
- [ ] Backup von `G:\UNSORTED\` erstellen
- [ ] Liste aller Output-Dateien erstellen
- [ ] Speicherplatz prüfen (min. 5 GB frei)

### Migration durchführen:

- [ ] `D:\SSZ_Render\` Verzeichnisstruktur erstellen
- [ ] `ssz_paths_config.py` erstellen und testen
- [ ] Scripts einzeln migrieren (mit Test nach jeder Änderung)
- [ ] Bestehende Outputs verschieben
- [ ] Duplikate entfernen oder nach `_bak/` verschieben

### Nach der Migration:

- [ ] Alle Scripts testen (mindestens eines pro Kategorie)
- [ ] Dokumentation aktualisieren
- [ ] Git-Commits vorbereiten
- [ ] README mit neuen Pfaden aktualisieren

---

## 🎯 ERWARTETES ENDERGEBNIS

```
D:\SSZ_Render\
├── audio\
│   ├── ssz_intro_de.wav
│   ├── ssz_intro_en.wav
│   └── ssz_intro_it.wav
├── video\
│   ├── ssz_intro_de.mp4
│   ├── ssz_intro_en.mp4
│   └── ssz_intro_it.mp4
├── timelines\
│   ├── ssz_anim_de.yaml
│   ├── ssz_anim_en.yaml
│   └── ssz_anim_it.yaml
├── data\
│   ├── spectrum_results.csv
│   ├── growth_best_mode.csv
│   ├── parameter_scan_results.csv
│   └── ... (alle CSVs/JSONs)
├── plots\
│   ├── blackhole_animation.png
│   ├── weinberg_response.png
│   └── ... (alle Plots)
├── logs\
│   └── tts_fallback_de.txt
└── final\
    ├── ssz_intro_trilanguage.gif
    ├── manifest.json
    └── ... (Preview-GIFs)
```

**Repository:**
```
H:\WINDSURF\Segmented-Spacetime-...\
├── scripts\          # Alle Python-Scripts
├── outputs\previews\ # Nur kleine GIFs (< 10 MB)
└── docs\             # Dokumentation
```

---

**Status:** ✅ INVENTAR KOMPLETT | BEREIT FÜR MIGRATION  
**Next Step:** User-Entscheidung über Migrations-Reihenfolge

© 2025 Carmen Wrede, Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
