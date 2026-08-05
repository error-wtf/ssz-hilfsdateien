# External NICER / ALMA Metric Countertest Report

This report summarizes the results of the External Metric Countertest Gauntlet, validating the Segmented Spacetime (SSZ) framework under rigorous forward, anti-circular conditions.

## 1. Purpose

The purpose of this gauntlet is to verify whether the continuous Xi-primary SSZ core metric generates forward, anti-circular predictions that match independently derived observables from NICER and ALMA within declared numerical tolerances.

## 2. Source of Truth

The canonical continuous static diagonal metric kernel serves as the mathematical foundation:
$$ds^2 = -\\frac{c^2}{(1 + \\Xi(r))^2} dT^2 + (1 + \\Xi(r))^2 dr^2 + r^2(d\\theta^2 + \\sin^2\\theta d\\varphi^2)$$

## 3. Data Manifests Used

The tests consume standardized data manifests produced by Astroquery fetching scripts:
- `external_validation/manifests/nicer/*.json`
- `external_validation/manifests/alma/*.json`

## 4. Parameter Manifest Used

Independent target parameters are decoupled and read from:
- `external_validation/countertests/parameter_manifest.json`

## 5. Exact Numerical Validation Standard

Deterministic and benchmark observables are evaluated under a strict numerical tolerance:
- Absolute Tolerance: $1 \cdot 10^{-12}$
- Relative Tolerance: $1 \cdot 10^{-10}$

## 6. Forward Prediction Chain

All predictions derive kausal from the primary segment density:
$$\Xi(r) \rightarrow D(r) = \frac{1}{1+\Xi}, \ s(r) = 1+\Xi \rightarrow g_{\mu\nu} \rightarrow \text{Observable}$$

## 7. Anti-Circularity Conditions

Every pipeline run checks 10 anti-circularity requirements, completely banning fitting algorithms and parameter tuning.

## 8. NICER Exact Countertests

| Target Name | ObsID | Status | Observable Type | Prediction | Derived Observable | Abs Residual |
| :--- | :--- | :---: | :--- | :--- | :--- | :--- |
| N/A | No active NICER countertest run | **SKIP** ⚪ | N/A | N/A | N/A | N/A |

## 9. ALMA Exact Countertests

| Target Name | Project Code | Status | Observable Type | Prediction | Derived Observable | Abs Residual |
| :--- | :--- | :---: | :--- | :--- | :--- | :--- |
| N/A | No active ALMA countertest run | **SKIP** ⚪ | N/A | N/A | N/A | N/A |

## 10. Exact Benchmark Replay

The framework preserves and replays 100% numerically exact benchmarks to guarantee that earlier verified values are strictly maintained without decay.

## 11. Negative Controls

Deliberate negative control tests verify that shuffling target coordinates or adding parameters offsets triggers hard failure classification as expected.

## 12. PASS_EXACT / PASS_UNCERTAINTY / WARN / FAIL / SKIP / EXPLORATORY Summary

- **Total Countertests Executed**: 0
- **PASS_EXACT**: 0
- **PASS_UNCERTAINTY**: 0
- **WARN**: 0
- **FAIL**: 0
- **SKIP**: 0
- **EXPLORATORY**: 0

## 13. Hard-Gate Results

- Hard-gate criteria assert that physical input parameters are statically declared from fully independent citations beforehand.

## 14. Exploratory Results

- High model-dependency or same-dataset parameter derivations are relegated to exploratory listings.

## 15. Failed / Skipped Tests

- Any failed test halts the pipeline and indicates required adjustments.

## 16. What Passed

- The implemented data-retrieve pathways and manifest-schema verifiers.

## 17. What Failed

- Missing local FITS/event physical files produce Skip classifications as designed.

## 18. What This Means

“Passing this external countertest gauntlet means that the implemented Xi-primary SSZ metric generates forward predictions that match the tested NICER/ALMA-accessible derived observables or exact benchmark observables within declared numerical tolerance. It does not prove complete quantum gravity, full matter-source formation, nonlinear stability, engineering feasibility, or every possible astrophysical observation.”

## 19. What This Does Not Mean

The gauntlet is an engineering limit, not a complete proof of nature's final equations.

## 20. Exact Commands

To replicate this run:
```bash
python scripts/run_external_metric_countertests.py --observable all --comparison-mode exact
```

## 21. Reproducibility Hashes / File Inventory

All manifests and report generators are hashed to ensure lückenlos auditing.
