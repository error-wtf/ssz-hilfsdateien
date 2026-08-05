# SSZ Complete Analysis Scripts - Reference Guide

**Complete listing of all analysis scripts in the SSZ repository**

© Carmen Wrede & Lino Casu, 2025  
Licensed under the Anti-Capitalist Software License v1.4

**Last Updated:** 2025-10-20

---

## 📋 Table of Contents

1. [Main Analysis Scripts](#main-analysis-scripts)
2. [Physics Validation Tests](#physics-validation-tests)
3. [Production-Ready Tools (NEW)](#production-ready-tools-new---oct-2025)
4. [Data Analysis](#data-analysis)
5. [Visualization](#visualization)
6. [Testing & Validation](#testing--validation)
7. [Utility Scripts](#utility-scripts)

---

## Main Analysis Scripts

### 1. Complete Pipeline
**Script:** `run_all_ssz_terminal.py`  
**Purpose:** Executes complete SSZ analysis pipeline (20+ phases)  
**Runtime:** ~10-15 minutes  
**Output:** Complete validation suite results

```bash
python run_all_ssz_terminal.py
```

### 2. All-in-One Extended Analysis
**Script:** `segspace_all_in_one_extended.py`  
**Purpose:** Comprehensive analysis with paired tests, mass validation, etc.  
**Runtime:** ~3-4 minutes

```bash
python segspace_all_in_one_extended.py all
```

### 3. Theory Calculations
**Script:** `ssz_theory_segmented.py`  
**Purpose:** Core SSZ theory computations (r_φ, Δ(M), mass inversion)  
**Features:** High-precision Decimal arithmetic

```python
from ssz_theory_segmented import rphi_from_mass, delta_percent
```

---

## Physics Validation Tests

### PPN Parameters
**Script:** `test_ppn_exact.py`  
**Validates:** β = γ = 1 (GR compatibility)

```bash
python test_ppn_exact.py
```

### Dual Velocity Invariant
**Script:** `test_vfall_duality.py`  
**Validates:** v_esc × v_fall = c²

```bash
python test_vfall_duality.py --mass Earth --r-mults 1.1,2.0
```

### Energy Conditions
**Script:** `test_energy_conditions.py`  
**Validates:** WEC/DEC/SEC for r ≥ 5r_s

```bash
python test_energy_conditions.py
```

### Continuity Tests
**Scripts:**
- `test_c1_segments.py` - C¹ continuity
- `test_c2_segments_strict.py` - C² strict continuity
- `test_c2_curvature_proxy.py` - C² curvature proxy

### Black Hole Physics
**Scripts:**
- `shadow_predictions_exact.py` - Shadow predictions
- `qnm_eikonal.py` - Quasi-normal modes

### Covariant Formulation
**Script:** `ssz_covariant_smoketest_verbose_lino_casu.py`  
**Validates:** Covariant formulation correctness

---

## Production-Ready Tools (NEW - Oct 2025)

### 1. Rapidity-Based Equilibrium Analysis ⭐⭐⭐
**Script:** [`perfect_equilibrium_analysis.py`](https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results/blob/main/perfect_equilibrium_analysis.py) (428 lines)  
**Purpose:** Demonstrates rapidity formulation for equilibrium points  
**Documentation:** [RAPIDITY_IMPLEMENTATION.md](RAPIDITY_IMPLEMENTATION.md)

```bash
python perfect_equilibrium_analysis.py
```

**Key Features:**
- ✅ Eliminates 0/0 singularities at v_eff → 0
- ✅ Rapidity formulation: χ = arctanh(v/c)
- ✅ Angular bisector for natural origin
- ✅ Expected improvement: 0% → 35-50% at r < 2 r_s

**Core Functions:**
```python
velocity_to_rapidity(v, c)    # NO singularities!
rapidity_to_velocity(chi, c)  # Smooth everywhere
bisector_rapidity(chi1, chi2) # Natural origin
```

### 2. Standalone Interactive Analysis ⭐⭐⭐⭐
**Script:** [`perfect_seg_analysis.py`](https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results/blob/main/perfect_seg_analysis.py) (480 lines)  
**Purpose:** User-friendly standalone tool for custom datasets  
**Documentation:** [PERFECT_SEG_ANALYSIS_GUIDE.md](PERFECT_SEG_ANALYSIS_GUIDE.md)

```bash
# Interactive mode
python perfect_seg_analysis.py --interactive

# Single observation
python perfect_seg_analysis.py --mass 1.0 --radius 10000 --redshift 0.001

# CSV batch
python perfect_seg_analysis.py --csv data.csv --output results.csv
```

**Key Features:**
- ✅ 3 usage modes (Interactive/Single/CSV)
- ✅ Flexible CSV column detection (auto-normalizes)
- ✅ Regime classification (Photon Sphere, Weak Field, etc.)
- ✅ Rapidity-based (NO 0/0!)
- ✅ Production-ready deployment

### 3. Perfect Paired Test Framework ⭐⭐⭐
**Script:** [`perfect_paired_test.py`](https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results/blob/main/perfect_paired_test.py) (470 lines)  
**Purpose:** Complete paired test with ALL findings incorporated  
**Documentation:** [PERFECT_PAIRED_TEST_GUIDE.md](PERFECT_PAIRED_TEST_GUIDE.md)

```bash
python perfect_paired_test.py --csv data/real_data_full.csv --output results.csv
```

**Key Features:**
- ✅ φ-geometry fundamental (not fitting!)
- ✅ Rapidity formulation (NO 0/0!)
- ✅ Regime stratification (Photon Sphere: 82%, High v: 86%)
- ✅ Complete statistics (binomial tests, p-values)
- ✅ Framework ready for full SEG integration

**Incorporated Findings:**
- PAIRED_TEST_ANALYSIS_COMPLETE.md
- STRATIFIED_PAIRED_TEST_RESULTS.md
- PHI_FUNDAMENTAL_GEOMETRY.md
- PHI_CORRECTION_IMPACT_ANALYSIS.md
- [EQUILIBRIUM_RADIUS_SOLUTION.md](https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results/blob/main/EQUILIBRIUM_RADIUS_SOLUTION.md)
- [RAPIDITY_IMPLEMENTATION.md](https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results/blob/main/RAPIDITY_IMPLEMENTATION.md)

---

## Data Analysis

### SegWave Ring Analysis
**Scripts:**
- `segwave_analysis.py` - Multi-ring validation
- `test_segwave_ringmask.py` - Ring mask validation

```bash
python segwave_analysis.py --ring-file data/g79_rings.csv
```

### GAIA Data Analysis
**Scripts:**
- `scripts/data_acquisition/fetch_gaia.py` - GAIA data fetching
- `scripts/data_acquisition/gaia_fetch_via_tap.py` - TAP queries

### Lagrangian Analysis
**Script:** `lagrangian_tests.py`  
**Validates:** Effective potential, ISCO, photon sphere

```bash
python lagrangian_tests.py --object sun
```

---

## Visualization

### Main Plotting Scripts
**Scripts:**
- `generate_key_plots.py` - 5 publication-ready plots (300 DPI)
- `scripts/plot_ssz_maps.py` - SSZ visualization maps
- `scripts/plot_comparison.py` - Model comparison plots

```bash
python generate_key_plots.py
```

**Generated Plots:**
1. `stratified_performance.png` - Performance by regime
2. `phi_geometry_impact.png` - WITH vs WITHOUT φ
3. `winrate_vs_radius.png` - φ/2 boundary validation
4. `stratification_robustness.png` - 3D stratification
5. `performance_heatmap.png` - Comprehensive metrics

---

## Testing & Validation

### Automated Test Suite
**Main Runner:** `run_full_suite.py`  
**Coverage:** 69 tests (35 physics + 23 technical + 11 validation)

```bash
python run_full_suite.py
```

**Pytest Tests:**
```bash
# All tests
pytest tests/ scripts/tests/ -s -v --tb=short

# Specific suites
pytest tests/test_segwave_core.py -s -v
pytest scripts/tests/test_ssz_kernel.py -s -v
```

### Smoke Tests (Quick Health Checks)
**Script:** `smoke_test_all.py`  
**Coverage:** 7 tests (including rapidity validation)  
**Runtime:** ~5 seconds

```bash
python smoke_test_all.py
```

**Tests:**
1. Critical imports
2. φ calculation
3. Data files
4. Output directories
5. Matplotlib
6. Precision
7. Rapidity equilibrium (NEW!)

### Double-Check Validation
**Scripts:**
- `phi_test.py` - φ-lattice BIC validation
- `phi_bic_test.py` - BIC comparison
- `final_validation_findings.py` - Comprehensive validation

---

## Utility Scripts

### Installation & Setup
**Scripts:**
- `install.ps1` / `install.sh` - Complete installation
- `PLATFORM_COMPATIBILITY_CHECK.py` - Platform validation

### Data Fetching
**Scripts:**
- `scripts/fetch_planck.py` - Planck data (2 GB)
- `scripts/data_acquisition/fetch_ned_spectra.py` - NED spectra
- `scripts/data_acquisition/gaia_fetch_via_tap.py` - GAIA TAP

### Output Processing
**Scripts:**
- `scripts/print_all_md.py` - Print all documentation
- `md_to_pdf.py` - Convert MD to PDF
- `echo_md.py` - Echo markdown files

### Stress-Energy Derivation
**Script:** `derive_effective_stress_energy.py`  
**Purpose:** Symbolic stress-energy tensor derivation

---

## Script Categories Summary

| Category | Count | Examples |
|----------|-------|----------|
| **Main Analysis** | 3 | run_all_ssz_terminal, segspace_all_in_one_extended |
| **Physics Tests** | 10 | test_ppn_exact, test_vfall_duality, energy_conditions |
| **Production Tools** | 3 | perfect_equilibrium_analysis, perfect_seg_analysis, perfect_paired_test |
| **Data Analysis** | 5 | segwave_analysis, GAIA fetching, Lagrangian tests |
| **Visualization** | 3 | generate_key_plots, plot_ssz_maps |
| **Testing** | 70+ | pytest suite, smoke tests, validation |
| **Utilities** | 10+ | Installation, data fetching, output processing |

**Total Scripts:** ~100+

---

## Quick Reference

### Most Used Scripts:
```bash
# Complete analysis
python run_all_ssz_terminal.py

# Quick test
python smoke_test_all.py

# Interactive analysis (NEW!)
python perfect_seg_analysis.py --interactive

# Generate plots
python generate_key_plots.py

# Full test suite
python run_full_suite.py
```

### For New Users:
```bash
# 1. Install
./install.sh  # or .\install.ps1 on Windows

# 2. Quick test
python smoke_test_all.py

# 3. Interactive exploration
python perfect_seg_analysis.py --interactive

# 4. Full analysis
python run_all_ssz_terminal.py
```

### For Developers:
```bash
# 1. Run tests
pytest tests/ scripts/tests/ -s -v

# 2. Validate rapidity
python perfect_equilibrium_analysis.py

# 3. Test paired framework
python perfect_paired_test.py --csv data/real_data_full.csv
```

---

## Documentation Links

**Core Guides:**
- [CODE_IMPLEMENTATION_GUIDE.md](docs/CODE_IMPLEMENTATION_GUIDE.md) - Complete code documentation
- [THEORY_AND_CODE_INDEX.md](docs/THEORY_AND_CODE_INDEX.md) - Theory & code index
- [DOCUMENTATION_INDEX.md](DOCUMENTATION_INDEX.md) - All documentation

**New Production Scripts:**
- [RAPIDITY_IMPLEMENTATION.md](RAPIDITY_IMPLEMENTATION.md) - Rapidity solution
- [PERFECT_SEG_ANALYSIS_GUIDE.md](PERFECT_SEG_ANALYSIS_GUIDE.md) - Standalone analysis
- [PERFECT_PAIRED_TEST_GUIDE.md](PERFECT_PAIRED_TEST_GUIDE.md) - Paired test framework

**Pipeline:**
- [SSZ_COMPLETE_PIPELINE.md](SSZ_COMPLETE_PIPELINE.md) - Complete pipeline documentation
- [COMPREHENSIVE_TESTING_GUIDE.md](COMPREHENSIVE_TESTING_GUIDE.md) - Testing guide

---

## Key Scientific Advances (Oct 2025)

**1. Equilibrium Point Treatment:**
- Problem: 0/0 singularity at r < 2 r_s where v_eff → 0
- Solution: Rapidity formulation with angular bisector
- Impact: Expected 0% → 35-50% (p<0.05 achievable!)

**2. φ-Geometry Validation:**
- φ = (1+√5)/2 is FUNDAMENTAL geometric basis
- WITHOUT φ: 0% wins, WITH φ: 51% wins
- Performance peaks at φ/2 boundary (~1.618 r_s)

**3. Regime-Specific Understanding:**
- Photon Sphere (2-3 r_s): 82% wins (DOMINANT!)
- High Velocity (v > 5%c): 86% wins (EXCELLENT!)
- Very Close (r < 2 r_s): Implementation gap (solvable!)
- Weak Field (r > 10 r_s): 37% wins (comparable)

---

**Complete reference for all SSZ analysis scripts! 🔬💻**

© 2025 Carmen Wrede, Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
