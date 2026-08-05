# Canonical SSZ Reference

**Source:** https://github.com/error-wtf/ssz-complete-documentation  
**Status:** Single Source of Truth for SSZ  
**Date Synced:** 2026-06-09  

---

## Core SSZ Formulas (Canonical)

### Central Quantity
```
Ξ(r) = dimensionless segment density field
```

### Key Formula
```
D_SSZ(r) = 1 / (1 + Ξ(r))
s(r) = 1 + Ξ(r) = 1 / D_SSZ(r)
```

### Horizon Values (Critical!)
```
Ξ(r_s) = 1 - exp(-φ) ≈ 0.801711847...
D(r_s) ≈ 0.555027709...
```

**⚠️ WARNING:** Never use Ξ(r_s) = 1 as canonical horizon value. The correct value is ≈0.8017.

---

## Regime Branches

### Weak-Field Branch
```
Ξ_weak(r) = r_s / (2r)
Valid for: r/r_s > 2.2
```

### Strong/Inner Branch
```
Ξ_strong(r) = 1 - exp(-φ * r_s / r)
Valid for: r_s/r < 1.8
φ = 0.20898764024997873... (SSZ scaling constant)
```

### Blend Zone
```
1.8 ≤ r/r_s ≤ 2.2
Use C² Hermite/quintic interpolation
Status: BLEND_PENDING if not fully implemented
```

---

## Regime Boundaries

| Regime | r/r_s Range | Ξ Characteristic |
|--------|-------------|------------------|
| very_close | < 1.8 | strong field, exp form |
| blended | 1.8 – 2.2 | interpolation zone |
| photon_sphere | 2.2 – 3.0 | transition |
| strong | 3.0 – 10.0 | weak field valid |
| weak | > 10.0 | asymptotic |

---

## Prime Directive

**Observable → Class → Method → Scope → Then calculate.**

### Observable Method Assignment

#### NULL / Light-Path Observables
**Method:** PPN Completion  
**Formula:** result = Ξ-only × (1+γ)  
**For GR-equivalent:** γ=1, factor 2  

**Examples:**
- Lensing
- Shapiro delay
- VLBI / group delay
- Light time delay
- Interferometry

#### TIMELIKE STATIC / Clock Observables
**Method:** Ξ Direct  
**Formula:** D(r) = 1/(1+Ξ)  

**Examples:**
- Gravitational redshift
- Time dilation
- GPS
- Pound-Rebka

#### TIMELIKE ORBIT Observables
**Method:** PPN Orbit Machinery  
**Not:** Ξ-only shortcuts

**Examples:**
- Perihelion advance
- Precession
- Frame dragging

---

## Deprecated Formula Ban

### ❌ HARD FAIL - Never Use:
```
Ξ = (r_s/r)^2 * exp(-r/r_phi)
```

### ⚠️ Toy Only - Not Canonical:
```
Ξ = r_s/r  (normalized toy model)
Ξ(r_s) = 1  (incorrect horizon value)
```

**Allowed contexts for toy formulas:**
- Explicitly marked toy proxy tests
- Legacy/historical archive
- Normalized simplified models with clear disclaimer

---

## Scope Limitations

### What SSZ Provides:
- Mathematical scaffold for segmented spacetime
- Geometric consistency checks
- Observable prediction framework
- Falsification criteria

### What SSZ Does NOT Claim:
- ❌ Physical metric generation mechanism solved
- ❌ Engineering feasibility established
- ❌ Biological transport validated
- ❌ Experimental validation achieved
- ❌ Nonlinear stability proven

---

## Validation Checklist

### Canonical Tests Required:
- [ ] Ξ_weak(10*r_s) = 0.05
- [ ] Ξ_weak(100*r_s) = 0.005
- [ ] Ξ_strong(r_s) = 0.801711847
- [ ] D(r_s) = 0.555027709
- [ ] s(r_s) = 1.801711847
- [ ] Ξ decreases monotonically with r in each branch
- [ ] Deprecated formula detection
- [ ] Method assignment correctness

---

## Version Alignment

**Current Version:** 1.1.0  
**Name:** SSZ-HOW-TO-BEAM v1.1.0 — Canonical SSZ Alignment  

This version implements canonical SSZ formulas from ssz-complete-documentation.

---

## References

1. **Primary Source:** https://github.com/error-wtf/ssz-complete-documentation
2. **Authors:** Carmen N. Wrede, Lino P. Casu
3. **License:** Anticapitalist Software License 1.4
