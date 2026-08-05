# Visualization Plots

Comprehensive visualizations of the **No-Fit Gravitational Lens Inversion Framework**.

## Quick Start

```bash
# Generate all plots
python generate_all_plots.py
```

This creates PNG and PDF versions of all plots in this directory.

---

## Plot Categories

### 1. Geometry Plots (`geometry_*.png`)

| Plot | Description |
|------|-------------|
| `geometry_einstein_cross.png` | Full annotated Einstein Cross with lens, source, images, and quadrupole axis |
| `geometry_quadrupole_effect.png` | How radial (a) and tangential (b) quadrupole terms distort the ring |
| `geometry_image_formation.png` | Image configurations for different source positions |
| `geometry_polar_view.png` | Images in polar coordinates (r vs φ) |

**Key insight:** The quadrupole distortion breaks the circular symmetry, creating 4 distinct images.

---

### 2. Rootfinding Plots (`rootfinding_*.png`)

| Plot | Description |
|------|-------------|
| `rootfinding_consistency.png` | The consistency function h(φ_γ) for different row combinations |
| `rootfinding_bisection.png` | Bisection convergence showing linear rate |
| `rootfinding_uniqueness.png` | Root stability across different source offsets |
| `rootfinding_algorithm.png` | Visual flowchart of the no-fit algorithm |

**Key insight:** φ_γ is found where h(φ_γ) = 0. This is the ONLY nonlinear step.

---

### 3. Residual Plots (`residuals_*.png`)

| Plot | Description |
|------|-------------|
| `residuals_bars.png` | Residual magnitude per equation (should be ~10⁻¹¹) |
| `residuals_spatial.png` | Residual vectors at image positions |
| `residuals_noise_comparison.png` | Clean vs noisy data residual comparison |
| `residuals_model_adequacy.png` | How residuals reveal missing physics (e.g., m=3 terms) |

**Key insight:** Large residuals indicate model inadequacy, NOT fitting failure.

---

### 4. Parameter Plots (`parameters_*.png`)

| Plot | Description |
|------|-------------|
| `parameters_comparison.png` | True vs recovered parameter values |
| `parameters_accuracy_grid.png` | Recovery accuracy across many random configurations |
| `parameters_error_distribution.png` | Error histograms (should be at machine precision) |
| `parameters_phase_recovery.png` | φ_γ recovery specifically (the nonlinear parameter) |

**Key insight:** Parameters are recovered EXACTLY (to machine precision) for clean data.

---

### 5. DoF Analysis Plots (`dof_*.png`)

| Plot | Description |
|------|-------------|
| `dof_bookkeeping.png` | Equation vs unknown counting for the m=2 model |
| `dof_comparison.png` | DoF balance for different multipole orders |
| `dof_system_diagram.png` | Visual structure of the 8×5 linear system |
| `dof_conditional_linearity.png` | Explanation of conditional linearity concept |

**Key insight:** 4 images → 8 equations, 6 unknowns → 2 redundant equations for consistency check.

---

## The No-Fit Philosophy

These plots illustrate the core principle:

```
NEVER minimize residuals.
ALWAYS solve exactly and LET residuals diagnose model adequacy.
```

| Traditional Fitting | No-Fit Inversion |
|---------------------|------------------|
| Minimize χ² | Solve exactly |
| Residuals → 0 by construction | Residuals reveal data quality |
| Model always "fits" | Model tested against data |
| Need uncertainty estimates | Exact solution or no solution |

---

## File List

```
plots/
├── generate_all_plots.py    # Master script
├── plot_geometry.py         # Lens geometry
├── plot_rootfinding.py      # Rootfinding visualization
├── plot_residuals.py        # Residual analysis
├── plot_parameters.py       # Parameter recovery
├── plot_dof.py              # DoF analysis
├── README.md                # This file
│
├── geometry_einstein_cross.{png,pdf}
├── geometry_quadrupole_effect.{png,pdf}
├── geometry_image_formation.{png,pdf}
├── geometry_polar_view.{png,pdf}
│
├── rootfinding_consistency.{png,pdf}
├── rootfinding_bisection.{png,pdf}
├── rootfinding_uniqueness.{png,pdf}
├── rootfinding_algorithm.{png,pdf}
│
├── residuals_bars.{png,pdf}
├── residuals_spatial.{png,pdf}
├── residuals_noise_comparison.{png,pdf}
├── residuals_model_adequacy.{png,pdf}
│
├── parameters_comparison.{png,pdf}
├── parameters_accuracy_grid.{png,pdf}
├── parameters_error_distribution.{png,pdf}
├── parameters_phase_recovery.{png,pdf}
│
├── dof_bookkeeping.{png,pdf}
├── dof_comparison.{png,pdf}
├── dof_system_diagram.{png,pdf}
└── dof_conditional_linearity.{png,pdf}
```

---

## Requirements

- Python 3.8+
- NumPy
- Matplotlib

```bash
pip install numpy matplotlib
```
