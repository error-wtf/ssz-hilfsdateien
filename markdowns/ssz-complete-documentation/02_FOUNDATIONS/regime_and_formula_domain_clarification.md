# Regime Boundaries vs. Formula Domains — Canonical Clarification

**Status:** CANONICAL  
**Book reference:** Ch 5b (Regime Boundaries, Formula Domains, and Misunderstanding Prevention)

---

## The Two Boundary Systems

SSZ uses two distinct boundary systems that must not be conflated:

### System 1: Formula Domains (Operative N-Segmentation Mapping)

These boundaries determine **which formula** is used to compute Ξ:

| Domain | r/rₛ range | Formula | Details |
|--------|-----------|---------|---------|
| g₁ domain | above 2.2 | Ξ = rₛ/(2r) | See [segment\_density.md](segment_density.md) §Weak-Field |
| Blend zone | 1.8 to 2.2 | Hermite C² interpolation | See [segment\_density.md](segment_density.md) §Blend Zone |
| g₂ domain | below 1.8 | Ξ = min(1−exp(−φ·r/rₛ), Ξ\_max) | See [segment\_density.md](segment_density.md) §Strong-Field |

### System 2: Physical Regimes (Interpretive Classification)

These boundaries classify the **physical environment**:

| Regime | r/rₛ range | Physical context | Ξ formula used |
|--------|-----------|-----------------|----------------|
| very\_close | below 1.8 | At/near horizon | g₂ (strong) |
| blended | 1.8 to 2.2 | Smooth transition | Hermite C² |
| photon\_sphere | 2.2 to 3.0 | Photon orbit zone | g₁ (weak) |
| strong | 3.0 to 10.0 | Neutron stars, compact objects | g₁ (weak) |
| weak | above 10.0 | Solar System, GPS, stars | g₁ (weak) |

For full regime definitions see [regime\_definitions.md](regime_definitions.md).

### The Key Difference

In the range 2.2 < r/rₛ < 10, the g₁ formula is used operatively, but the physical regime is "strong" or "photon\_sphere".

> **"g₁ formula for x > 2.2" does NOT mean "everything above 2.2 is weak field".**
>
> It means: "For computing Ξ, the g₁ branch is used above 2.2 because it provides the physically correct approximation there."

---

## Numerical Evidence

The **Δ** column shows the absolute difference between g₁ and g₂ — proving that the formula choice is physically decisive, not cosmetic.

| r/rₛ | Ξ\_g1 | Ξ\_g2 | Ξ operative | D operative | Regime | Formula | Δ (g1−g2) |
|------:|-------:|-------:|------------:|------------:|:-------|:--------|----------:|
| 0.5 | 1.000000 | 0.554704 | 0.554704 | 0.643209 | very\_close | g₂ | 0.445 |
| 1.0 | 0.500000 | 0.801712 | 0.801712 | 0.555028 | very\_close | g₂ | 0.302 |
| 1.8 | 0.277778 | 0.801712 | 0.277778 | 0.782609 | blended | blend | 0.524 |
| 2.2 | 0.227273 | 0.801712 | 0.801712 | 0.555028 | blended | blend | 0.574 |
| 3.0 | 0.166667 | 0.801712 | 0.166667 | 0.857143 | photon\_sphere | g₁ | 0.635 |
| 5.0 | 0.100000 | 0.801712 | 0.100000 | 0.909091 | strong | g₁ | 0.702 |
| 10.0 | 0.050000 | 0.801712 | 0.050000 | 0.952381 | strong | g₁ | 0.752 |
| 100.0 | 0.005000 | 0.801712 | 0.005000 | 0.995025 | weak | g₁ | 0.797 |

**Key result:** At r = rₛ, using g₁ would give D = 0.667 instead of the correct D = 0.555 — a **17% error**.

All values verified across three independent repositories:
- [segmented-calculation-suite](https://github.com/error-wtf/segmented-calculation-suite) — analytical reference
- [ssz-metric-pure](https://github.com/error-wtf/ssz-metric-pure) — independent implementation
- [ssz-qubits](https://github.com/error-wtf/ssz-qubits) — quantum corrections

Cross-repository consistency: < 10⁻¹⁵ for all Ξ values. See [special\_values.md](../03_FORMULAS/special_values.md).

---

## Saturation Form vs. Decay Form

Two variants of the strong-field formula exist. Only the saturation form is operative:

| Property | Saturation (operative) | Decay (didactic only) |
|----------|----------------------|----------------------|
| Formula | Ξ = min(1−exp(−φ·r/rₛ), Ξ\_max) | Ξ = 1−exp(−φ·rₛ/r) |
| r → 0 | Ξ → 0 (regular) | Ξ → 1 (saturates) |
| r → ∞ | Ξ → Ξ\_max ≈ 0.802 | Ξ → 0 (decays) |
| r = rₛ | Ξ = 0.802 | Ξ = 0.802 |
| Status | **CANONICAL** | Didactic/complementary |

Both agree exactly at r = rₛ but differ in asymptotic limits. See [forbidden\_formulas.md](../03_FORMULAS/forbidden_formulas.md) for deprecated variants.

---

## Two-Layer Coherence Collapse Clarification

SSZ distinguishes two conceptually different processes:

**Layer 1 — Spacetime regime assignment (irreversible):**
Once a spatial region acquires g₂ segmentation (e.g., by gravitational collapse), the regime label is permanent. The spacetime does not "un-segment." g₂ → g₁ is **FORBIDDEN** for spacetime regions.

**Layer 2 — Matter/radiation transport through regimes (physical process):**
Matter and radiation CAN physically move from a g₂ region outward into g₁ space (e.g., supernova, merger ringdown). When this happens, the coherence structure collapses irreversibly — ΔS\_seg > 0 always.

The Layer 2 process is NOT the reversal of Layer 1. It is a distinct entropy-producing process analogous to melting. Full details: [coherence\_collapse.md](coherence_collapse.md) and [regime\_definitions.md](regime_definitions.md).

---

## Common Misunderstandings

1. **"Ξ = rₛ/(r−rₛ) is the canonical SSZ formula."** — WRONG. This formula gives D(rₛ)=0, contradicting D\_min=0.555. It is [FORBIDDEN](../03_FORMULAS/forbidden_formulas.md).

2. **"Above r/rₛ > 2.2, everything is weak field."** — WRONG. Above 2.2 the g₁ *formula* is used; the physical *regime* is only "weak" above 10.

3. **"The blend zone is a numerical trick."** — WRONG. The [Hermite C² interpolation](segment_density.md) is the unique connection guaranteeing continuity of Ξ, dΞ/dr, and d²Ξ/dr².

4. **"Lensing and Shapiro delay use the Ξ formula."** — WRONG. They use [PPN with γ=1](../03_FORMULAS/ppn_formulas.md). Ξ modifies only g\_tt; lensing/Shapiro also depend on g\_rr.

5. **"Coherence collapse means g₂ → g₁."** — PARTIALLY WRONG. See the two-layer clarification above. Spacetime regime: g₁→g₂ irreversible. Matter transport: g₂→g₁ is the coherence collapse (Layer 2).

6. **"90/110 are regime boundaries."** — WRONG. They are [probe radii](regime_definitions.md) for continuity checks, not physical thresholds. The actual boundaries are 1.8 and 2.2.

---

## Cross-References

### Within this repository

- [segment\_density.md](segment_density.md) — Ξ(r): weak, strong, blend formulas
- [time\_dilation.md](time_dilation.md) — D(r) = 1/(1+Ξ), comparison with GR
- [scaling\_factor.md](scaling_factor.md) — s(r) = 1+Ξ = 1/D
- [regime\_definitions.md](regime_definitions.md) — 5 regimes, mandatory regime check, two-layer clarification
- [coherence\_collapse.md](coherence_collapse.md) — g₁→g₂ irreversible transition
- [phi\_geometry.md](phi_geometry.md) — Golden ratio as structural constant
- [intersection\_invariance.md](intersection_invariance.md) — r\*/rₛ = 1.387, mass-independent
- [energy\_conditions.md](energy_conditions.md) — WEC/DEC/SEC in SSZ
- [formula\_compendium.md](../03_FORMULAS/formula_compendium.md) — Complete formula list
- [special\_values.md](../03_FORMULAS/special_values.md) — Ξ(rₛ)=0.802, D(rₛ)=0.555
- [ppn\_formulas.md](../03_FORMULAS/ppn_formulas.md) — PPN γ=1, lensing, Shapiro (CRITICAL)
- [forbidden\_formulas.md](../03_FORMULAS/forbidden_formulas.md) — Deprecated/wrong formulas
- [quick\_reference.md](../03_FORMULAS/quick_reference.md) — Top-10 formulas on one page

### Repositories

- [segmented-calculation-suite](https://github.com/error-wtf/segmented-calculation-suite) — Ξ, D, Regime, C²-Blend
- [ssz-metric-pure](https://github.com/error-wtf/ssz-metric-pure) — 4D-Tensor, Einstein/Ricci
- [ssz-qubits](https://github.com/error-wtf/ssz-qubits) — GPS, Pound-Rebka, S2
- [Unified Results](https://github.com/error-wtf/Segmented-Spacetime-Mass-Projection-Unified-Results) — 25 test suites

---

© 2025–2026 Carmen N. Wrede, Lino P. Casu
