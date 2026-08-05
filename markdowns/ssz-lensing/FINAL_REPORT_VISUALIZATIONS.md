# FINAL REPORT: Visualizations

**Authors:** Carmen N. Wrede, Lino P. Casu | **Date:** January 2026

---

## Summary

20 publication-ready plots in PNG and PDF formats documenting the no-fit inversion framework.

---

## 1. Generated Plots

### Geometry (4 plots)

| Plot | Description |
|------|-------------|
| `geometry_einstein_cross.png` | Full lens geometry with source, images, quadrupole axis |
| `geometry_quadrupole_effect.png` | How a and b distort the Einstein ring |
| `geometry_image_formation.png` | Image configurations for various source positions |
| `geometry_polar_view.png` | Images in polar coordinates (r vs phi) |

### Rootfinding (4 plots)

| Plot | Description |
|------|-------------|
| `rootfinding_consistency.png` | h(phi_gamma) = 0 consistency function |
| `rootfinding_bisection.png` | Convergence of bisection algorithm |
| `rootfinding_uniqueness.png` | Root stability across parameter space |
| `rootfinding_algorithm.png` | Visual flowchart of inversion algorithm |

### Residuals (4 plots)

| Plot | Description |
|------|-------------|
| `residuals_bars.png` | Residual magnitude per equation |
| `residuals_spatial.png` | Residual vectors at image positions |
| `residuals_noise_comparison.png` | Clean vs noisy data comparison |
| `residuals_model_adequacy.png` | Residuals revealing missing physics |

### Parameters (4 plots)

| Plot | Description |
|------|-------------|
| `parameters_comparison.png` | True vs recovered parameter values |
| `parameters_accuracy_grid.png` | Recovery accuracy across configurations |
| `parameters_error_distribution.png` | Error histograms (machine precision) |
| `parameters_phase_recovery.png` | phi_gamma recovery specifically |

### DoF Analysis (4 plots)

| Plot | Description |
|------|-------------|
| `dof_bookkeeping.png` | Equation vs unknown counting |
| `dof_comparison.png` | DoF balance for different multipoles |
| `dof_system_diagram.png` | Visual structure of 8x5 linear system |
| `dof_conditional_linearity.png` | Conditional linearity concept |

---

## 2. Usage

```bash
cd gauge-gravitationslinse-quadratur
python plots/generate_all_plots.py
```

All plots saved to `plots/` directory in both PNG and PDF formats.

---

## 3. Key Visualizations Explained

### The Einstein Cross
Shows 4 images formed when source is inside diamond caustic. Quadrupole axis indicates orientation of mass distribution.

### Consistency Function h(phi_gamma)
The nonlinear equation that determines phi_gamma. Root at h=0 gives correct phase.

### Residual Bars
All residuals at ~10^-11 for adequate model. Large residuals indicate missing physics.

### DoF Diagram
8 equations (4 images x 2 coords) vs 6 unknowns = 2 redundant for consistency check.

---

## 4. Plot Scripts

| Script | Functions |
|--------|-----------|
| `plot_geometry.py` | `plot_einstein_cross`, `plot_quadrupole_effect`, etc. |
| `plot_rootfinding.py` | `plot_consistency`, `plot_bisection`, etc. |
| `plot_residuals.py` | `plot_residual_bars`, `plot_spatial`, etc. |
| `plot_parameters.py` | `plot_comparison`, `plot_accuracy_grid`, etc. |
| `plot_dof.py` | `plot_bookkeeping`, `plot_system_diagram`, etc. |

---

## 5. Output Summary

```
Generated: 20 PNG files + 20 PDF files
Total: 40 publication-ready figures
Status: All generated successfully
```

---

*Carmen N. Wrede & Lino P. Casu, 2026*
