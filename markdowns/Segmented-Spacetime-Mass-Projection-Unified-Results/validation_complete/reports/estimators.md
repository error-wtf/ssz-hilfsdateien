# estimators.md
**Robust estimation procedures for the Segmented Spacetime model**  
*(from observations → model inputs: z_geom, r_phi, ΔM, segment density, …)*

## 0) Purpose & scope
This document defines **reproducible estimators** that turn raw observations (spectral lines, radial velocities, orbital elements, BH shadow sizes, GW signals) into **auditable inputs** for the segmented–spacetime model (e.g., r_phi, z_geom, segment densities, ΔM).  
Goals:
- **Reproducibility** (uniform recipes + error propagation)
- **No circularity** (strict separation of SR vs. geometry)
- **Comparability** (GR baseline vs. Segment model)
- **CI-readiness** (train/test splits, robust metrics)

These estimators align with our test runners (`segspace_enhanced_test*.py`): *hint*, *deltaM*, *hybrid*, and the “final” evaluation with robust statistics.

---

## 1) Design principles
1. **Separate measured from modeled.** Remove the SR contribution first → geometric remainder z_geom.
2. **No dataset leakage.** Fit parameters (A, B, alpha, Theta) **only on the train split**; apply frozen values on test.
3. **Robust statistics.** Use medians, MAD trims, bootstrap CIs, and Wilcoxon (paired) tests.
4. **Flag heuristics.** Any assumption (e.g., tangential speed) must be flagged and reported separately.
5. **Consistent SI units & notation.** Centralize constants; keep variable names consistent.

---

## 2) Notation & constants

- c: speed of light  
- G: gravitational constant  
- phi_const := (1 + sqrt(5))/2   # Golden Ratio (dimensionless)  
- phi_len   := …                 # physical segment length (if used) — keep separate from phi_const!  
- r_s := 2 G M / c^2             # Schwarzschild radius  
- z_tot := f_emit/f_obs − 1      # or directly measured redshift  
- z_SR  := SR contribution (Doppler/γ, per mode)  
- z_geom := (1 + z_tot)/(1 + z_SR) − 1   # geometric part after SR removal  

**SR modes**
- STRICT: z_SR ≈ v_los / c  (non-rel., line-of-sight only; conservative)  
- FULL:   z_SR = γ (1 + β cosθ) − 1, with β = v_tot/c and γ = 1/sqrt(1−β²), if v_tot & geometry are known

**Combining independent contributions (conservative)**  
(1 + z_tot) = (1 + z_geom)(1 + z_SR)  ⇒  z_geom = (1 + z_tot)/(1 + z_SR) − 1

---

## 3) Minimum data schema
The following columns should be present when available. Our runners already recognize many of these:

- Spectral / kinematics: `f_emit, f_obs, z_obs (alias z_tot), v_los, v_tot, theta` (+ uncertainties: `sigma_f, sigma_v, …`)  
- Gravity / orbit: `M, a, e, P, r_peri, r_apo, D, theta_sh, r_eff_source`  
- Meta / flags: `object_id, class_tag (S-star, WD, MS, SMBH, …), is_strong_row`

Note: `is_strong_row=True` if orbit information is complete (e.g., S-stars). Runners emit Debug-CSVs (e.g., z_SR, z_geom, r_s, deltaM_term, “heuristic used”).

---

## 4) Estimators

### A) z-based estimator (near compact masses)
**Purpose:** From a spectral line + velocity, estimate z_geom, r_eff and/or r_phi.

**Inputs:** `f_emit, f_obs` (or `z_tot`), `v_los` (optional `v_tot, theta`), `M`, uncertainties.  
**Outputs:** `z_geom_hat`, `r_eff_hat` (GR comparison), `r_phi_hat` (Segment), optional `N_seg_hat`.

**Steps**
1. z_tot ← f_emit/f_obs − 1 (if not provided).  
2. SR removal:  
   - STRICT: z_SR ≈ v_los / c  
   - FULL:   z_SR = γ (1 + β cosθ) − 1  
   ⇒ z_geom = (1 + z_tot)/(1 + z_SR) − 1  
3. GR baseline (for comparison):  
   - weak field: z_GR ≈ GM/(r c²) = r_s/(2r)  ⇒  r_GR ≈ r_s/(2 z_geom)  
   - exact (Schwarzschild):  z = (1 − r_s/r)^(−1/2) − 1  ⇒  r = r_s / [1 − (1+z)^(−2)]  
4. Segment model: map z_geom → r_phi via r_phi = H(z_geom; Θ) · r_s  (Θ fitted on train only)  
   - optional: N_seg = S(z_geom) if your model defines a direct mapping  
5. Uncertainty: bootstrap over f_emit, f_obs, v, M → confidence intervals

**Validity:** meaningful for r ≳ 5–10 r_s.  
**Runner mapping:** the `hint` branch uses z_geom_hint and multiplies with SR; fallback is GR×SR where hints are unavailable.

---

### B) BH shadow estimator (EHT-like)
**Purpose:** From shadow angle θ_sh and distance D, estimate an effective radius r_phi.

**Inputs:** θ_sh (radians), D, M (or an independent mass estimate).  
**Outputs:** `r_eff_hat` or `r_phi_hat`.

**Steps**
1. R_app = D · θ_sh (apparent radius)  
2. GR baseline: R_sh,GR ≈ sqrt(27) · GM/c² = (sqrt(27)/2) · r_s  (Schwarzschild; spin/inclination → ~2.6…5.2)  
3. Segment model: r_phi = K_seg(θ_sh, D; Θ) · r_s  
4. Propagate σ(θ_sh), σ(D), σ(M)

**Tests:** M87*, Sgr A* (EHT publications).

---

### C) Perihelion precession estimator
**Purpose:** Use orbital precession to correct r_phi or segment parameters.

**Inputs:** a, e, M of the central mass, observed Δϖ per orbit.  
**Outputs:** `r_phi_hat` or Q_seg (model factor).

**Steps**
1. GR baseline: Δϖ_GR = 6π GM / [a (1 − e²) c²]  
2. Segment: Δϖ_seg = Δϖ_GR · Q_seg(a, e; Θ)  
3. Invert/fit against Δϖ_obs (fit on train, verify on test)

**Tests:** Mercury, pulsar binaries (where available).

---

### D) Spectral-line / calibration estimator (21-cm anchor)
**Purpose:** Derive segment scaling from reference lines.

**Inputs:** reference line (e.g., 21 cm), target line (λ, f), v_los.  
**Outputs:** N_seg scale, mapping constants.

**Steps**
1. Compute z_geom via SR removal as in A).  
2. Scale segments: N′ = N_ref · (λ_ref / λ′)  
3. Consistency: f′ = f_ref · (N_ref / N′)  
4. Fit/check segment scaling against lab data

---

### E) GW phase/dispersion estimator (LIGO hook)
**Purpose:** Frequency-dependent residuals versus GR templates.

**Inputs:** GW phase φ(f), amplitude A(f), distance, M1, M2.  
**Outputs:** φ_res(f) (Segment − GR), simple dispersion parameters.

**Steps:** Template matching (GR vs. Segment) → φ_res(f); SNR-weighted fits; frequency slices.

---

## 5) ΔM corrector (optional — fit only on train!)
**Motivation:** Scale **only** the GR part relative to segment-induced “mass accessibility” (do **not** multiply (1+z); SR remains separate).

**Form**  
ΔM(M) = (A · exp(−alpha · r_s) + B) · norm(log10 M)

- A, B, alpha are fitted **only on the train split**; frozen on test.  
- norm(log10 M): **do not** min–max over the *test* set; use fixed physical bounds (e.g., [−30, 10] in log10(M/M_sun)) **or** quantiles from **train** only.  
- Parameter sweep alpha ∈ [1e−13, 1e−9] m⁻¹; preferably couple to **segment density** σ(r) rather than r_s alone.

**Application (deltaM/hybrid branches)**  
z_seg = z_SR + ΔM(M) · z_GR + z_resid(geometry/hints)

Pipeline mapping: `deltaM` scales z_GR (fixing the old multiplication bug) and multiplies with SR; `hybrid` uses `hint` for S-stars and `deltaM` for all others.

---

## 6) Validation, CV & metrics

**Splits:** k-fold CV or fixed train/test split (stratified by class).  
**Leakage control:** Fit parameters on train; apply **frozen** on test.

**Metrics (per mode/class & global)**
- Median(|Δz|)
- Robust mean (e.g., 10% trim + MAD scaling)
- Max(|Δz|) (orientation only)
- Bootstrap CIs (2.5% / 97.5%)
- Wilcoxon signed-rank: Segment vs. GR (paired residuals)

**Slices (report additionally)**
- STRICT-SR vs. FULL-SR
- with/without velocity heuristic
- near-horizon (e.g., r_eff < 10 r_s)
- classes (S-stars, MS, WD, SMBH, …)

**Sanity guards (as in the “final” runner)**
- r_eff ≥ r_s; class-specific minimum radii
- v < 0.2 c for stars
- flags for missing/heuristic velocities

---

## 7) Reference pseudocode (building blocks)

```python
def sr_strict(v_los):
    return v_los / c  # conservative, non-relativistic

def sr_full(v_tot, theta):
    beta  = v_tot / c
    gamma = 1.0 / (1.0 - beta**2)**0.5
    return gamma * (1 + beta * math.cos(theta)) - 1.0

def z_geom_from_obs(f_emit=None, f_obs=None, z_tot=None,
                    sr_mode='STRICT', v_los=None, v_tot=None, theta=0.0):
    if z_tot is None:
        assert f_emit is not None and f_obs is not None
        z_tot = f_emit / f_obs - 1.0
    z_sr = sr_strict(v_los) if sr_mode=='STRICT' else sr_full(v_tot, theta)
    return (1.0 + z_tot) / (1.0 + z_sr) - 1.0

def r_from_z_gr(z_geom, r_s, exact=True):
    if exact:
        # Schwarzschild exact: z = (1 - r_s/r)^(-1/2) - 1
        # => r = r_s / (1 - (1+z)^(-2))
        return r_s / (1.0 - (1.0 / (1.0 + z_geom)**2))
    else:
        # weak field: z ≈ r_s / (2 r)  =>  r ≈ r_s / (2 z)
        return r_s / (2.0 * z_geom)

def r_phi_from_z_geom(z_geom, r_s, Theta_frozen):
    # Placeholder: H-function of the segment model
    H = H_model(z_geom, Theta_frozen)  # parameters from train split
    return H * r_s
````

---

## 8) Outputs (reports & debug)

Main report (CSV): object_id, class_tag, mode, |Δz|, z_obs, z_pred, r_eff, r_phi, sr_mode, flags (heuristic_velocity, near_horizon, sanity_violation)

Debug-CSV: full intermediates (z_SR, z_geom, r_s, deltaM_term, r_source, used_hint, used_deltaM, …)

Plots (at least): residual histograms per mode/class; boxplots STRICT vs. FULL; bar chart “Segment/GR” (medians)

## 9) Unit tests (minimum)

Synthetic: forward (M→z) & inverse (z→r) consistency; roundtrip tolerances

Lab anchor: 21-cm calibration against the reference frequency

Astro checks: Sirius B, S-stars (S2), one WD, one MS star; optionally an EHT object

Slices: STRICT-SR vs. FULL-SR; with/without velocity heuristic

CI gate (optional): e.g., “Segment median ≤ 1.2× GR median” on the test split

## 10) Changelog

v1.0 — Initial version: estimators A–E; ΔM form; SR modes; GR baselines; CV rules; reporting & tests

## 11) Recommended defaults & scans
SR mode: default STRICT; FULL only with reliable v_tot & geometry

alpha scan (deltaM): [1e−13, 1e−9] m⁻¹ (log scale)

Bootstrap: ≥ 1000 resamples per metric

Near-horizon flag: r_eff < 10 r_s

Sanity guards: r_eff ≥ r_s; class-specific minimum radii; v < 0.2 c for stars