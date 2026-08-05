# REPRODUCIBILITY GUIDE

**Generated:** 2025-01-16  
**Purpose:** How to reproduce any run using the run bundle

---

## RUN BUNDLE STRUCTURE

Every calculation creates a run bundle (ZIP) containing:

```
run_YYYYMMDD_HHMMSS_XXXXXX/
├── params.json          # All parameters and constants
├── data_input.csv       # Input data (normalized)
├── results.csv          # Calculation results
├── report.md            # Human-readable summary
├── plots/
│   ├── dilation.png     # Time dilation plot
│   ├── xi.png           # Segment density plot
│   └── redshift.png     # Redshift breakdown
└── errors.log           # (optional) Any errors/warnings
```

---

## PARAMS.JSON CONTENTS

```json
{
  "run_id": "20250116_185047_abc123",
  "timestamp": "2025-01-16T18:50:47",
  "version": "1.0.0",
  "constants": {
    "phi": 1.6180339887498948,
    "G": 6.6743e-11,
    "c": 299792458.0,
    "M_sun_kg": 1.989e30
  },
  "regime_rule": {
    "weak_threshold": 110,
    "strong_threshold": 90,
    "blend_function": "quintic_hermite"
  },
  "method_ids": ["schwarzschild_radius", "xi_auto", "D_ssz", "z_ssz"],
  "input_source": "upload|template|fetch_eso|...",
  "object_count": 10
}
```

---

## REPRODUCING A RUN

### Step 1: Extract Bundle
```bash
unzip run_20250116_185047_abc123.zip
cd run_20250116_185047_abc123/
```

### Step 2: Verify Constants
Check `params.json` matches expected:
- φ = 1.6180339887498948
- G = 6.6743e-11 m³/(kg·s²)
- c = 299792458.0 m/s

### Step 3: Load Input Data
```python
import pandas as pd
df = pd.read_csv("data_input.csv")
```

### Step 4: Run Calculation
```python
from segcalc.methods.core import calculate_all
results = calculate_all(df)
```

### Step 5: Compare Results
```python
original = pd.read_csv("results.csv")
# Compare columns: D_ssz, Xi, z_ssz_total, regime
```

---

## NO LOCAL PATHS IN UI

**Rule:** The UI never displays local filesystem paths.

**Instead:**
- Run ID is displayed (e.g., `20250116_185047_abc123`)
- "Download Run Bundle" button provides ZIP
- All artifacts are inside the bundle

**Verification:**
```bash
grep -r "E:\\" app_v3.py  # Should return nothing
grep -r "C:\\" app_v3.py  # Should return nothing
grep -r "/home/" app_v3.py  # Should return nothing
```

---

## RUN ID FORMAT

```
YYYYMMDD_HHMMSS_XXXXXX

YYYY = Year (4 digits)
MM   = Month (2 digits)
DD   = Day (2 digits)
HH   = Hour (2 digits, 24h)
MM   = Minute (2 digits)
SS   = Second (2 digits)
XXXXXX = Random hex (6 chars)

Example: 20250116_185047_a3f2c1
```

---

## VERIFICATION CHECKLIST

| Item | Expected | Verify Command |
|------|----------|----------------|
| Bundle created | ZIP file | Check file exists |
| params.json | Valid JSON | `python -m json.tool params.json` |
| data_input.csv | Valid CSV | `head data_input.csv` |
| results.csv | Valid CSV | `head results.csv` |
| Plots exist | PNG files | `ls plots/` |
| No local paths | None in UI | Visual inspection |

---

## EXAMPLE WORKFLOW

1. **User clicks "Calculate"** in Single Object tab
2. **System creates run bundle** in temp directory
3. **Run ID displayed** in UI (no path)
4. **Download button** offers ZIP download
5. **User downloads** `run_20250116_185047_abc123.zip`
6. **Bundle contains** all artifacts for reproduction

---

## DATA FLOW

```
User Input (UI)
     ↓
Validation + Normalization
     ↓
Calculate (segcalc methods)
     ↓
Generate Plots
     ↓
Create Bundle (params.json, CSVs, plots)
     ↓
Return Run ID + Download Link
```

---

## CONSTANTS TRACEABILITY

All constants in `params.json` are sourced from:
- `ssz_qubits.py` lines 29-36
- CODATA 2018 for physical constants
- Mathematical definition for φ

**No arbitrary or invented values.**
