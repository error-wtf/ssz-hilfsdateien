# SSZ Predictions

**Status:** CANONICAL

---

## Category 1: Confirmed Predictions (SSZ ≡ GR)

SSZ reproduces all confirmed GR weak-field results:

| Prediction | Value | Confirmed by |
|-----------|-------|--------------|
| GPS time correction | 45.85 μs/day | US Naval Observatory |
| Pound-Rebka redshift | Δν/ν = 2.46×10⁻¹⁵ | Pound & Rebka (1960) |
| Mercury perihelion | 42.98"/century | Observations |
| Eddington lensing | 1.75" | Eddington (1919) |
| Cassini Shapiro γ | 1 (exact) | Bertotti et al. (2003) |
| S2 Schwarzschild precession | Confirmed | GRAVITY/ESO (2020) |

---

## Category 2: Testable Predictions (SSZ ≠ GR)

### Neutron Star Redshift (+13%)
```
z_SSZ = z_GR + 13%  (systematic excess)
```

Specific objects:
| Object | z_GR | z_SSZ | Testable with |
|--------|------|-------|---------------|
| PSR J0030+0451 | 0.219 | 0.328 | NICER |
| PSR J0740+6620 | 0.346 | 0.413 | NICER |
| PSR J0348+0432 | 0.380 | 0.457 | XMM-Newton |

**Timeline:** 2025–2027 (NICER data releases)

### Pulsar Timing Delay (+30%)
```
Δt_SSZ = Δt_GR + 30%  (strong-field Shapiro enhancement)
```
**Timeline:** 2025–2028 (NANOGrav)

### Black Hole Shadow (-1.3%)
```
d_SSZ = d_GR - 1.3%  (slightly smaller shadow)
```
**Timeline:** 2028–2030 (next-generation EHT)

### Shapiro Delay Strong-Field (+12%)
```
Δt_SSZ = Δt_GR + 12%  (near compact objects)
```
**Timeline:** 2028+ (SKA)

### Universal Intersection Point
```
r*/r_s = 1.594811  (decay/global D comparison)
r*/r_s = 1.386562  (saturation/local D comparison)
```
**Timeline:** Indirect, via NS observations. The test must declare which Xi form and observable mapping is being used before comparison.

### Finite Horizon Values
```
D(r_s) = 0.555  (not 0)
z(r_s) = 0.802  (not ∞)
```
**Timeline:** Indirect, via gravitational wave ringdown (LISA, 2034+)

---

## Category 3: Specific Object Predictions

### G79.29+0.46 LBV Nebula
- Temperature and velocity diagnostics are exploratory and reproducible
- Current all-tests: 5/5 executed checks PASS, with parsec-conversion warning noted
- Repository: g79-cygnus-tests

### Cygnus X-1
- Modified X-ray timing predictions
- Strong-field redshift enhancement
- Repository: g79-cygnus-tests

### 13 Astronomical Objects
- Validated in maxwell test suite (45/45 PASS)
- Consistent across object classes

---

© 2025–2026 Carmen N. Wrede, Lino P. Casu
