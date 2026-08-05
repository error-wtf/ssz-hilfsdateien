# Critical Open-Data and Methodology Position

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️


Generated: 2026-05-19  
Repository: error-wtf/ssz-ligo-tests

---

## Summary

This repository is a reproducibility, provenance, and methodology project. It does not make allegations about intent, misconduct, or institutional wrongdoing.

It also does **not** claim that SSZ is confirmed or falsified by the current LIGO release data.

The central conclusion is narrower and more important:

> Public LIGO release products are useful for standard GR/CBC analyses and educational reproduction, but they are not sufficient, by themselves, for a fully independent, anti-circular test of alternative metric theories.

In other words:

- LIGO measures detector strain. The strain is real measurement input.
- But many higher-level products — masses, spins, QNM frequencies, remnant parameters, posterior samples, Bayes factors — are **not raw observables**.
- They are outputs of model-dependent inference pipelines.
- If those outputs are then used as independent proof of the same model assumptions that produced them, a circularity problem arises.

We call this problem: **model-bound self-confirmation**.

The data are not meaningless. But outside the official GR/CBC pipeline, their independent evidential power is much smaller than public communication often suggests.

---

## 1. Strain Is Data; Posterior Products Are Interpretation

LIGO measures calibrated detector strain: `h(t)`. Everything above that level is inferred.

Quantities such as `m1`, `m2`, chirp mass, final spin, QNM frequency, Bayes factors, and posterior samples are **not directly observed in the detector**. They are estimated from strain using waveform models, priors, noise assumptions, calibration, DQ selections, and GR/Kerr/CBC parameter-estimation pipelines.

Therefore such products are **not metric-neutral**.

For alternative metrics, the correct test is not:

```text
Does SSZ match the Kerr-derived posterior?
```

but:

```text
Can an SSZ forward model generate h_SSZ(f) that explains the calibrated strain
at least as well as a GR control, without using GR/Kerr posteriors as truth?
```

---

## 2. The Chirp Mass Is Not a Direct Measurement

The chirp mass is mathematically well-motivated (not arbitrary):

```text
M_chirp = (m1 * m2)^(3/5) / (m1 + m2)^(1/5)
```

It governs the GR inspiral rate: `df/dt ∝ M_chirp^(5/3) * f^(11/3)`.

However, `m1` and `m2` are **not directly measured object properties**. They are model-inferred parameters from Bayesian template matching.

| Layer | What it is | Status |
|-------|-----------|--------|
| `h(t)` — strain | Raw observable | Directly measured |
| `M_chirp`, `m1`, `m2`, `chi` | GR/CBC Bayesian posterior | Model-dependent |
| `f_QNM`, `tau_QNM` | Inferred under Kerr assumption | Model-dependent |

**`m1` and `m2` do not exist as numbers anywhere in the detector.**

Correct statement:
> Under GR/CBC assumptions, the strain is consistent with a source having this inferred chirp mass.

Not valid:
> The detector directly measured this chirp mass as a metric-neutral fact.

---

## 3. The Circularity Problem

```text
1. Assume GR/Kerr/CBC waveform models.
2. Search strain with GR/Kerr/CBC templates.
3. Estimate masses, spins, QNMs via GR/Kerr/CBC parameter estimation.
4. Publish those posterior products.
5. Treat them as independent evidence that GR/Kerr/CBC is correct.
```

This does not mean the experiment is fraudulent. It means the evidential scope must be stated honestly.

The pipeline can show: *"The data are consistent with the GR/CBC model family."*

It cannot, by itself, prove: *"All alternative metric models are excluded."*

For that, alternative models need their own strain-level forward models tested directly against calibrated strain.

---

## 4. Open Data vs. Open Reproducibility

The public GWOSC releases are open in a formal sense (calibrated strain, some metadata, some DQ bits, posterior products, tutorials). But this is not the same as full open reproducibility.

For a fully independent non-GR test, one also needs:

```text
Omicron triggers      iDQ products          offline DQ reports
auxiliary channels    line lists            known instrumental couplings
calibration details   state-vector context  detector-characterization decisions
```

Without these, external groups cannot independently decide whether an anomaly is a signal, a known glitch, an unvetoed transient, a line, a calibration feature, a whitening artifact, or a seismic coupling.

This is why we distinguish **formal open data** from **full open reproducibility**.

---

## 5. Why Public LIGO Products Are Not Enough for SSZ

SSZ is an alternative metric framework. A valid SSZ-LIGO test **cannot** use GR/Kerr posterior parameters as neutral input.

Circular inputs include:

```text
Kerr QNM posteriors           GR remnant mass/spin posteriors
pSEOBNR posterior samples     PE-derived QNM frequencies as ground truth
```

Valid input begins at strain level:

```text
calibrated H1/L1 strain       independent PSD estimation
independent whitening          independent artifact gates
SSZ forward model h_SSZ(f)    direct residual / likelihood comparison
```

This is the **anti-circular principle** of this project.

---

## 6. GW240925 — What the Pipeline Found

The pipeline successfully loaded and processed real LIGO strain. Tests run:
PSD estimation, H1/L1 diagnostics, Gaussianity, line/notch, STFT/Omicron-lite,
phase-randomization, DQ-bit provenance, H1-only exploratory, synthetic SSZ branches,
source-propagation twist, and phase-transport formalism.

Key empirical finding:

```text
Technically reproducible L1 non-Gaussianity concentrated in the 20-40 Hz sub-band.
L1 trigger excess kurtosis:  +44.9  (off-source -500s: +1.1)
Delta = +43.7 -- trigger-specific, not chronic broadband noise.
```

Current classification:

```text
H1:               USABLE_EXPLORATORY
L1:               DIAGNOSTIC_ONLY
H1/L1 coherence:  BLOCKED by L1 DQ
SSZ claim:        NO
SSZ falsification: NO
```

The public release products are insufficient to decide whether the L1 behavior is caused by low-frequency detector noise, seismic coupling, suspension/control system, unvetoed transient, line contamination, or filtering artifacts. Offline Omicron/iDQ/AUX products are needed.

---

## 7. What the L1 Anomaly Does and Does Not Mean

Does **not** mean:

```text
- SSZ is confirmed or falsified
- LIGO data has preprocessing or instrumental issues
```

Does mean:

```text
The released public data are not sufficient for a broadband non-GR H1/L1 coherence test.
```

The strongest fair statement:

> The L1 behavior is technically reproducible but not sufficiently explained by the public release DQ products. Without offline Omicron/iDQ/line/AUX context, L1 cannot be used for a claim-level broadband non-GR coherence test.

---

## 8. Detector Strain Is Not a Telescope Observable

For telescope-based SSZ tests, one may compare redshift, emission lines, lensing. LIGO is different. LIGO measures local interferometer strain: laser phase differences, arm projections, detector response, noise-weighted strain.

A valid SSZ-LIGO model must describe how SSZ affects source-frame emission, propagation, phase transport, polarization/twist, detector projection, and calibrated strain. The relevant target is `h_SSZ(f)`, not a Kerr-derived posterior table.

---

## 9. Phase Transport and Co-Scaling

If the detector, arms, optics, and local rulers co-scale, then a pure local scale factor is not directly observable as an absolute length change. What is observable is the relative phase accumulated by photons along different paths:

```text
DeltaPhi = Phi_x - Phi_y
```

Therefore, SSZ-LIGO must be formulated as a phase-transport / relative-holonomy problem, not as a naive local-arm-length correction. The local detector-arm correction was found to be negligible.

The relevant branch is:

```text
source / strong-field geometry
  -> SSZ scale and twist
  -> propagation
  -> polarization / phase transport
  -> detector projection
  -> strain residual
```

---

## 10. Source-Propagation Twist Branch

The project introduced:

```text
[h_plus_SSZ, h_cross_SSZ]^T  =  S(f) * R(theta) * [h_plus_GR, h_cross_GR]^T
```

where `S(f)` = scale/radial contribution, `R(theta)` = polarization/phase/frame twist.

Status:

```text
SOURCE_PROPAGATION_TWIST: synthetic pass
REAL_TWIST_SIGNAL:        not extractable from current GW240925 run
READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
```

---

## 11. What the Current Data Can Be Used For

**Can be used for:**

```text
pipeline construction           PSD estimation
signal-processing tests         H1/L1 diagnostic checks
Gaussianity tests               line/notch analysis
STFT / Omicron-lite             random-window background estimates
H1-only exploratory tests       synthetic SSZ branch validation
methodological demonstrations
```

**Cannot currently be used for:**

```text
a final SSZ claim                               a final SSZ falsification
a metric-neutral QNM test                       a claim-level H1/L1 non-GR coherence test
a complete artifact exclusion without Omicron/iDQ
```

---

## 12. What We Need from LIGO

For a serious independent non-GR forward-model test:

```text
Omicron triggers for the relevant GPS windows
iDQ information
offline DQ reports
line lists and known instrumental couplings
auxiliary-channel context
calibration uncertainty context
state-vector interpretation
detector-characterization notes
```

Concise question to LIGO:

> We cannot treat current PE/QNM posterior products as metric-neutral for our non-GR forward-model test. H1 is usable for exploratory validation, but L1 shows unresolved low-frequency bandpower / DQ context in the 20-40 Hz band (excess kurtosis +44.9 at trigger, +1.1 off-source). Are offline DQ/iDQ/Omicron/line products available, or should L1 be treated as diagnostic-only for broadband non-GR coherence tests?

---

## 13. Public Petition / Transparency Context

A public petition questioning aspects of the LIGO experiment is not, by itself, scientific proof that LIGO is wrong. However, it is relevant as a transparency signal.

The correct interpretation:

```text
petition = transparency and trust signal
not:
petition = physical disproof of LIGO
```

The petition should be evaluated by asking: which technical questions does it raise? Which are already answered? Which point to real reproducibility gaps? Which require unavailable DQ/Omicron/AUX data?

This project does not use any petition as evidence against LIGO. It uses the existence of public scrutiny as evidence that the reproducibility limits deserve serious attention.

---

## 14. Political / Funding-Relevant Interpretation

For policymakers, the key issue is not an allegation of misconduct. The key issue is whether publicly funded large-scale science should provide enough data and context for independent verification outside the collaboration's preferred model family.

Current situation:

```text
Open data:                       yes, in a limited formal sense
Open reproducibility:            only partially
Open alternative-model testing:  strongly limited
```

This is a legitimate open-science concern. If public money funds the experiment, then public releases should clearly state: what the data can prove, what they cannot prove, which products are model-dependent, and which detector-characterization products are missing.

Without that clarity, public "open data" can create an impression of complete openness while leaving decisive non-standard checks impossible. That is not strong open science.

---

## 15. Final Position

```text
LIGO strain is real measurement input.
LIGO posterior products are model-dependent outputs.
The public releases are useful but incomplete for anti-circular non-GR tests.
GW240925 is useful for pipeline and artifact-gate development.
GW240925 is not sufficient for a final SSZ test.
L1 remains diagnostic-only without offline DQ/Omicron/iDQ clarification.
No SSZ support claim is made.
No SSZ falsification claim is made.
```

The strongest fair criticism:

> The public LIGO releases are formally open, but not fully open in the sense required for independent alternative-metric reproducibility. They allow standard analyses to be reproduced, but they do not always provide enough detector-characterization context for external groups to independently test non-GR forward models at claim level.

This is the central methodological result.

---

*READY_FOR_REAL_LIGO_SSZ_CLAIM: NO*  
*SSZ_SUPPORT_CLAIM_MADE: NO*  
*SSZ_FALSIFICATION_CLAIM_MADE: NO*
