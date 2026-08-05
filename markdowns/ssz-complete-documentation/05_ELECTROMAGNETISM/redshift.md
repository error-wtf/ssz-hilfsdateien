# Gravitational Redshift

**Status:** CANONICAL
**Paper:** 21 — Interpretation of Gravitational Redshift

---

## SSZ Redshift Formula

The gravitational redshift between two observers:
```
1 + z = D(r_obs) / D(r_emit) = (1 + Ξ_emit) / (1 + Ξ_obs)
```

For an observer at infinity (Ξ_obs → 0):
```
z(r) = 1/D(r) - 1 = Ξ(r)
```

**The redshift equals the segment density!** This is a clean, direct correspondence.

---

## Comparison with GR

```
z_GR(r)  = 1/√(1-r_s/r) - 1
z_SSZ(r) = Ξ(r)
```

### Weak Field (identical)
```
z_GR  ≈ r_s/(2r)
z_SSZ = Ξ_weak = r_s/(2r)
```

### Strong Field (different)
```
z_GR(r_s)  = ∞
z_SSZ(r_s) = 0.802 (finite!)
```

---

## Neutron Star Redshifts (TESTABLE)

| Object | M/M☉ | R (km) | r/r_s | z_GR | z_SSZ | Excess |
|--------|-------|--------|-------|------|-------|--------|
| PSR J0030+0451 | 1.44 | 13.02 | 3.06 | 0.219 | 0.328 | **+50%** |
| PSR J0740+6620 | 2.08 | 13.70 | 2.23 | 0.346 | 0.413 | **+19%** |
| PSR J0348+0432 | 2.01 | 12.50 | 2.10 | 0.380 | 0.457 | **+20%** |
| Hypothetical NS | 2.5 | 11.0 | 1.49 | 0.580 | 0.652 | **+12%** |

**Systematic prediction: NS redshift +13% higher than GR.** Testable with NICER.

---

## φ-Frequency Grid

SSZ predicts a discrete frequency scaling:
```
R = 1 + z = φ^N,    N ∈ ℤ
```

This φ-grid is not a quantization of redshift but a preferred scaling at which segmentation effects align constructively.

---

## Curvature Detection via Frequency Comparison

Paper 10 introduces a curvature detection method using three-frequency comparison:
```
δ_AB = ln(ν_A / ν_B)
I_ABC = δ_AB + δ_BC + δ_CA

I_ABC = 0 → Flat spacetime
I_ABC ≠ 0 → Curved spacetime (segmented)
```

This provides a model-independent test for spacetime segmentation.

---

## Tests

| Test | Repository |
|------|------------|
| test_redshift.py | ssz-qubits |
| test_validation.py (GPS, PR, S2) | ssz-qubits |

---

© 2025–2026 Carmen N. Wrede, Lino P. Casu
