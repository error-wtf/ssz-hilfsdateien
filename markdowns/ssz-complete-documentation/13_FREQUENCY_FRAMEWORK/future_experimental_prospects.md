# Future Experimental Prospects

**Book reference:** Ch 17 (Future Experimental Prospects section)  
**Related:** Ch 33 (Observational Roadmap), Ch 34 (Conclusion)

---

## Summary

SSZ makes **quantitative, falsifiable predictions** that differ from GR in specific regimes. The table below shows predicted SSZ-GR deviations organized by observable and required precision.

## SSZ vs GR Prediction Table

| Observable | SSZ Prediction | GR Prediction | Deviation | Status |
|-----------|---------------|---------------|-----------|--------|
| GPS time correction | +38.45 μs/day | +38.4 μs/day | <0.1% | **Confirmed** |
| Mercury precession | 42.98"/century | 42.98"/century | 0% | **Confirmed** |
| Solar Shapiro delay | 262 μs | 264 μs | 0.8% | **Confirmed** |
| PPN gamma | 1.0000 | 1.0000 | 0% | **Confirmed** |
| NS surface redshift (R=12km) | z = 0.173 | z = 0.236 | -27% | Testable |
| BH shadow diameter | 1.3% smaller | baseline | -1.3% | Testable |
| QNM ringdown frequency | 39% higher | baseline | +39% | Future |
| QNM damping time | 39% longer | baseline | +39% | Future |
| Frequency curvature d^2D/dr^2 | 4x larger | baseline | +300% | Future |
| Penrose efficiency (max spin) | 21.4% | 20.71% | +3% | Future |

## Experimental Timeline

### Now (2024-2026): Optical Clocks

**NIST/PTB optical lattice clocks** can measure gravitational redshift to 10^-18 level.

- **Experiment:** Two clocks separated by 1 m in height, measure frequency curvature
- **SSZ prediction:** kappa = 3.4e-25 m^-1 (4x GR)
- **Required clock network:** 3 clocks at 10 km altitude separation (achievable with satellites)
- **Feasibility:** Near-term with ACES/STE-QUEST type missions

### 2025-2030: Event Horizon Telescope (EHT)

**Black hole shadow diameter test:**

```
SSZ shadow / GR shadow = [D_SSZ(r_photon) / D_GR(r_photon)]^{-1} ≈ 0.987 (-1.3%)
```

- **Current EHT precision:** ~15% (M87*, Sgr A*)
- **Next-generation EHT (ngEHT, 2027):** ~3% precision
- **Required for SSZ test:** <1.3% → available ~2030
- **Target:** Sgr A* (best constrained BH mass)

### 2027-2030: NICER / eXTP (Neutron Stars)

**Neutron star surface redshift:**

```
z_SSZ = 0.173  vs  z_GR = 0.236   (for M=1.4M_sun, R=12km)
```

- **NICER (operational):** δz ~ 0.05 (marginal)
- **eXTP (2027):** δz ~ 0.02 (**confirms or rules out SSZ at 3 sigma**)
- **Athena (2035):** δz ~ 0.01 (definitive 5+ sigma)
- **Target:** EXO 0748-676, SAX J1748, 4U 1820-30

### 2030-2035: Einstein Telescope / Cosmic Explorer

**Gravitational wave QNM frequencies:**

```
f_QNM_SSZ / f_QNM_GR = 1.39   (+39%)
```

- **Current LIGO:** QNM test uncertain (SNR limited)
- **Einstein Telescope / Cosmic Explorer (2030s):** QNM frequency to 1% precision
- **Required for SSZ test:** <39% → ET/CE easily achieves this
- **Target:** Stellar-mass BH mergers at 100 Mpc

### 2034-2038: LISA

**Millihertz gravitational waves and BH ringdown:**

- **LISA:** QNM tests for SMBH mergers (10^6 - 10^9 M_sun)
- **QNM frequency shift at 10 Mpc:** 39% (easily measurable at this SNR)
- **Also:** Holonomy deviation measurement during Galactic binary evolution
- **Target:** SMBH mergers detected at cosmological distances

### 2035+: Athena X-ray Observatory

**Neutron star atmosphere spectroscopy:**

- **Athena:** X-ray calorimeter with resolving power E/δE > 3000
- **Measurement:** Iron K-alpha emission from NS surface
- **Precision:** δz ~ 0.005 (definitive)
- **Outcome:** SSZ vs GR discriminated at >10 sigma for compact NSs

## Falsification Protocol

SSZ is **falsified** if ANY of:

```
1. NS surface redshift measured z > 0.20 for M=1.4, R=12km NS   [rules out SSZ, confirms GR]
2. BH shadow diameter within 0.5% of GR prediction              [rules out SSZ]
3. QNM frequency within 5% of GR prediction for known-mass BH   [rules out SSZ]
4. gamma measured != 1 at 5-sigma                                [rules out BOTH]
```

SSZ is **confirmed** if ALL of:

```
1. NS surface redshift measured z < 0.19 for M=1.4, R=12km NS
2. BH shadow 1-2% smaller than GR prediction
3. QNM frequency 30-45% higher than GR prediction
```

## Why SSZ Predictions are Conservative

All SSZ predictions listed above are for **canonical parameters** (M=1.4 M_sun, R=12 km for NS; Schwarzschild metric for BH). The actual deviations could be larger if:

1. NS equations of state give smaller R (more compact)
2. BH spin is near maximal (larger ergosphere effect)
3. The blend zone transitions at a different radius than assumed

SSZ makes minimum predictions; nature may show larger deviations.

## Relation to Other Sections

- [Neutron Star Redshift](../07_VALIDATION/neutron_star_redshift.md) — NS test details
- [QNM Spectrum](../06_STRONG_FIELD/qnm_spectrum.md) — ringdown predictions
- [Black Hole Metric](../06_STRONG_FIELD/black_hole_metric.md) — shadow calculation
- [Holonomy Invariants](holonomy_invariants.md) — LISA holonomy
- [Frequency Curvature](frequency_curvature.md) — optical clock experiment
- [Falsification Criteria](../08_FALSIFICATION/falsification_criteria.md) — formal falsification conditions
- [Instruments](../08_FALSIFICATION/instruments.md) — detailed instrument specs
