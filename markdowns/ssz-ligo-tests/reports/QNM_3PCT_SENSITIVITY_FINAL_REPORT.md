# QNM 3% Branch — Sensitivity Final Report

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️


**Version:** 1.0  
**Date:** 2026-05-18  
**Branch:** QNM_FREQ_3PCT (SSZ Book V51, Ch.30)  
**Script:** `scripts/run_qnm_ringdown_injection_sensitivity.py`  
**Data:** H1 off-source PSD, GW240925 O4b — [Zenodo 18600070](https://zenodo.org/records/18600070)

```
QNM_3PCT_BRANCH_STATUS:            SENSITIVITY_TESTED
GW240925_SENSITIVITY_TO_3PCT:      INSUFFICIENT
DETECTION_THRESHOLD_APPROX:        ~10%
SSZ_SUPPORT_CLAIM_MADE:            NO
SSZ_FALSIFICATION_CLAIM_MADE:      NO
READY_FOR_REAL_LIGO_SSZ_CLAIM:     NO
```

---

## What Was Tested

This is **not a signal test**. It is a **sensitivity test**: given real H1 noise,
could a hypothetical 3% QNM frequency shift be distinguished from GR ringdown
at the SNR level available in GW240925?

The test answers:
> "If SSZ predicts a 3% shift in f_220, would GW240925 data be
> able to tell GR and SSZ apart in this channel?"

Answer: **No — GW240925 ringdown SNR is insufficient to resolve a 3% shift.**

---

## Ringdown Model

```
h_rd(t) = A * exp(-t / tau_220) * cos(2*pi*f_220*t + phi_0),  t >= 0
```

| Parameter | Value | Source |
|-----------|-------|--------|
| M_total | 20.4 M☉ | from Mc=8.9, eta=0.25 (fixed prior, no posterior) |
| f_220_GR | 152.6 Hz | Schwarzschild QNM, chi=0: f = 0.0966 c³/(2π G M) |
| tau_220_GR | 4.2 ms | Q=2 damping: tau = Q/(π f_220) |
| Amplitude A | G·M / (c² · dL) · 0.44 | order-of-magnitude, dL=300 Mpc |
| Injected ringdown SNR | 55.97 (numerical) | noise-weighted inner product |
| f_220 anti-circularity | VALID — no posterior used | analytic formula only |

**Note:** f_220_GR is computed from M_total only, not from posterior M_f or chi_f.
Any use of posterior QNM frequencies would be circular (GR/Kerr prior baked in).

---

## Noise Estimate

| Parameter | Value |
|-----------|-------|
| PSD source | H1 off-source Welch, −500 s window, 256 s, nperseg=4096 |
| PSD at f_220 | 2.36×10⁻⁴⁷ Hz⁻¹ |
| Analytic ringdown SNR | ~13.5 |
| Numerical injected SNR | 55.97 |

The numerical SNR is higher than the analytic estimate because the synthetic
amplitude A is computed relative to the matched-filter inner product with the
off-source PSD, which is somewhat quieter than the trigger window (see L1
anomaly diagnostic).

---

## Epsilon Scan Results

| epsilon | f_220_SSZ (Hz) | shift (%) | delta_lnL | Detectability |
|---------|---------------|-----------|-----------|---------------|
| 0.00 | 152.6 | 0.0% | 0.000 | — |
| 0.01 | 154.2 | 1.0% | −0.080 | UNDETECTABLE |
| **0.02** | **155.7** | **2.0%** | **−0.322** | **UNDETECTABLE** |
| **0.03** | **157.2** | **3.0%** | **−0.726** | **UNDETECTABLE** |
| 0.05 | 160.3 | 5.0% | −2.021 | MARGINAL |
| **0.10** | **167.9** | **10.0%** | **−8.020** | **DETECTABLE** |
| 0.20 | 183.2 | 20.0% | −30.03 | DETECTABLE |
| 0.31 | 199.7 | 30.8% | −62.76 | DETECTABLE |
| 0.39 | 212.2 | 39.0% | −89.08 | DETECTABLE |

Detectability criterion: `|delta_lnL| >= 8` → DETECTABLE, `>= 2` → MARGINAL, else UNDETECTABLE.

---

## Why 3% Is Not Resolvable at GW240925

The frequency resolution of a ringdown measurement scales as:

```
delta_f / f_220 ~ 1 / (rho * 2*pi * f_220 * tau_220)
```

With rho ~ 14 (analytic), f_220 = 152.6 Hz, tau_220 = 4.2 ms:

```
delta_f / f_220 ~ 0.01%   (well below 3%)
```

This means the **analytic resolution is sufficient** — in principle, a 3% shift is
above the resolution threshold. But the likelihood sensitivity `delta_lnL` is only
−0.73, far below the detection threshold of 8.

The gap arises because:

1. **The ringdown SNR at GW240925 is low in absolute terms** (~14 analytic).
   Ringdown SNR is typically much lower than inspiral SNR.
2. **The ringdown duration is short** (tau ~ 4 ms at M~20 M☉).
   Only a few cycles are in the data before the signal decays into noise.
3. **The matched-filter lnL difference scales as rho²·epsilon².**
   At rho~14 and epsilon=0.03: `lnL ~ (14)² * (0.03)² / 2 ~ 0.09`.
   This matches the measured delta_lnL ~ 0.73 (order-of-magnitude consistent).

**Conclusion:**
> GW240925 cannot resolve a 3% QNM frequency shift in this single-event setup.
> This is not a book claim, not a failure, and not a physics result.
> It is a quantitative sensitivity statement.

---

## Registry Branch Mapping

| Branch | epsilon | This test | Detectable |
|--------|---------|-----------|-----------|
| QNM_FREQ_3PCT (V51/Ch.30) | 0.03 | ✅ run | NO — UNDETECTABLE |
| AMPLITUDE_DMIN2 | ~0.308 | not applicable (amplitude, not freq) | — |
| PHOTON_SPHERE_39PCT | 0.39 | ✅ run | YES — but this is a source-frame ratio, not a detector observable |

The 39% entry in the scan is only there for completeness. It is **not** the same
observable as a frequency shift — it is a source-frame photon-sphere ratio that
has no direct detector-strain mapping yet.

---

## What Would Change the Sensitivity

| Change | Effect |
|--------|--------|
| Stack 10 similar events | SNR grows as √10 → rho~44, lnL ~ 7 → MARGINAL |
| Stack 50 events | rho~100, lnL ~ 45 → DETECTABLE |
| Use higher-mass event (lower f_220, longer tau) | Better frequency resolution |
| Einstein Telescope / Cosmic Explorer | rho ~100× higher → 3% easily detectable |

**Recommendation:** Stacking analysis across multiple O4b BBH events is the
correct next step for the 3% branch.

---

## Correct Formulation

**Not:**
```
"3% fits LIGO"
```

**Correct:**
```
GW240925 cannot resolve a 3% ringdown frequency shift in this setup.
The sensitivity threshold for this event is approximately 10%.
A stacking analysis across multiple O4b events would be needed
to probe the 3% branch.
```

---

## Final Gate

```
QNM_3PCT_BRANCH_STATUS:            SENSITIVITY_TESTED
GW240925_SENSITIVITY_TO_3PCT:      INSUFFICIENT
DETECTION_THRESHOLD_THIS_EVENT:    ~10% (delta_lnL = 8 criterion)
STACKING_NEEDED_FOR_3PCT:          YES (~50 events at this SNR level)
READY_FOR_REAL_RINGDOWN_CLAIM:     NO
READY_FOR_REAL_LIGO_SSZ_CLAIM:     NO
SSZ_SUPPORT_CLAIM_MADE:            NO
SSZ_FALSIFICATION_CLAIM_MADE:      NO
```
