# SSZ Schumann Experiment - Quickstart

## Prerequisites

- Python 3.8+
- Required packages: `numpy`, `pandas`, `scipy`, `matplotlib`
- Zenodo Schumann data (already downloaded in `data/schumann/real/raw/`)

## Quick Start (End-to-End Real Data Analysis)

### 1. Extract Schumann Frequencies from Raw Data

```bash
python scripts/process_one_month.py
```

This processes the October 2013 data and creates:
- `data/schumann/real/processed/schumann_1310_processed.csv`

### 2. Generate Space Weather Proxies

```bash
python scripts/create_historical_proxies.py
```

Creates reconstructed F10.7 and Kp data from published monthly averages.

### 3. Run Real Data Analysis

```bash
# With fixed eta = 0.74
python scripts/run_ssz_schumann_realdata.py --station sierra_nevada --year 2013 --month 10

# With fitted eta
python scripts/run_ssz_schumann_realdata.py --station sierra_nevada --year 2013 --month 10 --fit-eta
```

### 4. Generate Plots

```bash
python scripts/plot_ssz_schumann_realdata.py --station sierra_nevada --year 2013 --month 10
```

### 5. View Results

Output files in `output/`:
- `ssz_schumann_realdata_results.json` - Complete results (JSON)
- `ssz_realdata_timeseries.png` - Frequency time series
- `ssz_realdata_deltas.png` - Per-mode delta comparison
- `ssz_realdata_diurnal.png` - Diurnal variation
- `ssz_realdata_summary.png` - SSZ test summary

## Expected Results (from actual runs)

With October 2013 data (744 hours):

| Metric | Value (eta=0.74) | Value (eta fitted) |
|--------|------------------|-------------------|
| delta_SSZ_global | -9.47% | -0.00% |
| chi^2/ndof | 55.36 | 55.36 |
| p-value | < 10^-4 | < 10^-4 |
| Mode spread | 3.17% | 2.90% |
| **Result** | **REJECTED** | **REJECTED** |

**Conclusion:** SSZ Minimalmodel rejected. Classical ionospheric dispersion dominates.

## Data Sources

| Data | Source | Status |
|------|--------|--------|
| Schumann | Zenodo doi:10.5281/zenodo.7761644 | REAL |
| F10.7 | NOAA monthly averages | RECONSTRUCTED |
| Kp | GFZ monthly averages | RECONSTRUCTED |

## Help

```bash
python scripts/run_ssz_schumann_realdata.py --help
python scripts/plot_ssz_schumann_realdata.py --help
```

---

*For detailed analysis, see SSZ_SCHUMANN_REALDATA_REPORT.md*
