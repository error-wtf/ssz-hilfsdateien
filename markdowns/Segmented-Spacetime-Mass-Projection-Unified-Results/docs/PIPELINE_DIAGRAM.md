# SSZ Pipeline Architecture

**Complete workflow from data acquisition to scientific results**

---

## 📊 Visual Pipeline Overview

```mermaid
graph TB
    subgraph "Data Sources"
        A1[GAIA DR3<br/>Stellar Data]
        A2[NED Database<br/>Galaxy Spectra]
        A3[Planck CMB<br/>Cosmology]
        A4[Local Observations<br/>Custom Data]
    end
    
    subgraph "Data Acquisition & Validation"
        B1[fetch_gaia.py<br/>Query & Download]
        B2[integrate_ned_spectrum.py<br/>Spectrum Integration]
        B3[fetch_planck.py<br/>CMB Data 2GB]
        B4[validate_dataset.py<br/>Quality Checks]
    end
    
    subgraph "Data Storage"
        C1[data/real_data_full.csv<br/>427 objects]
        C2[data/gaia/<br/>Stellar positions]
        C3[data/planck/<br/>CMB spectra]
        C4[data/observations/<br/>Multi-ring data]
    end
    
    subgraph "Core SSZ Engine"
        D1[SSZ Model<br/>φ-based geometry]
        D2[Mass Projection<br/>Segmented kernel]
        D3[Temporal Evolution<br/>φ^(-α·N)]
        D4[Metric Solver<br/>Field equations]
    end
    
    subgraph "Analysis Pipelines"
        E1[segspace_enhanced.py<br/>Main Analysis]
        E2[test_ppn_exact.py<br/>PPN Tests]
        E3[shadow_predictions.py<br/>Black Hole Tests]
        E4[phi_test.py<br/>φ Validation]
    end
    
    subgraph "Tests & Validation"
        F1[35 Physics Tests<br/>PPN, Energy, Limits]
        F2[34 Technical Tests<br/>UTF-8, Platform]
        F3[Multi-Ring Tests<br/>G79, Cygnus X]
    end
    
    subgraph "Results & Outputs"
        G1[out/<br/>CSV Results]
        G2[reports/<br/>Test Summaries]
        G3[Plots & Figures<br/>Visualizations]
        G4[Scientific Papers<br/>32 Documents]
    end
    
    A1 --> B1
    A2 --> B2
    A3 --> B3
    A4 --> B4
    
    B1 --> C2
    B2 --> C1
    B3 --> C3
    B4 --> C4
    
    C1 --> D1
    C2 --> D1
    C3 --> D3
    C4 --> D2
    
    D1 --> E1
    D2 --> E1
    D3 --> E2
    D4 --> E3
    
    E1 --> F1
    E2 --> F1
    E3 --> F2
    E4 --> F3
    
    F1 --> G1
    F2 --> G2
    F3 --> G3
    G1 --> G4
    G2 --> G4
    
    style A1 fill:#e1f5ff
    style A2 fill:#e1f5ff
    style A3 fill:#e1f5ff
    style A4 fill:#e1f5ff
    
    style D1 fill:#ffe1e1
    style D2 fill:#ffe1e1
    style D3 fill:#ffe1e1
    style D4 fill:#ffe1e1
    
    style G1 fill:#e1ffe1
    style G2 fill:#e1ffe1
    style G3 fill:#e1ffe1
    style G4 fill:#e1ffe1
```

---

## 🔄 Detailed Workflow

### Phase 1: Data Acquisition (10-30 min)

**Input:** Data source URLs, query parameters  
**Process:**
1. Query GAIA DR3 for stellar data
2. Fetch NED spectra for galaxies  
3. Download Planck CMB data (if missing)
4. Validate all datasets

**Output:** `data/real_data_full.csv` (427 objects)

**Key Files:**
- `scripts/data_acquisition/fetch_gaia.py`
- `scripts/data_generators/integrate_ned_spectrum.py`
- `scripts/fetch_planck.py`

---

### Phase 2: Data Preprocessing (5-10 min)

**Input:** Raw CSV data  
**Process:**
1. Column validation (7 critical columns)
2. Unit conversions (SI units)
3. Calculate derived quantities (z, r_emit, etc.)
4. Handle NaN patterns (acceptable vs fatal)

**Output:** Validated, preprocessed datasets

**Key Files:**
- `scripts/data_generators/validate_dataset.py`
- `core/preprocessing.py`

---

### Phase 3: SSZ Model Computation (30-60 min)

**Input:** Preprocessed data + model parameters  
**Process:**
1. Initialize φ-based segment field: N(x) = Σ γᵢ·Kᵢ(x)
2. Solve metric: g_μν = diag(-e^Φ, e^Λ, r², r²sin²θ)
3. Calculate time dilation: τ = φ^(-α·N(x))
4. Compute observables (redshift, velocities, etc.)

**Output:** `out/phi_step_debug_full.csv`, `out/_enhanced_debug.csv`

**Key Files:**
- `segspace_enhanced_test_better_final.py`
- `core/ssz_model.py`
- `core/segments.py`

---

### Phase 4: Analysis & Testing (1-2 hours)

**Input:** Model outputs  
**Process:**
1. **Physics Tests (35):**
   - PPN parameters (β, γ)
   - Energy conditions (WEC, DEC, SEC)
   - Dual velocity invariant
   - Shadow predictions
   - φ-based tests

2. **Technical Tests (34):**
   - UTF-8 encoding
   - Platform compatibility
   - CLI arguments
   - Data integrity

3. **Validation Tests (11):**
   - Multi-ring structures (G79, Cygnus X)
   - Ring completeness
   - Growth statistics

**Output:** `reports/summary-output.md`, test logs

**Key Files:**
- `run_full_suite.py` (orchestrates all tests)
- `tests/test_ppn_exact.py`
- `tests/test_energy_conditions.py`
- `tests/test_vfall_duality.py`
- `scripts/tests/test_ssz_kernel.py`

---

### Phase 5: Visualization & Reporting (15-30 min)

**Input:** Test results + model outputs  
**Process:**
1. Generate plots (r_φ vs mass, redshift comparison, etc.)
2. Create summary tables
3. Export results to CSV
4. Generate markdown reports

**Output:** Figures, summary reports, papers

**Key Files:**
- `scripts/plotting/plot_results.py`
- `SUMMARY_PIPELINE_README.md`

---

## ⚙️ Command-Line Execution

### Full Pipeline (All Phases)
```bash
# Windows
.\install.ps1

# Linux/macOS/WSL
./install.sh

# Takes ~10 minutes total
```

### Individual Phases

**Phase 1 - Data Acquisition:**
```bash
python scripts/data_acquisition/fetch_gaia.py --cone "RA DEC radius"
python scripts/data_generators/integrate_ned_spectrum.py --validate
```

**Phase 3 - SSZ Model:**
```bash
python segspace_enhanced_test_better_final.py
```

**Phase 4 - Tests:**
```bash
python run_full_suite.py
# Or individual test:
python tests/test_ppn_exact.py
```

**Phase 5 - Reports:**
```bash
python scripts/tools/generate_summary.py
```

---

## 📁 Key Directories

```
SSZ-Repository/
├── data/                    # All datasets
│   ├── real_data_full.csv  # Main dataset (427 objects)
│   ├── gaia/               # GAIA stellar data
│   ├── planck/             # CMB spectra (2GB)
│   └── observations/       # Multi-ring data
│
├── core/                    # SSZ model implementation
│   ├── ssz_model.py        # Main model
│   ├── segments.py         # Segment calculations
│   └── metrics.py          # Metric solver
│
├── tests/                   # Test suites
│   ├── test_ppn_exact.py   # PPN validation
│   ├── test_energy_conditions.py
│   └── test_vfall_duality.py
│
├── scripts/                 # Utilities
│   ├── data_acquisition/   # Data fetching
│   ├── analysis/           # Analysis tools
│   └── tests/              # Script tests
│
├── out/                     # Model outputs
│   ├── phi_step_debug_full.csv
│   └── _enhanced_debug.csv
│
├── reports/                 # Test reports
│   └── summary-output.md   # Complete log
│
└── papers/                  # Scientific papers
    ├── validation/         # 11 validation papers
    └── theory/             # 21 theory papers
```

---

## 🎯 Key Performance Metrics

| Phase | Duration | Output Size | CPU Usage |
|-------|----------|-------------|-----------|
| Data Acquisition | 10-30 min | ~5 MB | Low |
| Preprocessing | 5-10 min | ~10 MB | Low |
| SSZ Computation | 30-60 min | ~50 MB | High |
| Testing | 1-2 hours | ~100 MB | Medium |
| Reporting | 15-30 min | ~20 MB | Low |
| **Total** | **~2-4 hours** | **~200 MB** | **Variable** |

**Hardware Requirements:**
- RAM: 4 GB minimum, 8 GB recommended
- Storage: 3 GB (including Planck data)
- CPU: Multi-core recommended for tests

---

## 🔬 Scientific Workflow Integration

```
Research Question
      ↓
   Data Selection → GAIA/NED Query
      ↓
   SSZ Model Run → φ-based calculations
      ↓
   Validation → 69 automated tests
      ↓
   Analysis → Statistical evaluation
      ↓
   Paper → 32 documents available
```

---

## 🚀 Quick Commands

**Complete Pipeline:**
```bash
python run_full_suite.py
```

**Data Only:**
```bash
python scripts/fetch_planck.py
```

**Tests Only:**
```bash
pytest tests/ -v
```

**Custom Analysis:**
```bash
python segspace_enhanced_test_better_final.py --object "M87"
```

---

© 2025 Carmen Wrede & Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
