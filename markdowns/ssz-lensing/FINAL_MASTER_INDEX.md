# FINAL MASTER INDEX

## Gauge Gravitational Lens Inversion Framework

**Authors:** Carmen N. Wrede, Lino P. Casu  
**Version:** 1.0 Final | **Date:** January 2026

---

## Quick Navigation

| Document | Purpose |
|----------|---------|
| [FINAL_REPORT_THEORY.md](FINAL_REPORT_THEORY.md) | Complete theoretical framework |
| [FINAL_REPORT_IMPLEMENTATION.md](FINAL_REPORT_IMPLEMENTATION.md) | Code architecture & API |
| [FINAL_REPORT_VALIDATION.md](FINAL_REPORT_VALIDATION.md) | Test results & verification |
| [FINAL_REPORT_VISUALIZATIONS.md](FINAL_REPORT_VISUALIZATIONS.md) | Plot documentation |

---

## Project Overview

### Core Innovation

**No-Fit Inversion:** Exact algebraic solution instead of curve fitting.

```
Traditional: Minimize residuals → "Best fit"
No-Fit:      Solve exactly → Residuals diagnose model
```

### Key Results

| Metric | Value |
|--------|-------|
| Parameter recovery accuracy | Machine precision (~10⁻¹¹) |
| Test success rate | 100% |
| Generated plots | 20 (PNG + PDF) |
| Dependencies | NumPy only |

---

## Documentation Map

### Theory Documents

| File | Content |
|------|---------|
| `paper/general_framework.md` | Full theoretical derivation |
| `notes/design_decisions.md` | No-fit philosophy |
| `FINAL_REPORT_THEORY.md` | Consolidated theory |

### Implementation Documents

| File | Content |
|------|---------|
| `src/models/base_model.py` | Abstract model API |
| `src/inversion/root_solvers.py` | Bisection rootfinding |
| `src/inversion/exact_solvers.py` | Linear system solvers |
| `FINAL_REPORT_IMPLEMENTATION.md` | Full code guide |

### Validation Documents

| File | Content |
|------|---------|
| `tests/test_minimal_exact.py` | Exact recovery tests |
| `demos/demo_minimal.py` | Working demonstration |
| `FINAL_REPORT_VALIDATION.md` | Test documentation |

### Visualization Documents

| File | Content |
|------|---------|
| `plots/README.md` | Plot descriptions |
| `plots/generate_all_plots.py` | Master generator |
| `FINAL_REPORT_VISUALIZATIONS.md` | Plot documentation |

---

## Quick Start

### 1. Run Demo

```bash
python demos/demo_minimal.py
```

Expected: Exact parameter recovery with residuals ~10⁻¹¹

### 2. Run Tests

```bash
python tests/test_minimal_exact.py
```

Expected: All tests pass

### 3. Generate Plots

```bash
python plots/generate_all_plots.py
```

Expected: 40 files (20 PNG + 20 PDF)

---

## Algorithm Summary

```
INPUT: 4 image positions (x_i, y_i)
         ↓
    ┌─────────────────────┐
    │ 1. Rootfinding      │  Find phi_gamma where h(phi_gamma) = 0
    │    (Bisection)      │  via bracketing and bisection
    └─────────────────────┘
         ↓
    ┌─────────────────────┐
    │ 2. Linear Solve     │  Solve 5x5 system for
    │    (Exact)          │  [beta_x, beta_y, theta_E, a, b]
    └─────────────────────┘
         ↓
    ┌─────────────────────┐
    │ 3. Validate         │  Check: max|residual| < tolerance
    │    (Residuals)      │  Check: theta_E > 0
    └─────────────────────┘
         ↓
OUTPUT: Exact parameters + diagnostics
```

---

## Parameter Reference

| Symbol | Name | Meaning |
|--------|------|---------|
| θ_E | Einstein radius | Mass scale (arcsec) |
| a | Radial quadrupole | Mass profile slope |
| b | Tangential quadrupole | Ellipticity + shear |
| φ_γ | Quadrupole phase | Orientation (nonlinear) |
| β_x, β_y | Source position | Offset from axis |

---

## File Structure

```
gauge-gravitationslinse-quadratur/
├── README.md
├── FINAL_MASTER_INDEX.md          ← You are here
├── FINAL_REPORT_THEORY.md
├── FINAL_REPORT_IMPLEMENTATION.md
├── FINAL_REPORT_VALIDATION.md
├── FINAL_REPORT_VISUALIZATIONS.md
│
├── src/
│   ├── gauge_lens_inversion.py
│   ├── models/
│   ├── inversion/
│   └── dataio/
│
├── demos/
│   └── demo_minimal.py
│
├── tests/
│   └── test_minimal_exact.py
│
├── plots/                         ← 20 PNG + 20 PDF
│   ├── generate_all_plots.py
│   ├── plot_*.py
│   └── *.png, *.pdf
│
├── paper/
│   └── general_framework.md
│
└── notes/
    └── design_decisions.md
```

---

## Key Concepts

### 1. Conditional Linearity

The system is **linear in amplitudes** when **phases are fixed**.

This allows:
- Phases (φ_γ): 1D rootfinding
- Amplitudes (θ_E, a, b, β): Exact linear solve

### 2. Degrees of Freedom

```
4 images × 2 coords = 8 equations
6 unknowns (5 linear + 1 nonlinear)
───────────────────────────────────
2 redundant equations → consistency check
```

### 3. Residual Interpretation

| Residual | Meaning |
|----------|---------|
| ~10⁻¹¹ | Model adequate |
| ~10⁻³ | Noisy data |
| ~10⁻² | Model inadequate (missing physics) |

---

## Dependencies

**Required:**
```
numpy>=1.20.0
```

**Optional (visualization):**
```
matplotlib>=3.5.0
```

---

## Authors

**Carmen N. Wrede** & **Lino P. Casu**

Based on the Radial Scaling Gauge formalism for gravitational lensing.

---

## License

ANTI-CAPITALIST SOFTWARE LICENSE v1.4

---

*Final Master Index - Gauge Gravitational Lens Inversion Project*
