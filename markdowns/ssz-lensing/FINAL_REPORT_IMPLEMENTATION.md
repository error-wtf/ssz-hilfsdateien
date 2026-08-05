# FINAL REPORT: Implementation Guide

## Code Architecture and Usage

**Authors:** Carmen N. Wrede, Lino P. Casu  
**Date:** January 2026  
**Version:** 1.0 Final

---

## Executive Summary

This document describes the complete implementation of the no-fit gravitational lens inversion framework. The codebase is organized into modular components with clear responsibilities, using only NumPy for numerical operations (no scipy.optimize required).

**Key Features:**
- Pure Python 3.8+ with NumPy only
- Modular design with pluggable lens models
- Comprehensive residual diagnostics
- Full visualization suite

---

## 1. Project Structure

```
gauge-gravitationslinse-quadratur/
├── README.md                    # Project overview
├── FINAL_REPORT_*.md           # Final documentation
│
├── src/                        # Source code
│   ├── __init__.py
│   ├── gauge_lens_inversion.py # Original standalone script
│   │
│   ├── models/                 # Lens models
│   │   ├── __init__.py
│   │   ├── base_model.py      # Abstract model API
│   │   ├── ring_quadrupole_offset.py  # Minimal m=2 model
│   │   └── multipole_model.py # General multipole model
│   │
│   ├── inversion/             # Inversion algorithms
│   │   ├── __init__.py
│   │   ├── exact_solvers.py   # Linear system solvers
│   │   ├── root_solvers.py    # Bisection rootfinding
│   │   ├── constraints.py     # DoF bookkeeping
│   │   └── diagnostics.py     # Residual analysis
│   │
│   └── dataio/                # Data I/O
│       ├── __init__.py
│       ├── formats.py         # JSON/CSV handling
│       └── datasets.py        # Synthetic data generation
│
├── demos/                     # Demonstration scripts
│   ├── demo_minimal.py        # Basic usage demo
│   └── demo_multipole.py      # Framework demo
│
├── tests/                     # Unit tests
│   ├── test_minimal_exact.py  # Exact recovery tests
│   └── test_multipole_consistency.py
│
├── plots/                     # Visualization
│   ├── generate_all_plots.py  # Master generator
│   ├── plot_geometry.py       # Lens geometry
│   ├── plot_rootfinding.py    # Algorithm visualization
│   ├── plot_residuals.py      # Residual analysis
│   ├── plot_parameters.py     # Parameter recovery
│   ├── plot_dof.py            # DoF analysis
│   └── README.md              # Plot documentation
│
├── paper/                     # Theory documents
│   ├── gauge_gravitationslinse_quadratur.md
│   └── general_framework.md
│
├── notes/                     # Design notes
│   ├── discussion_context.md
│   └── design_decisions.md
│
└── data/                      # Example data
    └── example_points.json
```

---

## 2. Core Components

### 2.1 Models (`src/models/`)

#### Abstract Base Class

```python
# base_model.py
from abc import ABC, abstractmethod

class LensModel(ABC):
    """Abstract base class for lens models."""
    
    @abstractmethod
    def n_linear_params(self) -> int:
        """Number of linear parameters."""
        pass
    
    @abstractmethod
    def n_nonlinear_params(self) -> int:
        """Number of nonlinear parameters (phases)."""
        pass
    
    @abstractmethod
    def build_linear_system(self, images, nonlinear_params):
        """Build A matrix and b vector for Ax = b."""
        pass
    
    @abstractmethod
    def predict_images(self, linear_params, nonlinear_params):
        """Predict image positions from parameters."""
        pass
```

#### Minimal Quadrupole Model

```python
# ring_quadrupole_offset.py
class RingQuadrupoleOffset(LensModel):
    """
    Minimal m=2 model with:
    - Einstein ring (theta_E)
    - Quadrupole (a, b, phi_gamma)
    - Source offset (beta_x, beta_y)
    
    Linear params: [beta_x, beta_y, theta_E, a, b]
    Nonlinear params: [phi_gamma]
    """
    
    def build_linear_system(self, images, phi_gamma):
        n = len(images)
        A = np.zeros((2 * n, 5))
        b = np.zeros(2 * n)
        
        for i, (x, y) in enumerate(images):
            phi = np.arctan2(y, x)
            Delta = phi - phi_gamma
            
            # x equation
            A[2*i, 0] = 1.0  # beta_x
            A[2*i, 2] = np.cos(phi)  # theta_E
            A[2*i, 3] = np.cos(2*Delta) * np.cos(phi)  # a
            A[2*i, 4] = -np.sin(2*Delta) * np.sin(phi)  # b
            b[2*i] = x
            
            # y equation
            A[2*i+1, 1] = 1.0  # beta_y
            A[2*i+1, 2] = np.sin(phi)  # theta_E
            A[2*i+1, 3] = np.cos(2*Delta) * np.sin(phi)  # a
            A[2*i+1, 4] = np.sin(2*Delta) * np.cos(phi)  # b
            b[2*i+1] = y
        
        return A, b
```

### 2.2 Inversion (`src/inversion/`)

#### Exact Linear Solvers

```python
# exact_solvers.py

def solve_exact(A, b, row_indices):
    """
    Solve Ax = b exactly using specified rows.
    
    Parameters:
        A: Full matrix (m x n)
        b: Full RHS vector (m,)
        row_indices: Which rows to use (n,)
    
    Returns:
        x: Solution vector (n,)
    
    Raises:
        SingularMatrixError if system is singular
    """
    A_sub = A[row_indices, :]
    b_sub = b[row_indices]
    
    det = np.linalg.det(A_sub)
    if abs(det) < 1e-14:
        raise SingularMatrixError("Matrix is singular")
    
    return np.linalg.solve(A_sub, b_sub)
```

#### Root Solvers

```python
# root_solvers.py

def bisection(f, a, b, tol=1e-12, max_iter=100):
    """
    Find root of f in [a, b] via bisection.
    
    Precondition: f(a) * f(b) < 0
    """
    fa = f(a)
    for _ in range(max_iter):
        mid = (a + b) / 2
        fm = f(mid)
        
        if abs(fm) < tol or (b - a) / 2 < tol:
            return mid
        
        if fa * fm < 0:
            b = mid
        else:
            a = mid
            fa = fm
    
    return (a + b) / 2


def find_all_roots(f, a, b, n_samples=100, tol=1e-12):
    """
    Find all roots of f in [a, b].
    
    Strategy:
    1. Sample f at n_samples points
    2. Identify sign changes (brackets)
    3. Refine each bracket with bisection
    4. Verify roots are valid (not NaN/Inf)
    """
    x = np.linspace(a, b, n_samples)
    y = np.array([f(xi) for xi in x])
    
    roots = []
    for i in range(n_samples - 1):
        if np.isfinite(y[i]) and np.isfinite(y[i+1]):
            if y[i] * y[i+1] < 0:
                root = bisection(f, x[i], x[i+1], tol)
                # Verify root
                if np.isfinite(f(root)) and abs(f(root)) < tol * 100:
                    roots.append(root)
    
    return roots
```

#### Diagnostics

```python
# diagnostics.py

def compute_residuals(A, p, b):
    """Compute residuals r = Ap - b."""
    return A @ p - b


def analyze_residuals(residuals, images):
    """
    Analyze residual patterns.
    
    Returns dict with:
        - max_abs: Maximum absolute residual
        - rms: Root mean square
        - angular_correlation: Correlation with image angle
        - radial_correlation: Correlation with image radius
        - model_adequate: Boolean flag
    """
    max_abs = np.max(np.abs(residuals))
    rms = np.sqrt(np.mean(residuals**2))
    
    # Angular correlation
    angles = np.arctan2(images[:, 1], images[:, 0])
    res_per_image = residuals.reshape(-1, 2)
    # ... correlation analysis
    
    return {
        'max_abs': max_abs,
        'rms': rms,
        'model_adequate': max_abs < 1e-8
    }
```

### 2.3 Data I/O (`src/dataio/`)

#### Synthetic Data Generation

```python
# datasets.py

def generate_einstein_cross(theta_E, a, b, beta, phi_beta, phi_gamma):
    """
    Generate synthetic 4-image configuration.
    
    Returns:
        images: (4, 2) array of (x, y) positions
        phi_solutions: (4,) array of image azimuths
    """
    def angular_condition(phi):
        return beta * np.sin(phi - phi_beta) + b * np.sin(2*(phi - phi_gamma))
    
    # Find roots (image azimuths)
    roots = find_all_roots(angular_condition, 0, 2*np.pi)
    phi_solutions = np.array(roots)
    
    # Compute radii
    radii = (theta_E 
             + a * np.cos(2*(phi_solutions - phi_gamma))
             + beta * np.cos(phi_solutions - phi_beta))
    
    # Convert to Cartesian
    images = np.column_stack([
        radii * np.cos(phi_solutions),
        radii * np.sin(phi_solutions)
    ])
    
    return images, phi_solutions
```

---

## 3. Main Inversion Function

```python
def invert_no_fit(images, model=None, phi_range=(0, np.pi/2)):
    """
    Perform no-fit lens inversion.
    
    Parameters:
        images: (N, 2) array of image positions
        model: LensModel instance (default: RingQuadrupoleOffset)
        phi_range: Search range for phi_gamma
    
    Returns:
        List of valid solutions, each containing:
            - 'phi_gamma': Recovered phase
            - 'params': Linear parameters [beta_x, beta_y, theta_E, a, b]
            - 'residuals': Per-equation residuals
            - 'diagnostics': Residual analysis
    """
    if model is None:
        model = RingQuadrupoleOffset()
    
    # Define consistency function
    row_subset = [0, 1, 2, 3, 4]  # 5 rows for 5 unknowns
    check_row = 5  # Consistency check row
    
    def h(phi_gamma):
        A, b = model.build_linear_system(images, phi_gamma)
        try:
            p = solve_exact(A, b, row_subset)
            return A[check_row, :] @ p - b[check_row]
        except SingularMatrixError:
            return np.inf
    
    # Find all roots
    roots = find_all_roots(h, phi_range[0], phi_range[1])
    
    # Solve and validate for each root
    solutions = []
    for phi_gamma in roots:
        A, b = model.build_linear_system(images, phi_gamma)
        p = solve_exact(A, b, row_subset)
        
        # Physical constraints
        theta_E = p[2]
        if theta_E <= 0:
            continue
        
        # Compute residuals
        residuals = compute_residuals(A, p, b)
        diagnostics = analyze_residuals(residuals, images)
        
        if diagnostics['model_adequate']:
            solutions.append({
                'phi_gamma': phi_gamma,
                'params': p,
                'residuals': residuals,
                'diagnostics': diagnostics
            })
    
    return solutions
```

---

## 4. Usage Examples

### 4.1 Basic Usage

```python
import numpy as np
from src.dataio.datasets import generate_einstein_cross
from src.inversion.root_solvers import find_all_roots

# True parameters
theta_E = 1.0
a = 0.05
b = 0.15
beta = 0.08
phi_beta = np.radians(30)
phi_gamma = np.radians(20)

# Generate synthetic data
images, _ = generate_einstein_cross(theta_E, a, b, beta, phi_beta, phi_gamma)

# Invert
solutions = invert_no_fit(images)

# Report
for sol in solutions:
    print(f"phi_gamma: {np.degrees(sol['phi_gamma']):.2f} deg")
    print(f"theta_E: {sol['params'][2]:.6f}")
    print(f"max residual: {sol['diagnostics']['max_abs']:.2e}")
```

### 4.2 Running Demos

```bash
# Minimal demo with exact recovery
python demos/demo_minimal.py

# Expected output:
# TRUE PARAMETERS:
#   theta_E = 1.000000
#   a = 0.050000
#   b = 0.150000
#   ...
# 
# INVERSION RESULT:
#   theta_E = 1.000000000000
#   max|residual| = 2.98e-11
#   Status: EXACT RECOVERY
```

### 4.3 Running Tests

```bash
# Test exact recovery
python tests/test_minimal_exact.py

# Test framework consistency
python tests/test_multipole_consistency.py
```

---

## 5. Extending the Framework

### 5.1 Adding a New Lens Model

```python
from src.models.base_model import LensModel

class MyCustomModel(LensModel):
    """Custom lens model with m=3 octupole."""
    
    def n_linear_params(self):
        return 7  # beta_x, beta_y, theta_E, a2, b2, a3, b3
    
    def n_nonlinear_params(self):
        return 2  # phi_2, phi_3
    
    def build_linear_system(self, images, nonlinear_params):
        phi_2, phi_3 = nonlinear_params
        # Build extended system...
        return A, b
```

### 5.2 Adding New Observables

To add time delays:

```python
def add_time_delay_equations(A, b, images, delays, H0):
    """
    Add time delay constraints to linear system.
    
    Each delay adds 1 equation relating:
    dt_ij = f(theta_i, theta_j, beta, psi)
    """
    n_images = len(images)
    n_delays = len(delays)
    
    # Extend A and b
    A_extended = np.zeros((A.shape[0] + n_delays, A.shape[1]))
    A_extended[:A.shape[0], :] = A
    
    # Add delay equations
    for k, (i, j, dt) in enumerate(delays):
        # Compute coefficients for delay equation
        # ...
        A_extended[A.shape[0] + k, :] = delay_coeffs
    
    return A_extended, b_extended
```

---

## 6. Configuration

### 6.1 Tolerances

```python
# Rootfinding tolerance
ROOT_TOL = 1e-12

# Residual threshold for model adequacy
RESIDUAL_THRESHOLD = 1e-8

# Singularity detection threshold
SINGULARITY_TOL = 1e-14
```

### 6.2 Search Parameters

```python
# Phase search range (exploiting 90° periodicity)
PHI_RANGE = (0, np.pi/2)

# Number of samples for bracket detection
N_SAMPLES = 100
```

---

## 7. Error Handling

### 7.1 Exception Types

```python
class LensInversionError(Exception):
    """Base exception for inversion errors."""
    pass

class SingularMatrixError(LensInversionError):
    """Linear system is singular."""
    pass

class NoValidSolutionError(LensInversionError):
    """No physically valid solution found."""
    pass

class ModelInadequateError(LensInversionError):
    """Residuals indicate model inadequacy."""
    pass
```

### 7.2 Diagnostic Messages

| Error | Likely Cause | Recommended Action |
|-------|--------------|-------------------|
| `SingularMatrixError` | Degenerate image config | Try different row subset |
| `NoValidSolutionError` | theta_E < 0 for all roots | Check data quality |
| `ModelInadequateError` | Large structured residuals | Increase m_max |

---

## 8. Performance Notes

### 8.1 Computational Complexity

| Operation | Complexity | Notes |
|-----------|------------|-------|
| Linear system build | O(N) | N = number of images |
| 5x5 linear solve | O(1) | Fixed small system |
| Consistency function eval | O(1) | Single 5x5 solve |
| Rootfinding | O(n_samples) | ~100 samples typical |
| Total inversion | O(100) | Very fast |

### 8.2 Memory Usage

- Minimal: only stores 8x5 matrix and vectors
- No iterative optimization history
- Scales trivially to batch processing

---

## 9. Dependencies

### 9.1 Required

```
numpy>=1.20.0
```

### 9.2 Optional (for visualization)

```
matplotlib>=3.5.0
```

### 9.3 Installation

```bash
# Core functionality
pip install numpy

# With visualization
pip install numpy matplotlib

# Development
pip install numpy matplotlib pytest
```

---

## 10. API Reference Summary

### Models

| Class | Description |
|-------|-------------|
| `LensModel` | Abstract base class |
| `RingQuadrupoleOffset` | Minimal m=2 model |
| `MultipoleModel` | General multipole model |

### Solvers

| Function | Description |
|----------|-------------|
| `solve_exact(A, b, rows)` | Exact linear solve |
| `bisection(f, a, b)` | Bisection rootfinding |
| `find_all_roots(f, a, b)` | Find all roots in interval |

### Diagnostics

| Function | Description |
|----------|-------------|
| `compute_residuals(A, p, b)` | Compute r = Ap - b |
| `analyze_residuals(r, images)` | Pattern analysis |

### Data I/O

| Function | Description |
|----------|-------------|
| `generate_einstein_cross(...)` | Synthetic data |
| `load_json(path)` | Load from JSON |
| `save_json(data, path)` | Save to JSON |

---

## 11. Conclusion

This implementation provides:

1. **Clean modular architecture** with separation of concerns
2. **Pure NumPy implementation** without optimization libraries
3. **Extensible design** for new models and observables
4. **Comprehensive diagnostics** for solution validation
5. **Full test coverage** for reliability

The codebase is designed for **transparency and correctness** over optimization, matching the no-fit philosophy of the theoretical framework.

---

*Final Report: Implementation Guide*  
*Gauge Gravitational Lens Inversion Project*  
*Carmen N. Wrede & Lino P. Casu, 2026*
