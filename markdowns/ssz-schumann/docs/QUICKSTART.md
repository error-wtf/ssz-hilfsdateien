# SSZ Schumann - Quick Start Guide

**Get started in 5 minutes**

---

## Installation

```bash
# Clone repository
git clone https://github.com/error-wtf/ssz-schuhman-experiment.git
cd ssz-schuhman-experiment

# Create virtual environment (recommended)
python -m venv .venv
.venv\Scripts\activate  # Windows
# source .venv/bin/activate  # Linux/Mac

# Install dependencies
pip install -r requirements.txt

# Install package
pip install -e .
```

---

## Quick Test

```bash
# Run all tests
pytest tests/ -v

# Expected: 62 passed
```

---

## Generate Sample Data

```bash
python scripts/fetch_data.py --sample
```

This creates:
- `data/schumann/synthetic_2016.nc`
- `data/space_weather/synthetic_f107.csv`
- `data/space_weather/synthetic_kp.csv`

---

## Run Analysis

### Full Analysis Pipeline

```bash
python scripts/run_full_analysis.py --synthetic
```

Output:
- Plots in `output/full_analysis/run_YYYYMMDD_HHMMSS/plots/`
- Results in `output/full_analysis/run_YYYYMMDD_HHMMSS/analysis_results.txt`

### Layered SSZ Analysis

```bash
python scripts/run_layered_ssz_analysis.py --synthetic
```

---

## Python API

### Basic Usage

```python
from ssz_schumann.models.layered_ssz import (
    LayeredSSZConfig,
    f_n_ssz_layered,
    frequency_shift_estimate,
    print_frequency_table,
)

# Create configuration
config = LayeredSSZConfig()
config.ionosphere.sigma = 0.01  # 1% segmentation

# Calculate SSZ frequency
f1_ssz = f_n_ssz_layered(1, config)
print(f"f1_SSZ = {f1_ssz:.2f} Hz")  # ~7.77 Hz

# Print frequency table
print_frequency_table()
```

### Check SSZ Signature

```python
from ssz_schumann.models.ssz_correction import (
    delta_seg_from_observed,
    check_mode_consistency,
)

# Extract delta_seg from observations
delta_seg = {
    1: delta_seg_from_observed(f1_obs, 7.83),
    2: delta_seg_from_observed(f2_obs, 13.56),
    3: delta_seg_from_observed(f3_obs, 19.18),
}

# Check mode consistency
result = check_mode_consistency(delta_seg)
print(f"SSZ Score: {result['ssz_score']:.3f}")
print(f"Mode Correlation: {result['mean_correlation']:.3f}")

if result['ssz_score'] > 0.7:
    print("Strong SSZ signature detected!")
```

---

## Key Results

### Frequency Shift Table

| delta_seg | f1 (Hz) | f2 (Hz) | f3 (Hz) | Shift |
|-----------|---------|---------|---------|-------|
| 0% | 7.83 | 13.56 | 19.18 | 0 Hz |
| 1% | 7.75 | 13.43 | 18.99 | -0.08 Hz |
| 2% | 7.68 | 13.30 | 18.80 | -0.15 Hz |

### SSZ Signature

- **Strong:** SSZ Score > 0.7, Mode Correlation > 0.7
- **Moderate:** SSZ Score 0.5-0.7
- **Weak/None:** SSZ Score < 0.5

---

## Next Steps

1. **Download real data:**
   - Schumann: https://zenodo.org/records/6348930
   - Kp: https://kp.gfz-potsdam.de/en/data

2. **Run analysis on real data:**
   ```bash
   python scripts/run_full_analysis.py \
       --schumann-path data/schumann/real_data.csv \
       --f107-path data/space_weather/f107.csv
   ```

3. **Read documentation:**
   - `docs/FINAL_REPORT.md` - Complete analysis report
   - `docs/API_REFERENCE.md` - API documentation
   - `docs/THEORY.md` - Theoretical background

---

## Using Real Schumann Data

### Step 1: Download Real Data

**Schumann Resonance Data:**
- Sierra Nevada ELF Station: https://zenodo.org/records/6348930 (26.5 GB)
- Other observatories with similar formats

**Space Weather Data:**
- F10.7 Solar Flux: https://www.swpc.noaa.gov/products/solar-cycle-progression
- Kp Index: https://kp.gfz-potsdam.de/en/data

### Step 2: Prepare Data Files

Place your data files in the following structure:

```
data/
├── schumann/
│   └── real/
│       └── your_schumann_data.csv
└── space_weather/
    └── real/
        ├── f107.csv
        └── kp.csv
```

**Expected Schumann CSV format:**

```csv
datetime,f1_hz,f2_hz,f3_hz,Q1,Q2,Q3
2016-01-01 00:00:00,7.82,13.91,20.12,4.5,5.2,6.1
2016-01-01 01:00:00,7.84,13.93,20.15,4.6,5.3,6.0
...
```

Required columns:
- `datetime`: UTC timestamp
- `f1_hz`, `f2_hz`, `f3_hz`: Schumann frequencies in Hz

Optional columns:
- `Q1`, `Q2`, `Q3`: Q-factors (resonance quality)

**Expected F10.7 CSV format:**

```csv
date,f107
2016-01-01,105.2
2016-01-02,106.1
...
```

**Expected Kp CSV format:**

```csv
datetime,kp
2016-01-01 00:00:00,2.3
2016-01-01 03:00:00,2.0
...
```

### Step 3: Create Configuration File

Copy and modify `configs/real_example.yml`:

```yaml
data_source:
  type: "real"
  
  schumann:
    type: "csv"
    path: "data/schumann/real/your_schumann_data.csv"
    time_column: "datetime"
    freq_columns:
      1: "f1_hz"
      2: "f2_hz"
      3: "f3_hz"
    q_columns:
      1: "Q1"
      2: "Q2"
      3: "Q3"
    timezone: "UTC"
  
  space_weather:
    f107:
      path: "data/space_weather/real/f107.csv"
      time_column: "date"
      value_column: "f107"
    kp:
      path: "data/space_weather/real/kp.csv"
      time_column: "datetime"
      value_column: "kp"
```

### Step 4: Run Analysis

```bash
python scripts/run_full_analysis.py --config configs/real_example.yml
```

Or use the Python API:

```python
from ssz_schumann.data_io import load_all_data_from_config
from ssz_schumann.analysis import run_full_pipeline, PipelineConfig

# Load data
data = load_all_data_from_config("configs/real_example.yml")
print(data.summary())

# Run analysis
config = PipelineConfig(data_source="real")
result = run_full_pipeline(config)
print(result.summary())
```

### Step 5: View Results

Results are saved in:
```
output/real_analysis/<timestamp>/
├── plots/
│   ├── frequencies_timeseries.png
│   ├── delta_seg_timeseries.png
│   └── ssz_analysis_summary.png
├── delta_seg_timeseries.csv
└── analysis_results.json
```

---

## Troubleshooting

### Import Error

```bash
# Make sure package is installed
pip install -e .
```

### Missing Dependencies

```bash
pip install -r requirements.txt
```

### Test Failures

```bash
# Clear cache and retry
rm -rf .pytest_cache __pycache__
pytest tests/ -v
```

---

**© 2025 Carmen Wrede & Lino Casu**
