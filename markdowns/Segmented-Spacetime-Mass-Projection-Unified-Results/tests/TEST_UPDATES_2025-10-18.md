# Test-Ordner Updates - 2025-10-18

## Übersicht

Alle Test-Dateien wurden für **UTF-8-Kompatibilität** und **Planck-Pfad-Intelligenz** aktualisiert.

---

## 🔧 Aktualisierte Dateien

### 1. **tests/test_segwave_cli.py**
**Änderungen:** 10 subprocess.run() Aufrufe aktualisiert

**Problem:** Fehlende UTF-8 Encoding-Parameter führten zu 'charmap' codec Fehlern auf Windows

**Lösung:**
```python
# Vorher:
result = subprocess.run(
    [sys.executable, str(CLI_SCRIPT), "--help"],
    capture_output=True,
    text=True
)

# Nachher:
result = subprocess.run(
    [sys.executable, str(CLI_SCRIPT), "--help"],
    capture_output=True,
    text=True,
    encoding="utf-8",
    errors="replace"
)
```

**Aktualisierte Tests:**
- ✅ `test_help_flag`
- ✅ `test_missing_required_args`
- ✅ `test_invalid_csv_path`
- ✅ `test_fixed_alpha_execution`
- ✅ `test_fit_alpha_execution`
- ✅ `test_frequency_tracking`
- ✅ `test_custom_exponents`
- ✅ `test_negative_v0`
- ✅ `test_mutually_exclusive_alpha`
- ✅ `test_g79_cli_smoke_run`
- ✅ `test_cygx_cli_smoke_run`

---

### 2. **tests/test_print_all_md.py**
**Änderungen:** 1 subprocess.run() Aufruf aktualisiert

```python
# test_no_matching_files - hinzugefügt:
result = subprocess.run(cmd, capture_output=True, text=True, encoding="utf-8", errors="replace")
```

**Status:** ✅ UTF-8-safe

---

### 3. **scripts/tests/data_smoke_fetch.py**
**Änderungen:** Intelligente Planck-Pfad-Erkennung implementiert

**Problem:** 
- Test suchte nur nach `data/raw/planck/{run_id}/planck_map.fits`
- Fiel durch, wenn Datei in `data/raw/planck/planck_map.fits` lag

**Lösung:**
```python
def smoke_paths(run_id: str) -> dict:
    """Return expected paths for autofetch smoke test.
    
    For Planck, tries run-specific path first, then falls back to generic path.
    """
    base = Path("data/raw")
    
    # Check run-specific Planck path first, then generic
    planck_specific = Path(f"data/raw/planck/{run_id}/planck_map.fits")
    planck_generic = Path("data/raw/planck/planck_map.fits")
    
    planck_fits = planck_specific if planck_specific.exists() else planck_generic
    
    return {
        "gaia_parquet": base.parent / "gaia" / run_id / "gaia_quick.parquet",
        "sdss_csv":     base.parent / "sdss" / run_id / "sdss_quick.csv",
        "planck_fits":  planck_fits,  # ← Intelligent path selection
    }
```

**Vorteile:**
- ✅ Prüft zuerst run-spezifischen Pfad
- ✅ Fallback auf generischen Pfad
- ✅ Test schlägt nicht fehl, wenn Datei an einer der beiden Stellen liegt
- ✅ Konsistent mit `run_all_ssz_terminal.py` Logik

---

### 4. **scripts/tests/test_utf8_encoding.py**
**Status:** Bereits UTF-8-optimiert ✅

Dieser Test validiert die UTF-8-Umgebung:
- `test_utf8_environment()` - Prüft ENV-Variablen
- `test_stdout_encoding()` - Prüft stdout Encoding
- `test_utf8_file_write_read()` - Roundtrip-Test
- `test_json_utf8()` - JSON mit Sonderzeichen

**Keine Änderungen nötig** - Test ist bereits auf Windows-Kompatibilität ausgelegt.

---

## 📊 Statistik

### Aktualisierte subprocess.run() Aufrufe:
- **tests/test_segwave_cli.py**: 10 Aufrufe
- **tests/test_print_all_md.py**: 1 Aufruf
- **Gesamt**: 11 subprocess.run() Aufrufe aktualisiert

### Planck-Pfad-Fixes:
- **scripts/tests/data_smoke_fetch.py**: 1 Funktion (`smoke_paths`)
- **run_all_ssz_terminal.py**: 1 Abschnitt (bereits in BUGFIXES dokumentiert)

---

## 🧪 Test-Durchführung

### Alle Tests ausführen:
```bash
# Windows CMD
python -m pytest tests/ -v

# Mit UTF-8 erzwingen
python -X utf8 -m pytest tests/ -v

# Nur CLI-Tests
python -m pytest tests/test_segwave_cli.py -v

# Nur UTF-8-Tests
python -m pytest scripts/tests/test_utf8_encoding.py -v
```

### Smoke-Tests:
```bash
# Data fetch smoke test
python -m pytest scripts/tests/test_data_fetch.py -v

# Planck presence test
python -m pytest scripts/tests/test_data_fetch.py::test_planck_presence -v
```

---

## ✅ Erwartete Ergebnisse

### Vorher (mit Bugs):
```
FAILED tests/test_segwave_cli.py::TestCLIBasic::test_help_flag
  'charmap' codec can't decode byte 0x90

FAILED scripts/tests/test_data_fetch.py::test_planck_presence
  AssertionError: Planck FITS not found
```

### Nachher (gefixt):
```
PASSED tests/test_segwave_cli.py::TestCLIBasic::test_help_flag
PASSED scripts/tests/test_data_fetch.py::test_planck_presence
```

---

## 🔍 Verbleibende Test-Probleme

### 1. test_harmonize_columns_rejects_missing_errors
**Datei:** `scripts/tests/test_gaia_required_columns.py`

**Problem:**
```python
def test_harmonize_columns_rejects_missing_errors():
    df = _base_frame().drop(columns=["pmra_error"])
    with pytest.raises(KeyError):  # ← Erwartet Fehler
        ...
# ABER: Script erstellt fehlende Spalten mit NaN statt Fehler zu werfen
```

**Status:** ⚠️ Design-Frage (Feature vs. Bug)
- **Option A:** Test anpassen (akzeptiert NaN-Erstellung)
- **Option B:** Code anpassen (wirft KeyError bei fehlenden Spalten)

**Priorität:** Niedrig - Nicht kritisch für Produktion

---

## 📝 Best Practices für neue Tests

### 1. Immer UTF-8 Encoding verwenden:
```python
import subprocess

result = subprocess.run(
    cmd,
    capture_output=True,
    text=True,
    encoding="utf-8",      # ← WICHTIG für Windows
    errors="replace"       # ← Verhindert Crashes
)
```

### 2. Dateien mit UTF-8 lesen/schreiben:
```python
# Lesen
content = Path("file.txt").read_text(encoding="utf-8")

# Schreiben
Path("file.txt").write_text(content, encoding="utf-8")

# CSV
df = pd.read_csv("file.csv", encoding="utf-8")
```

### 3. Robuste Pfad-Prüfung:
```python
# Mehrere mögliche Pfade prüfen
paths = [
    Path(f"data/{run_id}/file.fits"),  # Spezifisch
    Path("data/file.fits"),             # Generic
]

for path in paths:
    if path.exists():
        return path

# Oder: Erster existierender Pfad
actual_path = next((p for p in paths if p.exists()), None)
```

---

## 🔗 Verwandte Dokumentation

- `BUGFIXES_2025-10-18.md` - Haupt-Bugfixes (run_all_ssz_terminal.py, ci/)
- `ci/POWERSHELL_CRASH_FIX.md` - PowerShell Extension Probleme
- `ci/README.md` - CI-Suite Dokumentation

---

## ✅ Zusammenfassung

**Alle Test-Dateien sind jetzt:**
- ✅ UTF-8-kompatibel (Windows + Linux)
- ✅ Planck-Pfad-intelligent (run-specific + generic)
- ✅ Fehler-resistent (errors="replace")
- ✅ Konsistent mit Haupt-Scripts

**Tests sollten nun durchlaufen ohne:**
- ❌ 'charmap' codec Fehler
- ❌ Planck-Pfad-Fehler
- ❌ Encoding-Crashes

---

---

## 🌟 NEU: Comprehensive Real Data Test Suite

Siehe: **`REAL_DATA_TESTS_README.md`**

**Neue umfassende Tests mit echten astronomischen Daten:**
- ✅ **test_ssz_real_data_comprehensive.py** (600+ Zeilen)
- ✅ PPN-Parameter mit physikalischer Interpretation
- ✅ Natürliche Grenze für Sonne, Sgr A*, M87*
- ✅ Duale Geschwindigkeiten mit Invarianten-Check
- ✅ Energie-Bedingungen für schwarze Löcher
- ✅ Integration mit `real_data_full.csv`

**Beispiel-Output:**
```
PPN PARAMETER β (Preferred-Frame)
Calculated β:  1.000000000000
GR prediction: 1.000000000000

Physical Interpretation:
  β = 1 → No preferred reference frame
  β = 1 → SSZ matches GR in weak fields
```

**Tests ausführen:**
```bash
pytest tests/test_ssz_real_data_comprehensive.py -v -s
```

---

## Lizenz

Anti-Capitalist Software License (v 1.4)
© 2025 Carmen Wrede, Lino Casu
