# SSZ Critical Errors Prevention Guide

**Version:** 1.0.0  
**Date:** 2025-01-17  
**Status:** AUTHORITATIVE - Follow this document to avoid known errors

---

## Executive Summary

This document catalogs ALL critical errors discovered during SSZ implementation
and provides definitive solutions. **Read this before modifying any physics code.**

---

## ERROR #1: Wrong Redshift Formula (CRITICAL)

### The Error

```python
# ❌ WRONG - This was the original implementation
z_ssz = 1/D_ssz - 1  # Gives z = Xi, which is ~350% wrong!
```

### Why It's Wrong

- This formula interprets D_ssz (time dilation) as directly giving redshift
- It produces z_ssz ≈ 0.78 for neutron stars (350% higher than GR!)
- The papers explicitly state that SSZ redshift matches GR almost exactly

### The Correct Formula

```python
# ✅ CORRECT - From "Dual Velocities" paper
z_ssz = z_gr * (1 + delta_m / 100)  # Only ~1-2% deviation from GR
```

### Source Documentation

> "In the segmented model γ_s is matched identical, therefore z(r) is identical"  
> — Dual Velocities in Segmented Spacetime, Section 4.2

> "Δ(M) multiplies the GR gravitational redshift by a factor 1 + Δ(M)"  
> — Verification Summary of Segmented Spacetime Repository

### Verification Test

```python
def test_redshift_formula():
    M_kg = 1.4 * M_SUN
    R_m = 12000
    result = z_ssz(M_kg, R_m)
    
    # z_SSZ should be within 5% of z_GR (NOT 350%!)
    diff_pct = abs(result["z_ssz_grav"] - result["z_gr"]) / result["z_gr"] * 100
    assert diff_pct < 5, f"z_SSZ differs from z_GR by {diff_pct}% - should be ~1-2%"
```

---

## ERROR #2: Confusing D_ssz with Redshift

### The Error

Using D_ssz = 1/(1+Ξ) directly for redshift calculations.

### Why It's Wrong

- D_ssz is the **time dilation factor** (dτ/dt)
- Redshift z is NOT simply 1/D - 1 in SSZ
- SSZ matches GR redshift with only a small Δ(M) correction

### Correct Usage

| Quantity | Formula | Use Case |
|----------|---------|----------|
| D_ssz | 1/(1+Ξ) | Time dilation comparisons |
| z_gr | 1/√(1-r_s/r) - 1 | Gravitational redshift |
| z_ssz | z_gr × (1 + Δ(M)/100) | SSZ redshift prediction |

### Key Insight

D_ssz ≠ D_gr, but z_ssz ≈ z_gr. The segment structure affects time dilation
differently than it affects photon redshift.

---

## ERROR #3: Wrong Xi Formula for Regime

### The Error

Using the deprecated exponential formula:

```python
# ❌ DEPRECATED - Do NOT use
Xi = (r_s/r)² × exp(-r/r_φ)
```

### Correct Formulas

```python
# ✅ CORRECT - Weak Field (r/r_s > 110)
Xi_weak = r_s / (2*r)

# ✅ CORRECT - Strong Field (r/r_s < 90)
Xi_strong = 1 - exp(-φ*r_s / r)

# Blend Zone (90 < r/r_s < 110): C² Quintic Hermite Interpolation
```

### Source

> WEAK_STRONG_FIELD_SPEC.md, Section 2: "Ξ-Formeln"

---

## ERROR #4: Missing Δ(M) Normalization

### The Error

Applying Δ(M) without mass-range normalization:

```python
# ❌ WRONG - No normalization
delta_m = A * exp(-alpha * r_s) + B
```

### Why It's Wrong

Without normalization, Δ(M) gives unrealistic corrections for extreme masses.

### Correct Formula

```python
# ✅ CORRECT - With log10(M) normalization
lM = log10(M_kg)
norm = (lM - lM_min) / (lM_max - lM_min)
norm = min(1.0, max(0.0, norm))
delta_m = (A * exp(-alpha * r_s) + B) * norm
```

### Parameters

| Parameter | Value | Source |
|-----------|-------|--------|
| A | 98.01 | φ-calibration |
| α | 2.7177×10⁴ | φ-calibration |
| B | 1.96 | φ-calibration |
| lM_min | 10.0 | Dataset minimum |
| lM_max | 42.0 | Dataset maximum |

---

## ERROR #5: Not Using z_geom_hint for S-Stars

### The Error

Using standard Δ(M) correction for S-star objects around Sgr A*.

### Why It's Wrong

- S-stars have observed redshifts (z_geom_hint) from orbital mechanics
- Standard Δ(M) gives ~51% win rate
- z_geom_hint gives **97.9%** win rate with ESO data

### Correct Implementation

```python
def z_ssz(M_kg, r_m, use_geom_hint=False):
    if use_geom_hint:
        # S-star mode: Use φ-geometric formula
        z_geom = z_geom_hint(M_kg, r_m)
        return z_geom
    else:
        # Standard mode: GR with Δ(M) correction
        return z_gr * (1 + delta_m / 100)
```

### When to Use Each Mode

| Object Type | Mode | Expected Win Rate |
|-------------|------|-------------------|
| S-stars around Sgr A* | use_geom_hint=True | 97.9% |
| Neutron stars | use_delta_m=True | 51-82% |
| White dwarfs | use_delta_m=True | ~50% |
| Weak field objects | use_delta_m=True | ~37% |

---

## ERROR #6: Incorrect Regime Boundaries

### The Error

Using arbitrary or inconsistent regime boundaries.

### Correct Boundaries

| Regime | r/r_s Range | Formula |
|--------|-------------|---------|
| very_close | < 2.0 | Strong field, near horizon |
| photon_sphere | 2.0 - 3.0 | SSZ optimal (82% wins) |
| strong | 3.0 - 10.0 | Strong field |
| weak | > 10.0 | Weak field |

### Blend Zone

| Boundary | r/r_s | Purpose |
|----------|-------|---------|
| REGIME_STRONG_THRESHOLD | 90 | Below: use Xi_strong |
| REGIME_WEAK_THRESHOLD | 110 | Above: use Xi_weak |
| Blend zone | 90-110 | C² Hermite interpolation |

---

## ERROR #7: Forgetting the Golden Ratio

### The Error

Using arbitrary constants instead of φ = (1+√5)/2.

### Why It's Wrong

φ is FUNDAMENTAL to SSZ. All corrections derive from φ-spiral geometry.

### Key φ-Dependent Values

| Value | Formula | Result |
|-------|---------|--------|
| φ | (1+√5)/2 | 1.618034 |
| φ/2 | Geometric factor | 0.809017 |
| Ξ(r_s) | 1 - exp(-φ) | 0.8017 |
| D(r_s) | 1/(1+Ξ(r_s)) | 0.555 |
| r*/r_s | Universal intersection | 1.595 |

---

## Verification Checklist

Before any physics code change, verify:

- [ ] z_ssz = z_gr × (1 + Δ(M)/100), NOT 1/D_ssz - 1
- [ ] Xi_weak = r_s/(2r) for weak field
- [ ] Xi_strong = 1 - exp(-φr_s / r) for strong field
- [ ] Δ(M) includes normalization factor
- [ ] φ = 1.618034 (golden ratio)
- [ ] D(r_s) = 0.555 (finite, not zero!)
- [ ] Ξ(r_s) = 0.802

---

## Test Commands

```bash
# Run all physics tests
python -m pytest segcalc/tests/test_ssz_physics.py -v

# Run comprehensive analysis
python comprehensive_analysis.py

# Validate ESO win rate
python test_eso_validation.py
```

---

© 2025 Carmen Wrede & Lino Casu
