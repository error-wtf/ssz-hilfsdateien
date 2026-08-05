# SSZ Code Architecture

**Segmented Spacetime (SSZ) - Code Structure & API**

© 2025 Carmen Wrede & Lino Casu  
Licensed under ANTI-CAPITALIST SOFTWARE LICENSE v1.4

---

## 1. Project Structure

```
Segmented-Spacetime-Mass-Projection-Unified-Results/
├── ssz/                      # Core SSZ modules
│   ├── __init__.py
│   └── segwave.py           # SegWave core functions
├── ssz_cosmos/              # Cosmological extensions
│   ├── __init__.py
│   ├── bodies.py            # Body definitions
│   └── field.py             # Multi-body field calculations
├── scripts/                 # Analysis scripts
│   ├── tests/               # Script-level tests
│   └── black_hole_bomb/     # Black hole analysis
├── tests/                   # pytest test suite
│   ├── cosmos/              # Cosmos tests
│   └── lastworking/         # Backup of working tests
├── data/                    # Data files
│   ├── observations/        # Observational data
│   ├── gaia/                # GAIA stellar data
│   └── planck/              # Planck CMB data
├── reports/                 # Generated reports
│   ├── figures/             # Generated plots
│   ├── full-output.md       # Complete test output
│   └── RUN_SUMMARY.md       # Test summary
├── docs/                    # Documentation
├── papers/                  # Theoretical papers
└── out/                     # Output files
```

---

## 2. Core Modules

### 2.1 ssz/segwave.py

**Q-Factor Calculation:**
```python
def compute_q_factor(
    T_curr: float,
    T_prev: float,
    beta: float = 1.0,
    n_curr: float = None,
    n_prev: float = None,
    eta: float = 0.5
) -> float:
    """
    Compute q_k = (T_curr/T_prev)^β × (n_curr/n_prev)^η
    
    Parameters:
        T_curr: Current ring temperature (K)
        T_prev: Previous ring temperature (K)
        beta: Temperature exponent (default: 1.0)
        n_curr: Current ring density (optional)
        n_prev: Previous ring density (optional)
        eta: Density exponent (default: 0.5)
    
    Returns:
        q_k: Energy ratio factor
    """
```

**Velocity Profile:**
```python
def predict_velocity_profile(
    temperatures: np.ndarray,
    v0: float,
    alpha: float = 1.0,
    beta: float = 1.0,
    densities: np.ndarray = None,
    eta: float = 0.5
) -> np.ndarray:
    """
    Predict velocity profile from temperature/density data.
    
    Parameters:
        temperatures: Array of ring temperatures
        v0: Initial velocity (km/s)
        alpha: Velocity scaling exponent
        beta: Temperature exponent
        densities: Optional density array
        eta: Density exponent
    
    Returns:
        velocities: Predicted velocity profile
    """
```

**Frequency Track:**
```python
def predict_frequency_track(
    gammas: np.ndarray,
    f0: float
) -> np.ndarray:
    """
    Predict frequency evolution through rings.
    
    Parameters:
        gammas: Array of cumulative gamma factors
        f0: Initial frequency (Hz)
    
    Returns:
        frequencies: Predicted frequency track
    """
```

---

### 2.2 ssz_cosmos/bodies.py

**Body Definition:**
```python
@dataclass
class BodyDefinition:
    """Definition of a celestial body."""
    name: str
    mass: float          # kg
    radius: float        # m
    position: np.ndarray # [x, y, z] in m
```

---

### 2.3 ssz_cosmos/field.py

**Body State:**
```python
@dataclass
class BodyState:
    """State of a body in the field."""
    name: str
    position: np.ndarray  # [x, y, z]
    mass: float           # kg
    alpha: float = 1.0    # Segment density exponent
    kappa: float = 0.015  # Refractive index coupling
```

**Multi-Body Field:**
```python
class MultiBodyField:
    """Calculate segment density for multiple bodies."""
    
    def sigma(
        self,
        points: np.ndarray,
        states: List[BodyState]
    ) -> np.ndarray:
        """
        Calculate total segment density at points.
        
        Parameters:
            points: Array of [x, y, z] coordinates
            states: List of BodyState objects
        
        Returns:
            sigma: Segment density at each point
        """
    
    def tau(
        self,
        points: np.ndarray,
        states: List[BodyState]
    ) -> np.ndarray:
        """
        Calculate time dilation factor at points.
        """
    
    def refractive_index(
        self,
        points: np.ndarray,
        states: List[BodyState]
    ) -> np.ndarray:
        """
        Calculate effective refractive index at points.
        """
```

---

## 3. Test Scripts

### 3.1 Root-Level Tests

| Script | Description |
|--------|-------------|
| `test_ppn_exact.py` | PPN parameters β=γ=1 |
| `test_vfall_duality.py` | Dual velocity invariant |
| `test_energy_conditions.py` | WEC/DEC/SEC |
| `test_c1_segments.py` | C1 continuity |
| `test_c2_segments_strict.py` | C2 strict continuity |
| `test_c2_curvature_proxy.py` | Curvature proxy |

### 3.2 SegWave Tests

| Test Class | Tests |
|------------|-------|
| `TestQFactor` | 5 tests (temperature, beta, density) |
| `TestVelocityProfile` | 6 tests (shells, alpha, density) |
| `TestFrequencyTrack` | 3 tests (gamma, frequency) |
| `TestResiduals` | 3 tests (match, bias, mixed) |
| `TestCumulativeGamma` | 3 tests (constant, ones, increasing) |

### 3.3 Cosmos Tests

| Script | Description |
|--------|-------------|
| `test_ssz_kernel.py` | SSZ kernel functions |
| `test_ssz_invariants.py` | Physical invariants |
| `test_segmenter.py` | Segmentation algorithm |
| `test_cosmo_fields.py` | Cosmological fields |
| `test_cosmo_multibody.py` | Multi-body interactions |
| `test_multi_body_sigma.py` | Sigma superposition |

---

## 4. Runner Scripts

### 4.1 run_full_suite.py

**Main test orchestrator:**
```bash
python run_full_suite.py           # Run all tests
python run_full_suite.py --quick   # Quick mode
```

**Features:**
- Restores test files from lastworking/ backup
- Clears all caches before tests
- Generates full-output.md and summary
- 25 test phases, ~4 minutes runtime

### 4.2 run_all_validations.py

**Complete validation pipeline:**
```bash
python run_all_validations.py
```

**Pipelines:**
1. run_full_suite.py (main tests)
2. run_ssz_validation.py (SSZ vs GR)
3. run_ssz_theory_validation.py (theory)
4. run_ssz_unified_validation.py (unified ToE)
5. run_complete_test_suite.py (complete)

### 4.3 smoke_test_all.py

**Quick validation (22 tests):**
```bash
python smoke_test_all.py
```

**Categories:**
- Core Dependencies (6 tests)
- SSZ Framework (5 tests)
- Physics Tests (11 tests)

---

## 5. Data Files

### 5.1 Observational Data

| File | Description | Size |
|------|-------------|------|
| `real_data_full.csv` | Full observational dataset | 32 KB |
| `real_astronomical_data.csv` | Real astronomical objects | 1.5 KB |
| `energy_dataset_1000.csv` | Energy framework test data | 101 KB |

### 5.2 GAIA Data

| File | Description |
|------|-------------|
| `gaia_sample_small.csv` | Small GAIA sample |
| `gaia_cone_g79.csv` | G79 region cone search |
| `gaia_cone_cygx.csv` | Cygnus X region cone search |

### 5.3 Ring Data

| File | Description |
|------|-------------|
| `G79_29+0_46_CO_NH3_rings.csv` | G79 multi-ring data |
| `CygnusX_DiamondRing_CII_rings.csv` | Cygnus X ring data |

---

## 6. Output Files

### 6.1 Reports

| File | Description |
|------|-------------|
| `full-output.md` | Complete test output (~300 KB) |
| `summary-output.md` | Compact summary (~1.4 KB) |
| `RUN_SUMMARY.md` | Test results summary |

### 6.2 Figures

Generated in `reports/figures/`:
- Analysis plots
- Validation plots
- Comparison plots

---

## 7. Configuration

### 7.1 pytest Configuration

**pyproject.toml:**
```toml
[tool.pytest.ini_options]
testpaths = ["tests", "scripts/tests"]
python_files = ["test_*.py"]
python_classes = ["Test*"]
python_functions = ["test_*"]
addopts = "-v --tb=short"
```

### 7.2 Environment Variables

```bash
PYTHONIOENCODING=utf-8:replace  # UTF-8 for Windows
PYTHONUTF8=1                    # Python 3.7+ UTF-8 mode
```

---

## 8. API Examples

### 8.1 Calculate Segment Density

```python
from ssz_cosmos.field import BodyState, MultiBodyField
import numpy as np

# Define bodies
sun = BodyState("Sun", np.zeros(3), 1.989e30, 1.0, 0.015)
earth = BodyState("Earth", np.array([1.5e11, 0, 0]), 5.972e24, 1.0, 0.015)

# Calculate field
field = MultiBodyField()
points = np.array([[1e11, 0, 0]])  # Test point
sigma = field.sigma(points, [sun, earth])

print(f"Segment density: {sigma[0]:.6e}")
```

### 8.2 Predict Velocity Profile

```python
from ssz.segwave import predict_velocity_profile
import numpy as np

# Ring temperatures (K)
temperatures = np.array([100, 90, 80, 70, 60])

# Initial velocity (km/s)
v0 = 10.0

# Predict profile
velocities = predict_velocity_profile(temperatures, v0, alpha=1.0)

print(f"Velocities: {velocities}")
```

### 8.3 Calculate Time Dilation

```python
import numpy as np

c = 299792458.0  # m/s
G = 6.67430e-11  # m³/kg/s²
M = 1.989e30     # kg (Sun)

r_s = 2 * G * M / c**2  # Schwarzschild radius
r = 10 * r_s            # Test radius

tau = np.sqrt(1 - r_s/r)
print(f"Time dilation at r=10r_s: τ = {tau:.6f}")
```

---

## 9. Testing

### 9.1 Run All Tests

```bash
# Full test suite
python run_full_suite.py

# Quick smoke tests
python smoke_test_all.py

# Specific test file
python -m pytest tests/test_segwave_core.py -v
```

### 9.2 Expected Results

```
Total Phases: 25
Passed: 25/25
Failed: 0/25
Success Rate: 100.0%
```

---

## 10. Dependencies

### 10.1 Required

```
numpy>=1.20
scipy>=1.7
pandas>=1.3
matplotlib>=3.4
astropy>=5.0
```

### 10.2 Optional

```
plotly>=5.0        # 3D visualization
pyarrow>=8.0       # Parquet support
astroquery>=0.4    # Astronomical queries
pytest>=7.0        # Testing
pytest-timeout     # Test timeouts
```

---

© 2025 Carmen Wrede & Lino Casu
