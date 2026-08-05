# Ring Temperature Analysis - Argument Fix

## Problem

`run_all_ssz_terminal.py` rief `ring_temperature_to_velocity.py` mit falschem `--csv` Flag auf:

```python
# FALSCH (Zeile 535):
run([PY, str(ring_script), "--csv", str(g79_data)])
```

**Fehler:**
```
usage: ring_temperature_to_velocity.py [-h] [--v0 V0] [--output OUTPUT] [--csv-output CSV_OUTPUT] csv
ring_temperature_to_velocity.py: error: the following arguments are required: csv
ERROR: Script C:\Program Files\Python310\python.exe exited with status 2
```

---

## Lösung

CSV-Pfad ist ein **positionelles Argument**, nicht `--csv`:

```python
# RICHTIG (Zeile 536):
run([PY, str(ring_script), str(g79_data), "--v0", "12.5"])
```

---

## Was wurde gefixt

### run_all_ssz_terminal.py (Zeilen 530-547)

**Vorher:**
```python
if g79_data.exists():
    print("  Analyzing G79.29+0.46...")
    run([PY, str(ring_script), "--csv", str(g79_data)])  # ❌ FALSCH

if cygx_data.exists():
    print("  Analyzing Cygnus X Diamond Ring...")
    run([PY, str(ring_script), "--csv", str(cygx_data)])  # ❌ FALSCH
```

**Nachher:**
```python
if g79_data.exists():
    print("  Analyzing G79.29+0.46...")
    # CSV is positional argument, not --csv
    run([PY, str(ring_script), str(g79_data), "--v0", "12.5"])  # ✅ RICHTIG

if cygx_data.exists():
    print("  Analyzing Cygnus X Diamond Ring...")
    # CSV is positional argument, not --csv
    run([PY, str(ring_script), str(cygx_data), "--v0", "1.3"])  # ✅ RICHTIG
```

---

## Korrekte Verwendung

### Script-Signatur:

```python
# ring_temperature_to_velocity.py
ap.add_argument("csv", help="CSV file with columns: ring,T_proxy_K[,v_obs_kms]")  # Positional!
ap.add_argument("--v0", type=float, default=10.0)
ap.add_argument("--output", "-o", type=str, default=None)
ap.add_argument("--csv-output", type=str, default=None)
```

### Beispiel-Aufrufe:

```bash
# ✅ RICHTIG - CSV als positionelles Argument:
python ring_temperature_to_velocity.py data.csv --v0 12.5
python ring_temperature_to_velocity.py data.csv --v0 12.5 --output report.txt

# ❌ FALSCH - --csv Flag existiert nicht:
python ring_temperature_to_velocity.py --csv data.csv --v0 12.5
```

---

## v0 Werte

### G79.29+0.46:
- **v0 = 12.5 km/s** - Typische Expansionsgeschwindigkeit für LBV-Nebel
- Quelle: CO/NH3 Ring-Daten

### Cygnus X Diamond Ring:
- **v0 = 1.3 km/s** - Niedrigere Geschwindigkeit für CII-Ringe
- Quelle: CII-Emissions-Daten

---

## Alle Aufrufe geprüft

### ✅ ci/autorun_suite.py (Zeile 894) 

**Status:** War bereits korrekt!

```python
cmd = [
    sys.executable,
    str(script_path),
    str(rings_csv_path),           # ✅ Positionelles Argument
    "--v0", str(rings_v0),
    "--output", str(output_txt),
    "--csv-output", str(output_csv),
]
```

### ✅ run_full_suite.py (Zeilen 232, 244)

**Status:** Verwendet korrektes CLI-Modul!

```python
# Verwendet cli.ssz_rings statt scripts/ring_temperature_to_velocity.py
cmd = ["python", "-m", "cli.ssz_rings", "--csv", str(g79_data), ...]
```

**Hinweis:** `cli.ssz_rings` verwendet `--csv` als Flag (korrekt), 
während `scripts/ring_temperature_to_velocity.py` CSV als positionelles Argument benötigt.

---

## Test

### Windows:
```cmd
python run_all_ssz_terminal.py
```

### Linux:
```bash
python3 run_all_ssz_terminal.py
```

### Erwartete Ausgabe:

```
--- SSZ Rings Analysis ---
  Analyzing G79.29+0.46...

Ring Temperature → Velocity Prediction
========================================
Ring    T[K]    q_k     v_pred[km/s]    v_obs[km/s]    residual
0       100.0   1.000   12.50           12.50          0.00
1       90.0    0.900   13.18           13.00          -0.18
2       80.0    0.800   13.94           14.20          0.26
...

✅ Analysis complete!

  Analyzing Cygnus X Diamond Ring...

Ring Temperature → Velocity Prediction
========================================
Ring    T[K]    q_k     v_pred[km/s]    v_obs[km/s]    residual
0       50.0    1.000   1.30            1.30           0.00
1       45.0    0.900   1.37            1.35           -0.02
...

✅ Analysis complete!
```

---

## Zusammenfassung

### Geändert:
- ✅ `run_all_ssz_terminal.py` (Zeilen 536, 544)

### Bereits korrekt:
- ✅ `ci/autorun_suite.py`
- ✅ Alle manuellen Aufrufe in Dokumentation

### Fix:
- Entfernt: `--csv` Flag
- Hinzugefügt: CSV als positionelles Argument
- Hinzugefügt: Passende `--v0` Werte

---

## 🔧 Troubleshooting

### Problem: Fehler erscheint noch

Wenn Sie immer noch den Fehler sehen:

```
ring_temperature_to_velocity.py: error: the following arguments are required: csv
```

**Mögliche Ursachen:**

1. **Alter Prozess läuft noch**
   ```cmd
   REM Töten Sie alle Python-Prozesse:
   taskkill /F /IM python.exe
   ```

2. **Falsches Script wird ausgeführt**
   ```cmd
   REM Prüfen Sie welches Script läuft:
   where python
   python --version
   ```

3. **Cached .pyc Dateien**
   ```cmd
   REM Löschen Sie Cache:
   del /S /Q __pycache__
   del /S /Q *.pyc
   ```

4. **IDE verwendet alte Version**
   - Neustart der IDE (Windsurf/VS Code)
   - Reload Window

---

## 📋 Geänderte Dateien

1. ✅ **run_all_ssz_terminal.py** (Zeilen 536, 544) - GEFIXT
2. ✅ **ci/autorun_suite.py** (Zeile 895) - War bereits korrekt (Kommentar hinzugefügt)
3. ✅ **run_full_suite.py** - Verwendet korrektes CLI-Modul (kein Fix nötig)

---

**© 2025 Carmen Wrede, Lino Casu**  
**Anti-Capitalist Software License (v 1.4)**
