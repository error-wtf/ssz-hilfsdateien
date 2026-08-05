# g1/g2 Methodological Framework for SSZ

**For use in scientific papers and academic review**

© 2025 Carmen N. Wrede & Lino P. Casu — Anti-Capitalist Software License v1.4

---

## 1. Epistemic Framework

SSZ (Segmented Spacetime) employs a rigorous two-layer operationalization:

| Layer | Symbol | Definition | Testability |
|-------|--------|------------|-------------|
| **Observable** | g1 | Measurable boundary signatures | Directly testable |
| **Formal** | g2 | Internal state/process space | Indirectly via g1 |

**Core Principle:** We make claims ONLY about g1-observables. g2 remains a formal mathematical construct validated exclusively through its g1-consequences.

---

## 2. Paper-Ready Methods Statement

> *The SSZ framework distinguishes between observable boundary signatures (g1) and the formal internal state space (g2). All empirical claims pertain exclusively to g1-observables—quantities directly accessible through measurement such as time dilation, gravitational redshift, and spectroscopic frequency shifts. The g2 layer constitutes a mathematical model of internal dynamics; its validity is assessed solely through consistency with g1-predictions. This separation ensures methodological rigor without requiring ontological commitments about unobservable interior processes.*

---

## 3. Observable Classification

### 3.1 Timelike Observables (g_tt-based) → Xi Method

| Observable | Formula | Validation |
|------------|---------|------------|
| Time Dilation | D = 1/(1+Ξ) | GPS: 45.7 μs/day ✓ |
| Gravitational Redshift | z = 1/D - 1 | Pound-Rebka: 2.46×10⁻¹⁵ ✓ |
| Frequency Shift | Δf/f = 1 - D | Atomic clocks ✓ |
| Spectroscopic z | z_obs | ESO: 46/47 wins ✓ |

### 3.2 Null-Geodesic Observables → PPN Method

| Observable | Formula | Note |
|------------|---------|------|
| Light Deflection | α = (1+γ)r_s/b | Requires PPN, not Xi alone |
| Shapiro Delay | Δt = (1+γ)r_s/c × ln(...) | Factor 2 from g_tt + g_rr |

**Critical:** Xi-only methods capture g_tt contributions. Null-geodesic observables require PPN formalism to account for spatial metric components.

---

## 4. Regime Boundaries (Canonical segcalc)

| Regime | r/r_s Range | Formula | g1 Status |
|--------|-------------|---------|-----------|
| **Very Close** | < 1.8 | Ξ_strong | Strong predictions |
| **Blended** | [1.8, 2.2] | Hermite C² | Smooth transition |
| **Photon Sphere** | (2.2, 3.0] | Ξ_strong | SSZ optimal (82% wins) |
| **Strong** | (3.0, 10.0] | Ξ_strong | Testable |
| **Weak** | > 10.0 | Ξ = r_s/(2r) | GR-convergent |

**No overlap by design.** Each r/r_s value maps to exactly one regime.

---

## 5. Canonical Constants

| Constant | Value | Precision |
|----------|-------|-----------|
| φ (Golden Ratio) | 1.6180339887 | Exact |
| Ξ(r_s) | 0.8017118 | 7 digits |
| D(r_s) | 0.5550667 | FINITE |
| r*/r_s | 1.594811 | Universal intersection (korrigiert) |

---

## 6. g2 → g1 Mapping

The formal layer (g2) predicts g1-observables through:

```
g2 (Segment Density Ξ) → g1 (Time Dilation D = 1/(1+Ξ))
                       → g1 (Redshift z = 1/D - 1)
                       → g1 (Frequency ν_obs = ν_emit × D)
```

**Validation criterion:** g1-predictions must match experimental data within specified tolerances.

---

## 7. What SSZ Does NOT Claim

1. **No ontological claims about g2:** The internal segment structure is a mathematical model, not a metaphysical assertion.
2. **No QM interpretation dependency:** SSZ is agnostic about quantum interpretations.
3. **No GR replacement in weak field:** For r/r_s > 10, SSZ asymptotically matches GR.

---

## 8. Experimental Validation Summary

| Experiment | g1 Observable | SSZ Prediction | Status |
|------------|---------------|----------------|--------|
| GPS | Time drift | 45.7 μs/day | ✓ |
| Pound-Rebka | Δf/f | 2.46×10⁻¹⁵ | ✓ |
| ESO Spectroscopy | z_obs | 46/47 closer | ✓ |
| S2 Star | Orbit | Consistent | ✓ |

**Combined g1 success rate: 97.9%** (ESO dataset)

---

## References

1. Wrede, C., Casu, L. (2025). *Segmented Spacetime - Mass Projection & Unified Results*.
2. Wrede, C., Casu, L., Bingsi (2025). *Dual Velocities in Segmented Spacetime*.
3. Implementation: `segcalc` Python package, `segmented-calculation-suite` repository.

---

*This document may be cited as methodological reference for SSZ papers.*
