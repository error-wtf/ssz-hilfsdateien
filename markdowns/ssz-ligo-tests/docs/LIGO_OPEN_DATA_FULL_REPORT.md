# LIGO Open Data — Full Report: Reproducibility, Calibration, and Auditability

**Authors:** Lino Casu, Carmen Wrede (SSZ Research Project)  
**Date:** 2026-05-19  
**Status:** Public methodology document — source-backed reproducibility and provenance evaluation  
**Repository:** [ssz-ligo-tests](https://github.com/error-wtf/ssz-ligo-tests)

---

## Legal Preamble

This is a reproducibility, provenance, and methodology project. It evaluates the limits of public GWOSC products for claim-level alternative-metric forward testing. It is limited to data-scope, provenance, and methodology.

This report documents, on the basis of publicly verifiable primary sources:

1. A structural reproducibility gap between what LIGO/GWOSC releases and what would
   be required for a fully independent external audit of the complete measurement chain
2. A calibration transparency deficit documented since 2016 and confirmed in 2025
3. Code provenance issues arising from software migration practices
4. The methodological consequences for non-GR forward-model tests

All claims are sourced. All quotes are verbatim from the cited documents.

---

## Executive Summary

```text
WHAT LIGO/GWOSC RELEASES:
  - Calibrated strain h(t)           — analysis-ready, pre-processed
  - Data quality segments             — CAT1/CAT2/CAT3 flags
  - GR/CBC posteriors                 — model-conditioned inference outputs
  - Subset of auxiliary channels      — selected runs, NDS2/OSDF required
  - Tutorials and software tools      — for standard GR/CBC analyses

WHAT IS NOT RELEASED:
  - PCal (Photon Calibrator) raw channels
  - DARM error and control signals
  - Time-dependent FIR/IIR filter coefficient archives
  - CalibEnv calibration model files (epoch-by-epoch)
  - Full auxiliary channel set via public API
  - Original merge requests from LIGO GitLab (pre-migration)
  - PB-scale raw diagnostic data (10^5+ channels per instrument)

CONSEQUENCE:
  Standard GR/CBC analyses:         GWOSC products are sufficient
  Non-GR forward-model tests:       Missing context is a material limitation
  Full independent calibration audit: Structurally impossible with public data
```

**The single sharpest fair sentence:**

> Ten years after GW150914, a fully independent external reconstruction of the
> calibration chain that produced the published h(t) remains practically impossible
> using only publicly available data. This is a reproducibility and provenance limitation.

---

## Part I: What GWOSC Provides and What It Does Not

### 1.1 The LIGO Data Management Plan

The LIGO Data Management Plan ([LIGO-M1000066-v31](https://dcc.ligo.org/public/0009/M1000066/031/Data_Management_Plan-v31.pdf))
explicitly defines calibrated strain as the primary public data product.

This was confirmed in a direct public exchange on Mastodon (3 December 2025):

> "Our full data management policy, as agreed with funding councils, is LIGO-M1000066.
> This covers calibrated data, not auxiliary channels. Hence, while we try our best to
> provide the community with what they request, we do not have resources to support
> everything."
> — LIGO @scicomm.xyz [[source]](https://chaos.social/deck/@LIGO@scicomm.xyz/116569194588841654)

### 1.2 What h(t) Actually Is

Strain h(t) is not a raw observable. It is a reconstructed signal:

> "The gravitational-wave strain [...] is computed by combining the DARM error signal
> with a model of the frequency-dependent response of the interferometer."
> — arXiv:1710.09973

External reproduction of h(t) from scratch requires:
- The DARM error and control signals at the time of the event
- The exact calibration model (frequency-dependent response function)
- Time-dependent FIR/IIR filter coefficients and their switch-over epochs
- Photon Calibrator channel data and injected waveforms

None of these are part of the standard GWOSC release.

### 1.3 Scale: What Is Recorded vs. What Is Released

The O4a open data documentation (arXiv:2508.18079) makes clear that:

- Calibrated strain: approximately **4 TB/year per instrument**
- Total detector data with all diagnostic channels: **several PB/year**
- Number of diagnostic channels: **hundreds of thousands per instrument**

What GWOSC releases is a small, processed fraction. The published channels include:

| Channel suffix | Meaning |
|----------------|---------|
| `CLEAN` | Noise subtraction applied |
| `NOLINES` | Spectral line removal applied |
| `SUB60HZ` | Sub-60 Hz noise subtracted |
| `AR` | Analysis Ready — full preprocessing applied |

These are **not raw measurements**. They are pre-processed analysis products.

```text
GWOSC releases:      ~4 TB/yr/instrument  — pre-processed, analysis-ready
Total recorded:      PB-scale             — 10^5+ channels, not public
```

### 1.4 Auxiliary Channels: Partial Release Only

The IGWN O3 auxiliary channel release explicitly describes the published set as a
**subset** of available sensor channels:

> IGWN forum: "New data release: O3 auxiliary channels"
> https://ask.igwn.org/t/new-data-release-o3-auxiliary-channels/470

Auxiliary channel data for O4 requires NDS2/OSDF access — not available through the
standard GWOSC web API. This creates a practical barrier to independent analysis.

---

## Part II: The Calibration Question — Since 2016

### 2.1 The Discovery Paper Reference

The GW150914 discovery paper (PRL 116, 061102, 2016) describes calibration as follows:

> "The detector output is calibrated in strain by measuring its response to test mass
> motion induced by photon pressure from a modulated calibration laser beam [63]."

Reference [63] at time of publication was an **unpublished e-print containing no data**.

### 2.2 The 2016 Petition (3,028 Verified Signatures)

A public petition addressed to Prof. Karsten Danzmann (Albert Einstein Institute)
raised three specific technical questions:

**Question 1:** Where are the actual calibration data — strain as a function of laser
power — published? The reference in the discovery paper leads to an unpublished document.

**Question 2:** The photon calibrator method was last applied in 2003 (LIGO-T030266-00-D,
Bruursema), achieving mirror excursions of ~10^-15 m. GW150914 required ~10^-18 m.
Was this method repeated since 2003 with documented improvement?

**Question 3:** If not, is there a plan to do so retroactively?

Source: https://www.change.org/p/prof-karsten-danzmann-beantworten-sie-bitte-3-fragen-%C3%BCber-das-ligo-experiment?signed=true

These are precise calibration traceability questions. They are not equivalent to
claiming the detection cannot be reconstructed. Their lack of complete public answers over the
following decade is a legitimate open-science concern.

### 2.3 The 2025 IGWN Forum Request

On 2 December 2025, an independent researcher submitted a formal reproducibility
request to the IGWN community forum:

> "Are there plans to release, as open data:
> - the relevant PCal channels,
> - the DARM error / control signals, and
> - the exact time-dependent filter definitions (FIR/IIR coefficients and switch-over epochs)
> so that public h(t) can be reproduced from scratch?"

Source: https://ask.igwn.org/t/request-for-fully-reproducible-calibration-chain-for-gwosc-strain-data/1397/2

The LIGO response confirmed the policy: calibrated data, not auxiliary channels.

Conclusion stated by the requester:

> "I understand now that, by policy, only calibrated strain is part of the public data
> products and that the full calibration chain and aux channels are not.
> For a project largely funded by public money I had hoped for a bit more
> reproducibility and openness — but I appreciate the honest answer."

---

## Part III: Code Provenance and Migration

### 3.1 The bilby Migration

The `bilby` Bayesian inference library is a core LVK analysis tool used for parameter
estimation of gravitational wave signals. Its changelog documents:

> "Migration from LIGO GitLab to GitHub. Old merge requests are only visible on the
> LIGO GitLab."
> — [bilby CHANGELOG.md](https://github.com/bilby-dev/bilby/blob/main/CHANGELOG.md)

### 3.2 Why This Matters

Published papers cite specific code versions. Scientific reproducibility requires:

```text
Code version cited in paper
  → source code publicly accessible
  → development history (merge requests, issues, reviews) publicly accessible
  → parameter choices traceable to documented decisions
  → no broken links in the scientific record
```

When migration moves merge requests to an internal-only system, the development history
becomes opaque. External reviewers cannot trace why specific algorithmic choices were made.

This creates **link rot in the scientific record** — a material reproducibility and provenance limitation and structural auditability gap.

### 3.3 The Broader Pattern

```text
Paper cites:   Code version X / Repository Y / Merge Request Z
Actual state:  Repository migrated, MRs internal-only, old links broken
Result:        External full-chain reproduction becomes practically impossible
```

---

## Part IV: Template Model Dependence and Circularity Risk

### 4.1 GR-Based Templates

When GR-based template banks are used for matched filtering, detections are sensitive
to the assumed model. This can create methodological circularity:

> "Mis-Modelling in Gravitational Wave Astronomy: The Trouble With Templates"
> — arXiv:1311.4898

> "The Issues of Mismodelling Gravitational-Wave Data for Parameter Estimation"
> — arXiv:2101.07743

### 4.2 Non-Gaussian Noise

Real LIGO data are non-stationary and non-Gaussian. Instrumental glitches require
auxiliary channel context (Omicron, iDQ) for reliable classification:

> "Performance of iDQ ahead of LIGO, Virgo, and KAGRA's fourth observing run"
> — arXiv:2412.04638

Without access to Omicron triggers, iDQ scores, and offline DQ context, external groups
cannot independently verify signal/glitch separation at claim level.

### 4.3 The GW150914 Reproduction Study

An independent 2020 study explicitly states:

> "While the main finding [...] could be reproduced, an exact replication of the original
> LIGO analysis was not possible because the original dataset was not publicly available."
> — arXiv:2010.07244

### 4.4 Danish Group Criticism (2017)

The German Wikipedia article on LIGO notes:

> "Eine dänische Gruppe von Wissenschaftlern kritisiert insbesondere eine unzureichend
> dokumentierte und potenziell fehleranfällige Trennung von tatsächlichem Signal und
> zufälligen Störungen. Weitere Analysen widersprechen jedoch dieser Kritik."
>
> [A Danish group of scientists criticizes an insufficiently documented and potentially
> error-prone separation of actual signal from random disturbances. Further analyses,
> however, contradict this criticism.]
> — https://de.wikipedia.org/wiki/LIGO

Wikipedia also notes that figures in the first detection publication were adjusted
"by eye" for pedagogical purposes without disclosure — a separate communication
transparency concern.

---

## Part V: Consequences for This Project

### 5.1 What This Project Uses

This project (SSZ-LIGO Forward Model Test Suite) uses:

- GWOSC public strain h(t) — via Zenodo DOI:10.5281/zenodo.18600070
- No model-conditioned posteriors as metric-neutral input
- Forward-model approach: predict SSZ observables, compare to measured strain
- Anti-circularity protocol: no use of GR/CBC/Kerr parameters as input

### 5.2 What the Reproducibility Gap Means for This Project

| Need | Available | Consequence |
|------|-----------|-------------|
| Calibrated strain | YES (GWOSC) | H1 usable for exploratory tests |
| DQ segments | YES (GWOSC) | Partial context only |
| Omicron/iDQ | NO | L1 20-100 Hz persistent background noise unresolved |
| PCal/DARM channels | NO | Cannot verify calibration chain |
| Aux channels (full) | NO | Cannot fully characterize glitches |
| Offline DQ | NO | Cannot gate L1 at claim level |

**Current project status:**

```text
H1:   PASS_EXPLORATORY — usable for forward-model validation
L1:   DIAGNOSTIC_ONLY — L1 20–100 Hz persistent background noise: trigger SNR ≈ off-source mean; unresolved without offline DQ context

PIPELINE_STATUS: PASS_EXPLORATORY
READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
```

### 5.3 The Epistemic Position

```text
What we must not claim:
- SSZ is confirmed by LIGO.
- SSZ is falsified by LIGO.
- L1 shows SSZ.
- The 39% branch is refuted.
- The current public release is sufficient for a claim-level non-Kerr forward test.

What we may say:
- The public GWOSC strain products are useful for standard workflows and diagnostics.
- For this alternative-metric forward-test use case, they are insufficient by themselves at claim level because full calibration, DQ, auxiliary, Omicron/iDQ, line and preprocessing context is missing.
- The L1 20–100 Hz SSZ-SNR metric is not trigger-specific and is DQ-blocked for physical interpretation.
```

---

## Part VI: The Reproducibility Standard

Ten years after GW150914, a complete reproducibility package for a publicly funded,
Nobel Prize-winning experiment would include:

1. **PCal data**: strain as a function of injected laser power, for each observing run,
   in a machine-readable, versioned format
2. **Filter archives**: version-controlled FIR/IIR coefficient archives per epoch, per
   instrument, covering all public event data
3. **DARM channels**: error and control signals for time windows containing published events
4. **Pipeline provenance**: fully public development history of all analysis code, including
   merge requests, parameter choices, and version tags — not just current code
5. **Executable chain**: a documented, executable pipeline that takes publicly available
   inputs and reproduces the published strain product, end-to-end

None of these currently exist in the GWOSC public release.

---

## Part VII: Strongest Formulations (Sourced, Legally Safe)

**On calibration:**
> Public GWOSC releases provide calibrated strain, but not the complete, externally
> reproducible calibration and auxiliary channel chain with which independent parties
> could reconstruct h(t) fully from raw/control signals to the final data product.

**On scale:**
> GWOSC releases approximately 4 TB/year/instrument of pre-processed strain.
> The total detector data with all diagnostic channels is several PB/year.
> For a fundamentally independent audit of the full measurement chain, the
> public release is structurally insufficient.

**On code provenance:**
> Open Data without stable, versioned, publicly accessible provenance is not a complete
> reproducibility guarantee. When analysis code, repositories, merge requests, or
> calibration artefacts are migrated, removed, or kept internally, the external
> auditability of published strain products is structurally weakened.

**On the ten-year gap:**
> Ten years after GW150914 it is scientifically difficult to justify that a fully
> independent reconstruction of the calibration chain remains practically impossible
> from publicly available data.

**This is a reproducibility, provenance, and methodology project. It evaluates the limits of public GWOSC products for claim-level alternative-metric forward testing. It is limited to data-scope, provenance, and methodology.**

---

## Part VIII: Primary Sources

| # | Document | URL |
|---|----------|-----|
| 1 | IGWN forum: reproducibility request (Dec 2025) | https://ask.igwn.org/t/request-for-fully-reproducible-calibration-chain-for-gwosc-strain-data/1397/2 |
| 2 | LIGO Mastodon response (Dec 2025) | https://chaos.social/deck/@LIGO@scicomm.xyz/116569194588841654 |
| 3 | Petition: 3,028 verified signatures (2016) | https://www.change.org/p/prof-karsten-danzmann-beantworten-sie-bitte-3-fragen-%C3%BCber-das-ligo-experiment?signed=true |
| 4 | LIGO Data Management Plan v31 | https://dcc.ligo.org/public/0009/M1000066/031/Data_Management_Plan-v31.pdf |
| 5 | bilby CHANGELOG — GitLab migration | https://github.com/bilby-dev/bilby/blob/main/CHANGELOG.md |
| 6 | LIGO Wikipedia (DE) — Danish group + figure adjustment | https://de.wikipedia.org/wiki/LIGO |
| 7 | IGWN O3 aux channels release | https://ask.igwn.org/t/new-data-release-o3-auxiliary-channels/470 |
| 8 | arXiv:1710.09973 — calibrated strain reconstruction | https://arxiv.org/abs/1710.09973 |
| 9 | arXiv:2412.04638 — iDQ performance O4 | https://arxiv.org/abs/2412.04638 |
| 10 | arXiv:1311.4898 — template mismodelling | https://arxiv.org/abs/1311.4898 |
| 11 | arXiv:2101.07743 — mismodelling / parameter estimation | https://arxiv.org/abs/2101.07743 |
| 12 | arXiv:2302.03676 — O3 open data paper | https://arxiv.org/abs/2302.03676 |
| 13 | arXiv:2010.07244 — GW150914 reproduction study | https://arxiv.org/abs/2010.07244 |
| 14 | arXiv:2508.18079 — O4a open data paper | https://arxiv.org/abs/2508.18079 |

---

*Part of the SSZ (Segmented Spacetime) research project.*  
*See also: [docs/LIGO_REPRODUCIBILITY_CRITIQUE.md](LIGO_REPRODUCIBILITY_CRITIQUE.md)*
