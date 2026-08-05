# run_full_suite.py - MD Echo Filter Fix

## Problem

`run_full_suite.py` rief in Phase 8 `print_all_md` OHNE Filter auf:

```python
# VORHER (Zeile 304):
cmd = ["python", "-m", "tools.print_all_md", "--root", ".", "--order", "path"]
```

**Ergebnis:** 
- ❌ Alle MD-Dateien wurden ausgegeben
- ❌ Inklusive aller Papers (Segmented Spacetime Theory, etc.)
- ❌ Inklusive Theory-Dokumentation
- ❌ Inklusive README-Dateien
- ❌ Hunderte von Zeilen irrelevanter Output

---

## Lösung

Jetzt werden **nur Dateien im reports/ Verzeichnis** ausgegeben:

```python
# NACHHER (Zeilen 315-328) - VIEL EINFACHER:
reports_dir = Path("reports")

if reports_dir.exists() and reports_dir.is_dir():
    cmd = [
        "python", "-m", "tools.print_all_md",
        "--root", "reports",           # Nur reports/ Verzeichnis
        "--order", "path"
    ]
```

**Warum einfacher?**
- ✅ Keine komplizierten Include/Exclude Patterns
- ✅ Alle Outputs landen sowieso in `reports/`
- ✅ Papers sind nicht in `reports/` → automatisch ausgeschlossen
- ✅ Zuverlässiger und leichter zu verstehen

---

## Was wird jetzt ausgegeben?

### ✅ NUR REPORTS/ VERZEICHNIS:

```
reports/
├── RUN_SUMMARY.md                                      ← Suite Zusammenfassung
├── 2025-10-17_gaia_ssz_real/
│   ├── output-summary.md                              ← Analyse Output
│   ├── pytest_results.md                              ← Test Ergebnisse
│   └── ring_temperature_analysis.md                   ← Ring Analysen
├── g79_test.txt                                       ← G79 Beispiel
└── cygx_test.txt                                      ← Cygnus X Beispiel
```

**Das war's!** Nur diese Dateien werden ausgegeben.

### ❌ AUTOMATISCH AUSGESCHLOSSEN (Nicht in reports/):

Alle diese Dateien sind **nicht** in `reports/` und werden deshalb ignoriert:

```
# Papers (in Root oder papers/):
Segmented-Spacetime-*.md
DualVelocitiesinSegmentedSpacetime-*.md
EmergentSpatialAxesfromOrthogonalTemporalInterference.md

# Theory Docs:
docs/theory/*.md

# README-Dateien:
README.md
ci/README.md
tests/REAL_DATA_TESTS_README.md

# Sonstige:
BUGFIXES_2025-10-18.md
COMPREHENSIVE_TESTS_SUMMARY.md
etc.
```

---

## Vergleich

### Vorher (ALT - Alle MD-Dateien):
```bash
$ python run_full_suite.py

PHASE 8: ECHOING ALL MARKDOWN OUTPUTS
================================================================================

=== papers/SegmentedSpacetime-ANewPerspectiveonLightGravityandBlackHoles.md ===
# Segmented Spacetime - A New Perspective...
[... 500+ Zeilen Theory ...]

=== DualVelocitiesinSegmentedSpacetime-EscapeFallandGravitationalRedshift.md ===
# Dual Velocities in Segmented Spacetime...
[... 300+ Zeilen Theory ...]

=== README.md ===
# SSZ Projection Suite
[... 200+ Zeilen README ...]

[... VIELE weitere irrelevante Dateien ...]

TOTAL: 30+ MD-Dateien, 5000+ Zeilen Output ❌
```

### Nachher (NEU - Nur reports/):
```bash
$ python run_full_suite.py

PHASE 8: ECHOING REPORTS & SUMMARIES
================================================================================
[RUNNING] Markdown Echo
  Directory: reports/

=== reports/RUN_SUMMARY.md ===
# SSZ Suite Run Summary
**Date:** 2025-10-18 13:45:00
- Total Phases: 12
- Passed: 12
- Failed: 0
[... Test-Zusammenfassung ...]

=== reports/2025-10-17_gaia_ssz_real/output-summary.md ===
# Analysis Output Summary
- PPN tests: PASSED
- Energy conditions: PASSED
[... Nur relevante Analyse-Ergebnisse ...]

TOTAL: 2-3 MD-Dateien, ~200 Zeilen Output ✅
```

---

## Technische Details

### Vereinfachter Ansatz:

Statt komplizierter Include/Exclude Patterns verwenden wir jetzt einfach:

```python
# EINFACH: Nur ein Verzeichnis durchsuchen
cmd = [
    "python", "-m", "tools.print_all_md",
    "--root", "reports",    # Nur dieses Verzeichnis
    "--order", "path"       # Nach Pfad sortieren
]
```

**Vorteile:**
- ✅ Viel einfacher zu verstehen
- ✅ Keine Pattern-Matching-Probleme
- ✅ Funktioniert zuverlässig
- ✅ Papers/Theory sind automatisch ausgeschlossen (nicht in reports/)

### Warum kein Root-Scan mehr?

Das alte System scannte das gesamte Repository und versuchte mit Patterns zu filtern:

```python
# ALT - zu kompliziert:
--root .                    # Scannt ALLES
--include *output*.md       # Dann filtern...
--exclude papers/**         # Und excluden...
```

**Problem:** Pattern-Matching ist kompliziert und fehleranfällig.

**Lösung:** Nur das `reports/` Verzeichnis scannen:

```python
# NEU - viel einfacher:
--root reports              # Scannt nur reports/
```

---

## Usage

### Mit MD Echo (Standard):
```bash
python run_full_suite.py
# → Zeigt gefilterte MD-Dateien
```

### Ohne MD Echo:
```bash
python run_full_suite.py --no-echo-md
# → Kein MD-Output
```

### Quick Mode (ohne MD Echo):
```bash
python run_full_suite.py --quick
# → Schnelle Tests, dann MD-Output
```

---

## Änderungen im Detail

### Datei: `run_full_suite.py`

#### 1. Docstring (Zeilen 2-37):
```python
# ALT:
"""... echoes all Markdown outputs."""

# NEU:
"""... echoes relevant Markdown outputs."""

# + Neue Sektion:
MD Echo Includes:
    - *output*.md (analysis outputs)
    - reports/**/*.md (generated reports)
    ...
    
MD Echo Excludes:
    - papers/** (theory papers)
    - docs/theory/** (theory documentation)
    ...
```

#### 2. Phase 8 Header (Zeile 302):
```python
# ALT:
print_header("ECHOING ALL MARKDOWN OUTPUTS", "=")

# NEU:
print_header("ECHOING RELEVANT MARKDOWN OUTPUTS", "=")
```

#### 3. Command Construction (Zeilen 309-334):
```python
# ALT (1 Zeile):
cmd = ["python", "-m", "tools.print_all_md", "--root", ".", "--order", "path"]

# NEU (16 Zeilen mit Filtern):
cmd = [
    "python", "-m", "tools.print_all_md",
    "--root", ".",
    "--order", "path",
    "--include", "*output*.md",
    "--include", "reports/**/*.md",
    # ... weitere Includes ...
    "--exclude", "papers/**",
    "--exclude", "docs/theory/**",
    # ... weitere Excludes ...
]
```

#### 4. Info-Output (Zeilen 326-329):
```python
# ALT:
print(f"[RUNNING] Markdown Echo")
print(f"  Command: {' '.join(cmd)}")

# NEU:
print(f"[RUNNING] Markdown Echo (filtered)")
print(f"  Includes: *output*.md, reports/*.md, *_analysis*.md, *_results*.md, *_summary*.md")
print(f"  Excludes: papers/, theory docs, READMEs")
print(f"  Command: {' '.join(cmd)}")
```

#### 5. UTF-8 Encoding (Zeile 332):
```python
# ALT:
subprocess.run(cmd, check=False)

# NEU:
subprocess.run(cmd, check=False, encoding="utf-8", errors="replace")
```

---

## Testing

### Test 1: Normale Ausführung
```bash
python run_full_suite.py --quick
```

**Erwartung:**
- ✅ Nur Output-, Report- und Analyse-MD-Dateien
- ❌ Keine Papers
- ❌ Keine READMEs
- ❌ Keine Theory-Docs

### Test 2: Ohne MD Echo
```bash
python run_full_suite.py --quick --no-echo-md
```

**Erwartung:**
- ✅ Phase 8 wird komplett übersprungen
- ✅ Kein MD-Output

### Test 3: Manueller Test des Filters
```bash
python -m tools.print_all_md --root . --include "*output*.md" --include "reports/**/*.md" --exclude "papers/**" --exclude "**/README*.md"
```

**Erwartung:**
- ✅ Nur gefilterte Dateien
- ✅ Reihenfolge nach Pfad

---

## Vorteile

### 1. Übersichtlichkeit
- Nur relevante Test- und Analyse-Ergebnisse
- Keine 1000+ Zeilen Theory-Output

### 2. Performance
- Schnellerer Output (weniger Dateien)
- Weniger I/O

### 3. Klarheit
- User sehen nur was wichtig ist
- Theory-Papers bleiben im Repository, werden aber nicht ausgegeben

### 4. Flexibilität
- Filter können leicht angepasst werden
- Neue Patterns können hinzugefügt werden

---

## Zukünftige Erweiterungen

### Weitere Include-Pattern:
```python
"--include", "*_validation*.md",   # Validierungs-Dateien
"--include", "*_test*.md",         # Test-Protokolle
"--include", "experiments/**/*.md", # Experiment-Ergebnisse
```

### Weitere Exclude-Pattern:
```python
"--exclude", "**/*draft*.md",      # Draft-Dateien
"--exclude", "**/*WIP*.md",        # Work-in-Progress
"--exclude", "backups/**",         # Backup-Ordner
```

---

## Lizenz

Anti-Capitalist Software License (v 1.4)
© 2025 Carmen Wrede, Lino Casu
