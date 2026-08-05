# Segmented Spacetime (SSZ) — Complete Documentation

**Authors:** Carmen N. Wrede, Lino P. Casu
**AI Assistants:** Bingsi, Akira
**Status:** Canonical Reference — Single Source of Truth
**Last Updated:** 2026-05-19 (long-baseline replication + reproducibility critique added)

---

## What is SSZ?

Segmented Spacetime (SSZ) is a falsifiable extension of General Relativity (GR) built around a single additional quantity: a **dimensionless segment density field Ξ(r)**. SSZ reproduces GR exactly in weak fields while producing systematic, testable deviations in strong fields — especially around neutron stars and compact objects.

**Core equation:**
```
D_SSZ(r) = 1 / (1 + Ξ(r))
```

At the Schwarzschild radius: **D(r_s) = 0.555** (finite!) vs GR: D(r_s) = 0 (singularity).

---

## Documentation Structure

| # | Section | Contents |
|---|---------|----------|
| 01 | [Overview](01_OVERVIEW/) | What is SSZ, core postulates, relation to GR |
| 02 | [Foundations](02_FOUNDATIONS/) | Ξ(r), D(r), regimes, φ-geometry, φ-lattice, scaling factor |
| 03 | [Formulas](03_FORMULAS/) | Complete compendium, PPN, worked examples, special values, units |
| 04 | [Kinematics](04_KINEMATICS/) | Dual velocities, geodesics, orbital mechanics, frame dragging |
| 05 | [Electromagnetism](05_ELECTROMAGNETISM/) | Maxwell gauge, group velocity, energy, Shapiro delay, lensing |
| 06 | [Strong Field](06_STRONG_FIELD/) | BH metric, singularities, ISCO, QNM, Penrose, Lagrangian |
| 07 | [Validation](07_VALIDATION/) | GPS, Cassini, Mercury, NS redshift, power law, GR vs SSZ |
| 08 | [Falsification](08_FALSIFICATION/) | Testable predictions, instruments, falsification criteria |
| 09 | [Papers](09_PAPERS/) | All 25 papers, bibliography, preprints |
| 10 | [Repositories](10_REPOSITORIES/) | All 35 repos, test index, reproducibility |
| 11 | [Guardrails](11_GUARDRAILS/) | Prime directive, method assignment, confusion prevention |
| 12 | [Glossary](12_GLOSSARY/) | EN/DE terminology |
| 13 | [Frequency Framework](13_FREQUENCY_FRAMEWORK/) | Holonomy invariants, frequency curvature, experimental prospects |

---

## Complete File Index

### 01_OVERVIEW
- [ssz_overview.md](01_OVERVIEW/ssz_overview.md) — What is SSZ, executive summary
- [core_postulates.md](01_OVERVIEW/core_postulates.md) — The 5 core postulates
- [relation_to_gr.md](01_OVERVIEW/relation_to_gr.md) — How SSZ relates to GR
- [authors.md](01_OVERVIEW/authors.md) — Carmen N. Wrede, Lino P. Casu

### 02_FOUNDATIONS
- [segment_density.md](02_FOUNDATIONS/segment_density.md) — Xi(r): weak, strong, blend formulas
- [time_dilation.md](02_FOUNDATIONS/time_dilation.md) — D(r) = 1/(1+Xi)
- [scaling_factor.md](02_FOUNDATIONS/scaling_factor.md) — s(r) = 1+Xi = 1/D
- [regime_definitions.md](02_FOUNDATIONS/regime_definitions.md) — 5 regimes, transition radii, two-layer coherence collapse clarification
- [regime_and_formula_domain_clarification.md](02_FOUNDATIONS/regime_and_formula_domain_clarification.md) — Formula domains vs physical regimes, numerical table, 6 common misunderstandings
- [phi_geometry.md](02_FOUNDATIONS/phi_geometry.md) — Golden ratio in SSZ
- [phi_lattice_discretization.md](02_FOUNDATIONS/phi_lattice_discretization.md) — φ-lattice x_k=φ^k, bracket theorem, QNM connection
- [intersection_invariance.md](02_FOUNDATIONS/intersection_invariance.md) — two mass-independent r*/r_s comparisons: 1.594811 and 1.386562
- [coherence_collapse.md](02_FOUNDATIONS/coherence_collapse.md) — g1→g2 irreversible transition
- [energy_conditions.md](02_FOUNDATIONS/energy_conditions.md) — WEC/DEC/SEC/NEC in SSZ, SEC violation
- [emergent_axes.md](02_FOUNDATIONS/emergent_axes.md) — Emergent coordinate axes
- [euler_derivation.md](02_FOUNDATIONS/euler_derivation.md) — Euler identity connection
- [fine_structure.md](02_FOUNDATIONS/fine_structure.md) — alpha = 1/137 derivation
- [structural_constants.md](02_FOUNDATIONS/structural_constants.md) — phi, alpha_SSZ, r*/r_s
- [temporal_growth.md](02_FOUNDATIONS/temporal_growth.md) — Temporal growth rate

### 03_FORMULAS
- [formula_compendium.md](03_FORMULAS/formula_compendium.md) — Complete formula list with origin + domain
- [quick_reference.md](03_FORMULAS/quick_reference.md) — Top-10 formulas on one page
- [symbol_table.md](03_FORMULAS/symbol_table.md) — All symbols defined
- [ppn_formulas.md](03_FORMULAS/ppn_formulas.md) — PPN gamma=1, lensing, Shapiro — **CRITICAL**
- [worked_examples.md](03_FORMULAS/worked_examples.md) — Cassini, Mercury, GPS, NS calculations
- [unit_conversion_table.md](03_FORMULAS/unit_conversion_table.md) — SI/CGS/Natural units
- [special_values.md](03_FORMULAS/special_values.md) — Xi(r_s)=0.80171, D(r_s)=0.55503, r*/r_s, phi-table
- [phi_beta_calibration.md](03_FORMULAS/phi_beta_calibration.md) — Calibration curves
- [forbidden_formulas.md](03_FORMULAS/forbidden_formulas.md) — Deprecated/wrong formulas to avoid

### 04_KINEMATICS
- [dual_velocities.md](04_KINEMATICS/dual_velocities.md) — v_coord vs v_physical
- [lorentz_v0.md](04_KINEMATICS/lorentz_v0.md) — Lorentz factor at v=0
- [kinematic_closure.md](04_KINEMATICS/kinematic_closure.md) — Kinematic closure condition
- [frame_dragging.md](04_KINEMATICS/frame_dragging.md) — Lense-Thirring, Gravity Probe B
- [geodesics.md](04_KINEMATICS/geodesics.md) — Geodesic equations, radial free-fall
- [orbital_mechanics.md](04_KINEMATICS/orbital_mechanics.md) — ISCO, photon sphere, effective potential

### 05_ELECTROMAGNETISM
- [radial_scaling.md](05_ELECTROMAGNETISM/radial_scaling.md) — Radial scaling gauge for Maxwell fields
- [group_velocity.md](05_ELECTROMAGNETISM/group_velocity.md) — Group velocity in segment lattice
- [light_travel_time.md](05_ELECTROMAGNETISM/light_travel_time.md) — Additive travel time correction
- [maxwell_rotating.md](05_ELECTROMAGNETISM/maxwell_rotating.md) — Maxwell equations in rotating SSZ
- [redshift.md](05_ELECTROMAGNETISM/redshift.md) — Gravitational redshift z = Delta_Xi
- [energy_em_field.md](05_ELECTROMAGNETISM/energy_em_field.md) — EM energy in segment lattice, u = s^2*u_flat
- [shapiro_delay.md](05_ELECTROMAGNETISM/shapiro_delay.md) — Shapiro delay, PPN factor, Cassini
- [gravitational_lensing.md](05_ELECTROMAGNETISM/gravitational_lensing.md) — Lensing alpha=2r_s/b, Eddington, VLBI

### 06_STRONG_FIELD
- [black_hole_metric.md](06_STRONG_FIELD/black_hole_metric.md) — SSZ Schwarzschild metric
- [singularities.md](06_STRONG_FIELD/singularities.md) — Singularity resolution, D(r_s)=0.555
- [dark_star.md](06_STRONG_FIELD/dark_star.md) — Dark star (no true horizon)
- [cosmic_censorship.md](06_STRONG_FIELD/cosmic_censorship.md) — SSZ version of cosmic censorship
- [infalling_matter.md](06_STRONG_FIELD/infalling_matter.md) — Infalling matter, no freezing
- [superradiance.md](06_STRONG_FIELD/superradiance.md) — Wave amplification in ergosphere
- [rotating_black_holes.md](06_STRONG_FIELD/rotating_black_holes.md) — Kerr-SSZ, ergosphere, frame dragging
- [qnm_spectrum.md](06_STRONG_FIELD/qnm_spectrum.md) — QNM: f_SSZ/f_GR = 1.39, phi-lattice connection
- [isco_comparison.md](06_STRONG_FIELD/isco_comparison.md) — ISCO: SSZ r_ISCO = 2.95 r_s vs GR 3 r_s
- [penrose_process.md](06_STRONG_FIELD/penrose_process.md) — Penrose efficiency: SSZ 21.4% vs GR 20.71%
- [lagrangian_mechanics.md](06_STRONG_FIELD/lagrangian_mechanics.md) — Effective Lagrangian, Euler-Lagrange, orbit equations

### 07_VALIDATION
- [all_tests_2026-05-07.md](07_VALIDATION/all_tests_2026-05-07.md) — Canonical all-tests snapshot: 1296/1296 PASS
- [test_methodology.md](07_VALIDATION/test_methodology.md) — Forward-prediction test framework and method assignment
- [consistency_checks.md](07_VALIDATION/consistency_checks.md) — Formula and cross-repository consistency checks
- [gr_vs_ssz_tables.md](07_VALIDATION/gr_vs_ssz_tables.md) — Side-by-side comparison tables
- [curvature_detection.md](07_VALIDATION/curvature_detection.md) — Frequency curvature observables
- [nebulae_validation.md](07_VALIDATION/nebulae_validation.md) — G79.29+0.46 LBV nebula (Cygnus X-1)
- [gps_validation.md](07_VALIDATION/gps_validation.md) — GPS: +38.45 µs/day confirmed
- [cassini_test.md](07_VALIDATION/cassini_test.md) — Cassini: gamma=1.000021±0.000023
- [mercury_precession.md](07_VALIDATION/mercury_precession.md) — Mercury: 42.98"/century confirmed
- [neutron_star_redshift.md](07_VALIDATION/neutron_star_redshift.md) — NS: z_SSZ=0.173 vs z_GR=0.236
- [power_law_universal.md](07_VALIDATION/power_law_universal.md) — E/E_rest = 1+0.32*(r_s/R)^0.98, R²=0.997
- [ligo_gw240925_v0_pipeline.md](07_VALIDATION/ligo_gw240925_v0_pipeline.md) — GW240925 O4b forward model pipeline (EXPLORATORY, no claim) — data: [Zenodo 18600070](https://zenodo.org/records/18600070)
- [ligo_final_interpretation_lock.md](07_VALIDATION/ligo_final_interpretation_lock.md) — Locked interpretation of LIGO pipeline results
- [ligo_artifact_gate_gw240925.md](07_VALIDATION/ligo_artifact_gate_gw240925.md) — L1 artifact gate: 20-40 Hz excess, kurtosis +44.9
- [ligo_h1l1_mini_pipeline_test_plan.md](07_VALIDATION/ligo_h1l1_mini_pipeline_test_plan.md) — 10-phase hard-gate test plan for H1/L1 artifact exclusion
- [ligo_h1l1_time_delay_replication.md](07_VALIDATION/ligo_h1l1_time_delay_replication.md) — H1/L1 FFT xcorr lag scan ±50ms, COHERENT_WITH_SIGN_FLIP
- [ligo_h1l1_long_baseline_plan.md](07_VALIDATION/ligo_h1l1_mini_pipeline_test_plan.md) — 100 off-source windows, Z-score, subband abs_corr (PENDING run)

### 08_FALSIFICATION
- [falsification_criteria.md](08_FALSIFICATION/falsification_criteria.md) — When SSZ is falsified
- [predictions.md](08_FALSIFICATION/predictions.md) — Quantitative predictions
- [instruments.md](08_FALSIFICATION/instruments.md) — EHT, NICER, ET, LISA, Athena
- [known_limitations.md](08_FALSIFICATION/known_limitations.md) — Known limitations and open questions
- [ligo_open_data_position.md](08_FALSIFICATION/ligo_open_data_position.md) — Strain vs posteriors: model-bound self-confirmation problem
- [ligo_physics_clarification.md](08_FALSIFICATION/ligo_physics_clarification.md) — Chirp mass, posteriors, L1 anomaly, anti-circularity
- [ligo_reproducibility_critique.md](08_FALSIFICATION/ligo_reproducibility_critique.md) — Sourced critique: calibration gap, bilby migration, PB-scale data vs public release ([ssz-ligo-tests/docs](https://github.com/error-wtf/ssz-ligo-tests/blob/main/docs/LIGO_REPRODUCIBILITY_CRITIQUE.md))
- [ligo_open_data_full_report.md](08_FALSIFICATION/ligo_open_data_full_report.md) — **Full Report** (8 parts, 14 sources): calibration chain, PCal/DARM gap, code provenance, template dependence, GW150914 reproduction failure, reproducibility standard ([ssz-ligo-tests/docs](https://github.com/error-wtf/ssz-ligo-tests/blob/main/docs/LIGO_OPEN_DATA_FULL_REPORT.md))

### 09_PAPERS
- [paper_index.md](09_PAPERS/paper_index.md) — All 25 papers with abstracts
- [bibliography.md](09_PAPERS/bibliography.md) — References
- [preprints.md](09_PAPERS/preprints.md) — Preprint status

### 10_REPOSITORIES
- [repo_index.md](10_REPOSITORIES/repo_index.md) — All 37 repositories
- [test_file_index.md](10_REPOSITORIES/test_file_index.md) — All test files
- [reproducibility.md](10_REPOSITORIES/reproducibility.md) — How to reproduce results
- [ligo_tests_findings.md](10_REPOSITORIES/ligo_tests_findings.md) — ssz-ligo-tests: pipeline findings, H1/L1 delay test, open blockers

### 11_GUARDRAILS
- [prime_directive.md](11_GUARDRAILS/prime_directive.md) — Observable → Class → Method → Scope
- [method_assignment.md](11_GUARDRAILS/method_assignment.md) — Which method for which observable
- [confusion_prevention.md](11_GUARDRAILS/confusion_prevention.md) — Common errors and how to avoid them
- [cross_repo_rules.md](11_GUARDRAILS/cross_repo_rules.md) — Cross-repository consistency rules

### 12_GLOSSARY
- [glossary_en.md](12_GLOSSARY/glossary_en.md) — English terminology
- [glossary_de.md](12_GLOSSARY/glossary_de.md) — German terminology

### 13_FREQUENCY_FRAMEWORK
- [holonomy_invariants.md](13_FREQUENCY_FRAMEWORK/holonomy_invariants.md) — I_ABC=1, LISA connection, topological invariance
- [frequency_curvature.md](13_FREQUENCY_FRAMEWORK/frequency_curvature.md) — d²D/dr² = 4× GR, 3-clock measurement
- [future_experimental_prospects.md](13_FREQUENCY_FRAMEWORK/future_experimental_prospects.md) — Timeline 2024–2038: EHT, eXTP, ET, LISA, Athena

---

## Key Numbers

| Metric | Value |
|--------|-------|
| Papers | 25 primary + 7 additional |
| LIGO Tests (ssz-ligo-tests) | v0.5.0 — 330+ tests, GW240925 O4b, long-baseline xcorr, NO CLAIM |
| Repositories | 37 total |
| Tests | 1296/1296 verified in canonical all-tests run |
| Documentation files | 63+ MD files (this repo) |
| Consistency checks | 0 failed in all-tests snapshot |


---

## Quick Start

1. **New to SSZ?** → Start with [01_OVERVIEW/ssz_overview.md](01_OVERVIEW/ssz_overview.md)
2. **Need formulas?** → Go to [03_FORMULAS/formula_compendium.md](03_FORMULAS/formula_compendium.md)
3. **Quick card** → See [03_FORMULAS/quick_reference.md](03_FORMULAS/quick_reference.md)
4. **Method selection** → Read [11_GUARDRAILS/prime_directive.md](11_GUARDRAILS/prime_directive.md)
5. **Validation data** → Check [07_VALIDATION/all_tests_2026-05-07.md](07_VALIDATION/all_tests_2026-05-07.md) and [07_VALIDATION/gr_vs_ssz_tables.md](07_VALIDATION/gr_vs_ssz_tables.md)
6. **Regime vs formula domains?** → Read [02_FOUNDATIONS/regime_and_formula_domain_clarification.md](02_FOUNDATIONS/regime_and_formula_domain_clarification.md)
7. **φ-Lattice** → See [02_FOUNDATIONS/phi_lattice_discretization.md](02_FOUNDATIONS/phi_lattice_discretization.md)
8. **Experimental timeline** → See [13_FREQUENCY_FRAMEWORK/future_experimental_prospects.md](13_FREQUENCY_FRAMEWORK/future_experimental_prospects.md)

---

## The SSZ Mantra

> **Observable → Class → Method → Scope → Then calculate.**

| Observable Type | Method | Formula |
|----------------|--------|---------|
| Timelike (clocks) | Ξ-based | D = 1/(1+Ξ) |
| Null (light) | PPN (1+γ) | α = 2r_s/b |
| Orbit (precession) | PPN (β,γ) | Standard PPN |

---

## License

This project is licensed under the **Anti-Capitalist Software License v1.4**.

See [LICENSE.md](LICENSE.md) for the full license text.

### Citation

```bibtex
@misc{wrede2026sszdocs,
  title={Segmented Spacetime (SSZ) -- Complete Documentation},
  author={Wrede, Carmen N. and Casu, Lino P.},
  year={2026},
  note={Available at https://github.com/error-wtf/ssz-complete-documentation}
}
```

© 2025–2026 Carmen N. Wrede, Lino P. Casu
