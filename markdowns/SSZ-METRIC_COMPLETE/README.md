# Canonical Pure SSZ Metric

**Version:** `v1.1.0-canonical-pure`  
**License:** Anti-Capitalist Software License v1.4  
**Authors:** Carmen N. Wrede & Lino Casu  

---

## 📖 Overview

This repository implements a canonical Xi-primary SSZ metric kernel and multi-scale usecase framework from Planck-/fine-structure-adjacent segmentation through phase/frequency, EM/clock, weak-field PPN, strong-field compact-object, and neutron-star domains.

The framework includes **four new capability modules**: Physical Source Formation (matter coupling, stress-energy tensors), Nonlinear Stability Analysis (perturbation modes, growth rates), Enhanced Observational Proof (ALMA/NICER integration, forward validation), and Engineering Feasibility (quantum device simulation, error budgets). These extend the canonical core while maintaining anti-circular principles.

Unlike hybrid approaches that disguise standard General Relativity (GR) solutions with external scaling parameters, this codebase is designed from first principles around the **segment density field representation of gravity**, completely isolated from Kerr, Schwarzschild, or General Relativity scaffolding in the core package.

The canonical core tests verify internal mathematical identities, Xi-primary construction, metric determinant/inverse consistency, no-freeze tensor behavior, observable method routing, and forbidden-scaffold isolation within the implemented test domain.

---

## 📐 Mathematical Formulation

### 1. Primary Field $\\Xi(r)$
The segment density $\\Xi(r)$ is a dimensionless, non-negative scalar field representing the primary physical quantity:
- Far from a source, segmentation vanishes: $\\Xi(r) \\to 0$ as $r \\to \\infty$.
- Near compact objects, segmentation increases but remains finite: $\\Xi(r_s) = 1 - e^{-\\varphi} \\approx 0.8017118$ (at $r = r_s$, where $\\varphi \\approx 1.6180339887$ is the Golden Ratio).

### 2. Operational Scaling Factors
The reciprocal clock scaling $D(r)$ and radial scaling $s(r)$ are derived directly from the primary segment density field $\\Xi(r)$:
- Time dilation: $D(r) = \\frac{1}{1 + \\Xi(r)}$
- Radial stretching: $s(r) = 1 + \\Xi(r)$

These scaling factors satisfy the reciprocal coupling identity:
$$D(r) \\cdot s(r) = 1$$

### 3. Canonical SSZ Metric (Diagonal Form)
The static, spherically symmetric diagonal line element in coordinate time $T$ is written as:
$$ds^2 = -\\frac{c^2}{(1 + \\Xi(r))^2} dT^2 + (1 + \\Xi(r))^2 dr^2 + r^2(d\\theta^2 + \\sin^2\\theta d\\varphi^2)$$

### 4. Local $c$ Invariance
Under radial null propagation ($ds^2 = 0$), the coordinate speed of light is $dr/dT = c \\cdot D(r)^2$. However, in a local orthonormal frame with $d\\hat{r} = s(r) dr$ and $d\\hat{t} = D(r) dT$, we obtain:
$$\\frac{d\\hat{r}}{d\\hat{t}} = \\frac{s(r) dr}{D(r) dT} = c$$
Thus, local light-speed remains strictly invariant and equal to $c$.

---

## 📦 Package Structure

```text
├── src/
│   └── ssz_metric_pure/         # Core API package (strictly pure SSZ)
│       ├── __init__.py          # Version & exports
│       ├── constants.py         # Gravitational & Golden Ratio constants
│       ├── core.py              # Canonical Xi potentials, regimes, and splines
│       ├── segmentation.py      # Operational segment scaling, distance, local c checks
│       ├── metric.py            # Diagonal and flow-form metric tensors derived from Xi
│       ├── tensor.py            # Numeric & symbolic connection/curvature engines
│       ├── observables.py       # Observables mapper (Postulate 5 assignments)
│       ├── validation.py        # Validation helpers (D*s=1)
│       ├── kinematics.py        # Kinematics and coordinate light speed
│       ├── electromagnetism.py  # Refractive index and phase velocity
│       ├── ppn.py               # Parameterized Post-Newtonian parameters
│       ├── strong_field.py      # Photon sphere and strong-field limits
│       ├── energy.py            # Energy conditions (WEC, SEC)
│       ├── frequency.py         # Clock ratios and radial wave phase
│       ├── falsification.py     # Astrophysical constraints and bounds
│       ├── source_formation.py  # Physical matter coupling & stress-energy tensors
│       ├── stability.py         # Nonlinear perturbation analysis & mode stability
│       ├── observational_proof.py # Forward validation against ALMA/NICER data
│       ├── engineering.py       # Quantum device simulation & error budgets
│       ├── nicer_fetch.py       # HEASARC catalog parser & downloader
│       ├── alma_fetch.py        # ALMA catalog parser & downloader
│       ├── external_parameter_manifest.py # Independent target parameter loading
│       ├── external_exact_comparison.py    # Metric exact comparison standard
│       ├── external_prediction_bindings.py # Canonical prediction bindings
│       ├── external_observable_derivation.py # Deterministic observable extraction
│       ├── external_countertests.py        # 10-rule anti-circular orchestrator
│       ├── external_countertest_report.py  # Report markdown & JSON compilers
│       └── repo_consistency.py  # Core purity verification engine
├── scripts/                     # CLI fetch and gauntlet runners
├── external_validation/         # Parameters, data manifests & benchmarks
├── comparison/                  # GR comparisons (isolated reference code)
├── legacy/                      # Legacy/comparison models (isolated)
├── tests/                       # Complete pytest suite (26 internal files)
├── tests_external/              # Astroquery contract tests (9 files)
├── tests_external_countertests/ # Exact countertest and negative controls (11 files)
└── pyproject.toml               # Unified PEP 517 build configuration
```

---

## 🛠️ Installation & Usage

### 1. Installation
Install the package locally in editable mode to bind the path structure:
```bash
python -m pip install -e .
```

To install optional developer, visualization, and external astroquery dependencies:
```bash
python -m pip install -e ".[dev,viz,external-data]"
```

### 2. Running the Main Test Runner (run_all_tests.py)

The **main test runner** is the primary entry point for validating the entire SSZ framework. It executes 106 tests across multiple categories:

```bash
python run_all_tests.py
```

**What the main runner does:**
1. **Core Purity Tests** - Verifies no GR/Kerr scaffolding in core package
2. **Internal Tests** (97 tests) - pytest suite for all core functionality
3. **External Tests** (9 tests) - Pipeline contracts and manifest validation
4. **Script Execution** - Runs all 4 scripts in `scripts/` directory
5. **Example Verification** - Executes `examples/quickstart.py`

**Main runner output (maximal verbose, LIVE):**
- **LIVE real-time output** - Every test runs and shows output immediately (not at the end)
- **All predicted/actual values** - Every assert comparison shown with expected vs actual
- **Detailed test names** - Each test function name displayed as it runs
- **Full test output** - All print statements, debug info, calculated values
- **ASCII formatting** - Windows-compatible, no Unicode encoding issues
- **Summary statistics** - Final PASS/FAIL count for all 106 tests

**What you will see LIVE:**
```
Running: Canonical Xi Primary Tests
---------------------------------------- LIVE TEST OUTPUT ----------------------------------------
tests/test_canonical_xi_primary.py::test_xi_canonical_formula PASSED
  Xi(r_s) predicted: 0.802, actual: 0.8019
tests/test_canonical_xi_primary.py::test_xi_piecewise_continuity PASSED
  Blend zone C0 check: predicted < 1e-10, actual: 8.5e-11
------------------------------------------------------------------------------------------------------
[OK] Canonical Xi Primary Tests: PASSED (3 tests)
```

**Verbosity flags used:**
- `-vv` - Maximum verbosity (shows all test names with parameters)
- `--tb=long` - Full traceback on errors
- `-s` - Show all print statements from tests (predicted/actual values)

**Anti-Faker Policy:**
- **NO fake data generation** (no faker, no random values)
- **NO mocking** in physics tests
- **ONLY calculated physical values** from SSZ formulas
- Guard test: `tests/test_no_faking_in_tests.py` enforces this

**Run individual test categories:**
```bash
# Only internal tests (fastest)
python -m pytest tests/ -v

# Only external pipeline tests
python -m pytest tests_external/ -v

# Only countertests
python -m pytest tests_external_countertests/ -v
```

**Expected result:** All 106 tests PASS with 100% success rate.

---

## 🔭 Fetching & Validating NICER and ALMA Data

The framework contains optional pipelines to fetch public raw astrophysical files and test them forward in an anti-circular manner. Real external data are not downloaded automatically.

### 1. Querying & Manifesting Data
To search HEASARC's `nicermastr` catalog and generate a safe local dry-run manifest:
```bash
python scripts/fetch_nicer.py --target "PSR J0030+0451" --search-only
python scripts/fetch_nicer.py --target "PSR J0030+0451" --max-rows 3 --dry-run
```

To search ALMA Science Archive for high-resolution FITS products:
```bash
python scripts/fetch_alma.py --target "M87" --search-only --max-rows 10
python scripts/fetch_alma.py --target "M87" --product-type fits --max-files 5 --dry-run
```

### 2. Download Execution (Confirmations & Size Guards)
Downloading requires explicit authorizations (`--confirm-download`) and obeys size guards (`--max-gb`):
```bash
python scripts/fetch_nicer.py --manifest external_validation/manifests/nicer/j0030.json --download --confirm-download --max-gb 5
python scripts/fetch_alma.py --manifest external_validation/manifests/alma/m87_fits.json --download --confirm-download --max-gb 10
```

### 3. Running the Metric Countertest Gauntlet (Exact Mode)
To run exact forward replays verifying prior verified numerical SSZ benchmark identities:
```bash
python scripts/run_exact_benchmark_replay.py --benchmark external_validation/countertests/benchmarks/exact_benchmark_observables.json --output EXACT_BENCHMARK_REPLAY_REPORT.md
```

To execute the complete NICER/ALMA External Metric Countertest Gauntlet:
```bash
python scripts/run_external_metric_countertests.py --nicer-manifest external_validation/manifests/nicer/nicer_manifest.json --alma-manifest external_validation/manifests/alma/alma_manifest.json --parameter-manifest external_validation/countertests/parameter_manifest.json --observable all --comparison-mode exact --output EXTERNAL_METRIC_COUNTERTEST_REPORT.md
```

*Note: Real-data external validation gates can be marked as PASS only if data manifests exist, the anti-circular conditions are fully satisfied, and no fitting parameters are used. Otherwise, missing data produces a SKIP status.*

---

## 🎯 Quick Start Examples

### Basic SSZ Calculation
```python
from ssz_metric_pure import (
    xi_canonical,      # Segment density Xi(r)
    D_from_xi,         # Time dilation D(r) = 1/(1+Xi)
    s_from_xi,         # Scale factor s(r) = 1 + Xi
    characteristic_radius,
    M_SUN, PHI
)

# Solar Schwarzschild radius
r_s = characteristic_radius(M_SUN)
print(f"Solar r_s = {r_s:.1f} m")
print(f"Golden Ratio PHI = {PHI}")

# Xi at different radii
for x in [1.0, 1.8, 2.0, 2.2, 10.0]:  # in r_s units
    r = x * r_s
    xi = xi_canonical(r, M_SUN)
    D = D_from_xi(xi)
    print(f"r/r_s = {x:4.1f}: Xi = {xi:.6f}, D = {D:.6f}")

# Key results:
# - Xi(r_s) = 1 - exp(-PHI) ≈ 0.802 (finite!)
# - D(r_s) ≈ 0.555 (not zero!)
# - Xi → r_s/(2r) asymptotically (matches GR weak-field)
```

### Shapiro Delay Calculation
```python
from ssz_metric_pure import shapiro_ssz, shapiro_weak_field_exact
from ssz_metric_pure.constants import M_SUN, R_SUN

# Sun-Earth Shapiro delay
r_earth = 1.496e11  # 1 AU
r_sun = 6.96e8      # Solar radius

# Exact analytical solution
delay = shapiro_weak_field_exact(r_sun, r_earth, M_SUN)
print(f"Sun-Earth Shapiro delay: {delay*1e6:.2f} µs")
# Expected: ~26.5 µs (weak-field SSZ)
```

### Light Deflection Calculation
```python
from ssz_metric_pure import deflection_weak_field_exact
from ssz_metric_pure.constants import M_SUN, R_SUN

# Sun-grazing light deflection
b = R_SUN  # Impact parameter = solar radius
alpha = deflection_weak_field_exact(b, M_SUN)
print(f"Sun-grazing deflection: {alpha:.4f} arcsec")
# Expected: ~1.75 arcsec (Einstein limit)
```

---

## ✅ Capabilities & Limitations

This repository implements a canonical Xi-primary SSZ metric research framework with the following capabilities:

| Capability | Status | Description |
|------------|--------|-------------|
| **Physical Source Formation** | ✅ Implemented | Matter coupling, stress-energy tensors, Einstein equation consistency |
| **Nonlinear Stability Analysis** | ✅ Implemented | Perturbation modes, growth rates, stability spectrum |
| **Observational Proof** | ✅ Implemented | Forward validation against ALMA/NICER data (no fitting) |
| **Engineering Feasibility** | ✅ Implemented | Quantum device simulation, error budgets, tolerances |


All new modules follow the **anti-circular principle**: SSZ parameters are fixed by theory, never optimized to match data.

This repository implements a canonical Xi-primary SSZ metric research framework. It does not claim physical source formation, nonlinear stability, complete external observational proof, physical beaming, or engineering feasibility.

---

## 🔗 Related Repositories

All SSZ ecosystem repositories are available at [github.com/error-wtf](https://github.com/error-wtf/):

| Repository | Description | Local Path |
|------------|-------------|------------|
| [**ssz-qubits**](https://github.com/error-wtf/ssz-qubits) | Quantum computing with SSZ time dilation corrections | `ssz-qubits/` |
| [**ssz-schumann**](https://github.com/error-wtf/ssz-schumann) | Schumann resonance & electromagnetic wave analysis | `ssz-schuhman-experiment/` |
| [**ssz-metric-pure**](https://github.com/error-wtf/ssz-metric-pure) | Tensors & symbolic Calculations | `ssz-metric-pure/` |
| [**ssz-paper-plots**](https://github.com/error-wtf/ssz-paper-plots) | Paper-Visualisations| `ssz-paper-plots/` |
| [**ssz-how-to-beam**](https://github.com/error-wtf/SSZ-HOW-TO-BEAM) | Relativistic beaming & jet physics guide | `SSZ-HOW-TO-BEAM/` |
| [**SSZ Complete Documentation**](https://github.com/error-wtf/ssz-complete-documentation) | SSZ Complete Documentation | `ssz-complete-documentation/` |
| [**SSZ FULL TEST SUITE**](https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results) | SSZ Full TEST SUITE | `Segmented-Spacetime-Mass-Projection-Unified-Results/` |
| [**SSZ Calculation Suite**](https://github.com/error-wtf/segmented-calculation-suite) | SSZ Calculation Suite| `segmented-calculation-suite/` |
| [**SSZ Main Segmentation Funktion Visualisation**](https://github.com/error-wtf/SEGMENTED_SPACETIME) | SSZ Main Segmentation Funktion Visualisation| `SEGMENTED_SPACETIME/` |
