# Critical Methodology and Open-Reproducibility Position

**Date:** 2026-05-19 | **Cross-ref:** `ssz-ligo-tests/reports/OPEN_DATA_METHODOLOGY_POSITION.md`

## Summary

This repository does **not** claim that LIGO data are fake, manipulated, or useless.
It does **not** claim that SSZ is confirmed or falsified by the current public LIGO release.

The central conclusion is methodological:

> Public LIGO/GWOSC release products are valuable for standard GR/CBC analyses. However,
> by themselves they are not sufficient for a fully independent, anti-circular test of
> alternative metric theories.

| Level | Meaning | Status for SSZ/non-GR testing |
|-------|---------|-------------------------------|
| Calibrated strain `h(t)` | Detector measurement input | Usable, with DQ caution |
| DQ / Omicron / iDQ / AUX context | Detector-characterization context | Often essential, not fully public |
| PE / QNM / posterior products | Model-conditioned inference output | Not metric-neutral |

---

## 1. Strain vs. Posterior Products

LIGO measures calibrated detector strain `h(t)`. It does not directly measure `m1`, `m2`,
chirp mass, final spin, QNM frequency, or Bayes factors. Those are inferred from strain
under GR/CBC waveform assumptions — meaningful for standard analyses, but not metric-neutral.

The anti-circular test question is:

> Can an SSZ forward model generate `h_SSZ(f)` that explains calibrated strain without
> using GR/Kerr posterior products as ground truth?

---

## 2. Chirp Mass: Meaningful, Not Directly Measured

```text
M_chirp = (m1*m2)^(3/5) / (m1 + m2)^(1/5)
```

The detector does not directly output `M_chirp`. It is inferred under GR/CBC assumptions.
For alternative-metric tests, chirp mass posteriors are not used as primary observables.

---

## 3. Open Data vs. Open Reproducibility

We do not claim LIGO hides or manipulates data. We state that the public GWOSC release
provides calibrated strain and selected DQ information, but not the full
detector-characterization context needed to independently resolve the L1 low-frequency
anomaly for our non-GR forward-model test.

Context that would be needed: Omicron triggers, iDQ products, offline DQ reports,
auxiliary-channel context, line lists, calibration uncertainty context.

This is a reproducibility concern, not an accusation of fraud.

---

## 4. GW240925 Current Status

```text
H1:              usable for exploratory single-detector validation
L1:              diagnostic-only until further DQ clarification
H1/L1 coherence: not claim-level for this event
SSZ support claim:       NO
SSZ falsification claim: NO
READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
```
