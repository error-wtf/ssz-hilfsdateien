# SSZ Forward and Anti-Circularity Protocol

This document outlines the strict guidelines governing model prediction and observational validation under the canonical Segmented Spacetime (SSZ) metric research framework.

## Purpose

To prevent the common pitfall in alternative gravity research where model equations or parameters are adjusted post-hoc ("curve fitted") to match observational datasets, SSZ enforces a strict **Forward and Anti-Circular Pipeline**.

## Core Axioms

1. **Analytical Priority (Forward)**:
   All physical inputs are defined analytically and fixed *before* evaluating any observable predictions.
   $$\Xi(r) \rightarrow D(r), s(r) \rightarrow g_{\mu\nu} \rightarrow \text{Observable Prediction} \rightarrow \text{Comparison}$$

2. **Parameter Isolation (Anti-Circularity)**:
   Model parameter values (e.g. core boundary, spline matching boundaries, $\varphi$) are fixed by fundamental mathematical and dimensional requirements (e.g. $r_s = 2GM/c^2$, $x = r/r_s$, $\varphi = \frac{1+\sqrt{5}}{2}$). Under no circumstances is it permitted to adjust, tune, or optimize these parameters to fit observational data.

3. **Banned Optimization Routines**:
   No code in the canonical validation layers may call fitting algorithms or parameter optimizers, including but not limited to:
   - `scipy.optimize.curve_fit` / `least_squares` / `minimize`
   - `numpy.polyfit` / `linregress`
   - `lmfit` / `scikit-learn` regressions
   - Manual parameter grid searches or tolerance inflations.

4. **Category Separation**:
   Validation results must be rigorously partitioned into:
   - **Internal Consistency**: Direct identities and mathematical correctness.
   - **Forward Predictions**: Theoretical predictions evaluated against standard PPN/GR analytic limits.
   - **External Validation**: Comparison against raw/empirical physical observations where available.
   - **Exploratory / Pending**: Experimental limits or fields requiring external data that are currently pending.
