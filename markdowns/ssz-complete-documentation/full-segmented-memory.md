# SSZ Complete Documentation — Full Segmented Memory

**Repo:** github.com/error-wtf/ssz-complete-documentation
**Path:** `E:\clone\ssz-complete-documentation\`
**Authors:** Carmen N. Wrede, Lino P. Casu | AI: Bingsi, Akira
**License:** Anti-Capitalist Software License v1.4
**Stand:** 2026-02-25

---

## 1. WHAT IS SSZ?

Falsifiable GR extension with one additional dimensionless segment density field Ξ(r).
- Core: D_SSZ(r) = 1/(1+Ξ(r))
- At r_s: D=0.555 (finite!) vs GR: D=0 (singular)
- Zero free parameters. φ=1.618 as structural constant
- Mantra: Observable → Class → Method → Scope → Calculate

---

## 2. REPO STRUCTURE (12 sections + BOOKS)

| Section | Files | Content |
|---------|-------|---------|
| 01_OVERVIEW | 4 | ssz_overview, core_postulates, relation_to_gr, authors |
| 02_FOUNDATIONS | 9 | segment_density, regime_definitions, phi_geometry, time_dilation, euler_derivation, emergent_axes, fine_structure, structural_constants, temporal_growth |
| 03_FORMULAS | 5 | formula_compendium, quick_reference, forbidden_formulas, symbol_table, phi_beta_calibration |
| 04_KINEMATICS | 4 | dual_velocities, kinematic_closure, lorentz_v0, frame_dragging |
| 05_ELECTROMAGNETISM | 5 | radial_scaling, redshift, group_velocity, maxwell_rotating, light_travel_time |
| 06_STRONG_FIELD | 6 | black_hole_metric, singularities, cosmic_censorship, dark_star, infalling_matter, superradiance |
| 07_VALIDATION | 5 | test_methodology, gr_vs_ssz_tables, consistency_checks, curvature_detection, nebulae_validation |
| 08_FALSIFICATION | 4 | predictions, falsification_criteria, known_limitations, instruments |
| 09_PAPERS | 3+88 | paper_index, bibliography, preprints + pdf/(24 PDFs) + markdown/(64 MDs) |
| 10_REPOSITORIES | 3 | repo_index (36 repos), reproducibility, test_file_index |
| 11_GUARDRAILS | 4 | prime_directive, method_assignment, cross_repo_rules, confusion_prevention |
| 12_GLOSSARY | 2 | glossary_en, glossary_de |
| BOOKS | 5 | 01_segments_index, SSZ_BOOK_EN.pdf (663p/15.4MB), SSZ_BOOK_DE.pdf (678p/15.3MB), SSZ_COMPLETE_BOOK_EN.md, SSZ_COMPLETE_BOOK_DE.md |

---

## 3. CORE FORMULAS

### Segment Density Ξ(r)
- Weak (r/r_s>10): `Ξ_weak = r_s/(2r)`
- Inner/decay branch (r/r_s<1.8): `Ξ_decay = 1-exp(-φ·r_s/r)`
- Local saturation form (paper/metric-pure context): `Ξ_sat = min(1-exp(-φ · r_s / r), Ξ_max)`
- Blend (1.8-2.2): Hermite C² interpolation
- DEPRECATED/FORBIDDEN: `Ξ = (r_s/r)²·exp(-r/r_φ)` — NEVER USE

### Time Dilation
- `D(r) = 1/(1+Ξ(r))`
- `s(r) = 1+Ξ(r) = 1/D(r)` (scaling factor)
- `z(r) = Ξ(r)` (redshift = segment density)

### Key Values
- Ξ(r_s) = 0.80171, D(r_s) = 0.55503, z(r_s) = 0.80171
- r*/r_s = 1.594811 (decay/global D comparison) or 1.386562 (saturation/local D comparison), both mass-independent
- φ/2 = 0.80902 (coupling factor)
- β = γ = 1 (PPN, exact)

### Kinematic Closure
- v_esc = c·√(r_s/r), v_fall = c·√(r/r_s)
- v_esc × v_fall = c² (universal invariant)

---

## 4. METHOD ASSIGNMENT (PRIME DIRECTIVE)

| Observable Type | Method | Formula |
|----------------|--------|---------|
| Timelike (clocks, redshift) | Ξ-based | D = 1/(1+Ξ) |
| Null (light: lensing, Shapiro) | PPN (1+γ) | result = Ξ_only × 2 |
| Orbit (precession) | PPN (β,γ) | Standard PPN |

**50% of GR for null observables = NOT a bug** → missing PPN (1+γ) factor.

---

## 5. REGIME DEFINITIONS

| Regime | r/r_s | Formula |
|--------|-------|---------|
| very_close | <1.8 | g2 / inner exponential |
| blended | 1.8-2.2 | Hermite C² |
| photon_sphere | 2.2-3.0 | physical photon-sphere regime; current operative branch is g1 |
| strong | 3.0-10.0 | physical strong regime; current operative branch is g1 |
| weak | >10.0 | Ξ_weak |

- 90/110 are PROBE RADII, NOT regime boundaries
- g1→g2 transition is IRREVERSIBLE (coherence-collapse)

---

## 6. STRONG FIELD

### SSZ Metric Tensor
- `ds² = -D²(r)c²dt² + s²(r)dr² + r²dΩ²`
- g_tt(r_s) = -0.308 (finite), g_rr(r_s) = 3.248 (finite)
- No coordinate singularity, no physical singularity
- All curvature invariants finite

### Singularity Resolution
- At r_s: D=0.555 (not 0), z=0.802 (not ∞)
- At r→0: Ξ→0, D→1 (flat spacetime at center)
- No information paradox, no firewall

### Dark Star (replaces Black Hole)
- No event horizon, no singularity
- Light escapes but heavily redshifted (z=0.802)
- BH shadow -1.3% smaller than GR
- Natural boundary: r_φ = (φ/2)·r_s·[1+β·Δ(M)]

### Cosmic Censorship: Trivially satisfied (no singularities to censor)
### Superradiance: Naturally stabilized (bounded Ξ prevents runaway)

---

## 7. VALIDATION & TESTS

### Weak-Field (SSZ ≡ GR, all PASS)
- GPS: 45.85 μs/day, Pound-Rebka: 2.46×10⁻¹⁵
- Mercury: 42.98"/century, Eddington: 1.75"
- Cassini: γ=1.000021±0.000023, S2: z=0.00018

### Strong-Field Predictions (SSZ ≠ GR)
- NS redshift: +13% over GR (NICER 2025-2027)
- Pulsar timing: +30% (NANOGrav 2025-2028)
- BH shadow: -1.3% (ngEHT 2028-2030)
- Shapiro strong-field: +12% (SKA 2028+)

### Test Infrastructure
- Canonical all-tests snapshot: 1296/1296 PASS, 0 failed, 12 executed targets
- Source: `E:\clone\ssz-all-tests\really-full-output.md` (run date 2026-05-07)
- Historical partial summaries such as 171/171, 747+, 801+, and 835 pass are superseded by the all-tests snapshot
- Anti-circularity enforced: M→r_s→Ξ→D→Observable (one-directional)

### Falsification Criteria (SSZ is WRONG if):
1. NS redshift ≠ z_SSZ ± 5%
2. r*/r_s is inconsistent with the declared Xi-form comparison
3. BH shadow inconsistent with D(r_s)=0.555
4. Pulsar timing ≠ Δt_SSZ ± 10%

---

## 8. REPOSITORIES (36 total)

### SSZ/Physics (18 repos)
| Repo | Tests | Scope |
|------|-------|-------|
| segmented-calculation-suite | 158 | All regimes, core engine |
| Unified-Results | 147 | 25 test suites and unified framework |
| ssz-qubits | 184 | Weak field (GPS, PR, S2), qubit applications |
| frequency-curvature-validation | 82 | PPN, Shapiro, lensing |
| ssz-lensing | 279 | Gravitational lensing |
| ssz-metric-pure | 36 | 4D tensors, Einstein eq. |
| ssz-schumann | 178 | Schumann resonance |
| g79-cygnus-tests | 5 | G79 LBV nebula |
| ssz-lagrange | 54 | Lagrange, Kerr, quantum |
| segmented-energy | 7 | 129 astronomical objects |
| ssz-trajectories | 63 | Geodesic trajectory integration |
| chord-partition (local) | 103 | Eigenmodes and phi resonance |
| + archives/reference | — | paper plots, starmaps, metric-final, full-metric, emergent, SEGMENTED_SPACETIME, docs, LIGO |

### Other: 2 math, 3 research, 3 tools, 8 web, 2 private

---

## 9. PAPERS (25 primary + 7 additional)

01-Radial Scaling Gauge, 02-Dual Velocities, 03-Frequency Framework,
04-BH Metric, 05-Infalling Matter, 06-Euler Derivation,
07-Kinematic Closure, 08-Group Velocity, 09-Dark Star,
10-Curvature Detection, 11-Nebulae, 12-Superradiance,
13-π and φ, 14-Emergent Axes, 15-Fine-Structure Constant,
16-Singularities, 17-Cosmic Censorship, 18-φ/2 Calibration,
19-Lorentz v=0, 20-Temporal Growth, 21-Redshift,
22-Maxwell Rotating, 23-Light-Travel Time, 24-Frame Dragging,
25-Coherence-Collapse Law

All available as PDF (09_PAPERS/pdf/) and MD (09_PAPERS/markdown/).

---

## 10. GUARDRAILS (Confusion Prevention)

### 5 Common False Alarms
1. **50% of GR** → Missing PPN (1+γ), not a bug
2. **r* mismatch (1.387 vs 1.595)** → Different Ξ forms, both correct
3. **Ξ values differ between repos** → Different scopes (weak vs strong)
4. **D_SSZ ≠ D_GR** → That's the entire point of SSZ
5. **Energy not conserved** → Use multiplicative, not additive accounting

### Repo Scope Index
| Repo | Scope | Ξ Formula | PPN? |
|------|-------|-----------|------|
| ssz-qubits | Weak | r_s/(2r) | NO |
| ssz-metric-pure | Strong | min(1-exp(-φr_s / r), Ξ_max) | YES |
| maxwell | Blend | Hermite C² | YES |
| Unified-Results | All | Full | YES |

---

## 11. BOOKS

| Edition | Pages | Size | Format |
|---------|-------|------|--------|
| EN PDF | 663 | 15.4 MB | SSZ_BOOK_EN.pdf |
| DE PDF | 678 | 15.3 MB | SSZ_BOOK_DE.pdf |
| EN MD | — | ~970 KB | SSZ_COMPLETE_BOOK_EN.md |
| DE MD | — | ~1.1 MB | SSZ_COMPLETE_BOOK_DE.md |

9 Parts, 32 Chapters + 7 Appendices (A-G).
Built with Pandoc 3.9 + LuaLaTeX (MiKTeX).

---

## 12. KEY CONSTANTS

```
φ = 1.6180339887498948    c = 299792458 m/s
G = 6.67430e-11 m³/(kg·s²)  ℏ = 1.054571817e-34 J·s
M☉ = 1.98892e30 kg       r_s = 2GM/c²
Ξ_max = 0.80171           D_min = 0.55503
```

---

## 13. ELECTROMAGNETISM

- Scaling factor: s(r) = 1+Ξ(r) = effective refractive index
- E'=s·E, B'=s·B (fields stronger in high-Ξ regions)
- Maxwell: ∇·(s²E)=0, wave eq includes s·s' term
- Light-travel: Δt_total = Δt_flat + ∫Ξ(r)dr/c
- Shapiro: Δt = (1+γ)(r_s/c)ln(4r₁r₂/d²) — always distinguish one-way vs round-trip

---

## 14. GLOSSARY HIGHLIGHTS

- **Dark Star:** SSZ replacement for black hole (no singularity, no horizon)
- **Natural Boundary:** r_φ = (φ/2)·r_s·[1+β·Δ(M)]
- **Coherence-Collapse:** Irreversible g1→g2 transition
- **Anti-Circularity:** Never calibrate against predicted data
- **Hermite C²:** Quintic interpolation ensuring Ξ, dΞ/dr, d²Ξ/dr² continuity
- **Δ(M):** Mass-dependent correction: A·exp(-α/M^B), from φ-geometry

---

*This file is the complete analytical summary of all 50+ documentation files in ssz-complete-documentation.*
