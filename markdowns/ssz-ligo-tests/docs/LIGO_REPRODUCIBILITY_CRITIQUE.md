# LIGO Open Data: Reproducibility Gap — A Methodological Critique

**Date:** 2026-05-19 | **Authors:** Lino Casu, Carmen Wrede (SSZ Research Project)
**Legal note:** This is a reproducibility, provenance, and methodology project. It evaluates the limits of public GWOSC products for claim-level alternative-metric forward testing. It is limited to data-scope, provenance, and methodology.

---

## 1. Position Statement

This is a reproducibility, provenance, and methodology project. It evaluates the limits of public GWOSC products for claim-level alternative-metric forward testing. It is limited to data-scope, provenance, and methodology.

This document DOES claim, based on primary sources:
- Public GWOSC releases are pre-calibrated analysis products, not raw measurement data
- The full calibration chain (PCal channels, DARM signals, filter definitions) is not
  publicly available in a form that allows independent external reconstruction of h(t)
- This is a material reproducibility limitation for non-standard and non-GR analyses
- The distinction between "open data product" and "fully reproducible measurement chain"
  has not been clearly communicated in public discourse around LIGO

---

## 2. What GWOSC Releases — And What It Does Not

### Released by GWOSC
- Calibrated strain h(t) — the main scientific data product
- Data quality segments — veto flags, CAT1/CAT2/CAT3 classifications
- Event posteriors — mass, spin, distance estimates under GR/CBC models
- Tutorials, documentation, GWpy workflows
- A subset of auxiliary channels (selected runs only; not via standard web API)

### NOT released as standard public product
- Raw DARM error and control loop signals
- Photon Calibrator (PCal) raw channels and injected waveforms
- Time-dependent FIR/IIR filter coefficient archives used to produce h(t)
- Full CalibEnv calibration model files, epoch-by-epoch
- Auxiliary channels via GWOSC web API (NDS2/OSDF required, partial access only)

This is confirmed by LIGO's own data management policy:

> "This covers calibrated data, not auxiliary channels."
> — LIGO @scicomm.xyz, Mastodon, 3 December 2025

Source: https://chaos.social/deck/@LIGO@scicomm.xyz/116569194588841654

The LIGO Data Management Plan (LIGO-M1000066-v31) confirms calibrated strain as the
scope of the agreed public release:
https://dcc.ligo.org/public/0009/M1000066/031/Data_Management_Plan-v31.pdf

---

## 3. The Reproducibility Request (December 2025)

On 2 December 2025, a technical request was submitted to the IGWN community forum asking:

> "Are there plans to release, as open data:
> - the relevant PCal channels,
> - the DARM error / control signals, and
> - the exact time-dependent filter definitions (FIR/IIR coefficients and switch-over epochs)
> so that public h(t) can be reproduced from scratch?"

Source: https://ask.igwn.org/t/request-for-fully-reproducible-calibration-chain-for-gwosc-strain-data/1397/2

The GWOSC/LIGO response:

> "Our full data management policy, as agreed with funding councils, is LIGO-M1000066.
> This covers calibrated data, not auxiliary channels. Hence, while we try our best to
> provide the community with what they request, we do not have resources to support
> everything."

Conclusion drawn after this exchange:

> "I understand now that, by policy, only calibrated strain is part of the public data
> products and that the full calibration chain and aux channels are not.
> For a project largely funded by public money I had hoped for a bit more
> reproducibility and openness — but I appreciate the honest answer."

This is a factual observation confirmed by LIGO's own response.

---

## 4. Historical Context: The Calibration Question Since 2016

The calibration transparency question is not new. In 2016, a public petition addressed to
Prof. Karsten Danzmann (Albert Einstein Institute, LIGO co-investigator) raised three
specific questions about calibration of the GW150914 measurement (3,028 verified signatures):

Source: https://www.change.org/p/prof-karsten-danzmann-beantworten-sie-bitte-3-fragen-%C3%BCber-das-ligo-experiment?signed=true

The petition asked:

1. The GW150914 discovery paper (PRL 116, 061102, 2016) cites Reference [63] —
   an unpublished e-print — for the photon-pressure calibration method.
   **Where are the actual data (strain as function of laser power) published?**

2. In 2003, the photon calibrator method achieved mirror excursions of ~10^-15 m
   (LIGO-T030266-00-D, Bruursema). GW150914 implied ~10^-18 m.
   **Was the calibration repeated since 2003, and is the improvement documented?**

3. **If not, is there a plan to perform this retroactively?**

These are precise, technical questions about calibration traceability. They are not
equivalent to claiming the detection cannot be reconstructed. Their lack of complete, prominent
public answers over the following decade substantiates the reproducibility and provenance limitation.

---

## 5. What the Literature Confirms

### 5.1 h(t) is a reconstructed product, not a raw observable

> "The gravitational-wave strain [...] is computed by combining the DARM error signal
> with a model of the frequency-dependent response of the interferometer."
> — arXiv:1710.09973 [1]

External reproduction requires the calibration model — parameters, filter definitions,
and epoch-dependent versions. These are not part of the standard GWOSC release.

Reference [1]: https://arxiv.org/abs/1710.09973
"Reconstructing the calibrated strain signal in the Advanced LIGO detectors"

### 5.2 Non-Gaussian noise requires auxiliary context to interpret

Real LIGO data are non-stationary and non-Gaussian. Classification of instrumental glitches
requires Omicron triggers, iDQ scores, and aux-channel context:

> arXiv:2412.04638 — "Performance of iDQ ahead of LIGO, Virgo, and KAGRA's fourth
> observing run" [2]
> https://arxiv.org/abs/2412.04638

Without this context, external groups cannot independently distinguish instrumental
artifacts from signal candidates at claim level.

### 5.3 Template model dependence creates evidential circularity risk

When GR-based template banks are used for detection and parameter estimation, and the
results are then cited as evidence for GR, a methodological circularity arises:

> arXiv:1311.4898 — "Mis-Modelling in Gravitational Wave Astronomy: The Trouble With
> Templates" [3]
> https://arxiv.org/abs/1311.4898

> arXiv:2101.07743 — "The Issues of Mismodelling Gravitational-Wave Data for Parameter
> Estimation" [4]
> https://arxiv.org/abs/2101.07743

The pipeline shows: data are consistent with GR/CBC. It cannot, by itself, prove that
all alternative metric models are excluded.

### 5.4 Open data scope is explicitly limited

> arXiv:2302.03676 — "Open data from the third observing run of LIGO, Virgo, KAGRA
> and GEO" [5]
> https://arxiv.org/abs/2302.03676

The O3 open data paper describes the release scope. Auxiliary channel data are
explicitly characterized as a "subset" — not a complete sensor/channel archive.

IGWN O3 auxiliary release announcement:
https://ask.igwn.org/t/new-data-release-o3-auxiliary-channels/470

### 5.5 GW150914 reproducibility: "not exactly reproducible"

An independent reproduction study explicitly states:

> "While the main finding [...] could be reproduced, an exact replication of the original
> LIGO analysis was not possible because the original dataset was not publicly available."
> — arXiv:2010.07244 [6]
> https://arxiv.org/abs/2010.07244

### 5.6 Signal/noise separation criticism (Danish group, 2017)

The German Wikipedia article on LIGO notes:

> "Eine dänische Gruppe von Wissenschaftlern kritisiert insbesondere eine unzureichend
> dokumentierte und potenziell fehleranfällige Trennung von tatsächlichem Signal und
> zufälligen Störungen. Weitere Analysen widersprechen jedoch dieser Kritik."
> [A Danish group of scientists criticizes in particular an insufficiently documented
> and potentially error-prone separation of actual signal from random disturbances.
> Further analyses, however, contradict this criticism.]
> — https://de.wikipedia.org/wiki/LIGO

Wikipedia also notes that members of the LIGO consortium acknowledged that figures in the
first detection publication were adjusted "by eye" for pedagogical purposes without
disclosure at the time — a separate communication transparency concern.

---

## 6. Summary: Open Data Product vs. Reproducible Measurement Chain

```text
Layer                          | Publicly available | Sufficient for non-GR test
-------------------------------|--------------------|--------------------------
Calibrated strain h(t)         | YES (GWOSC)        | Partially
DQ segments (CAT1-3)           | YES (GWOSC)        | Partially
GR/CBC posteriors              | YES (GWOSC)        | NOT metric-neutral
Omicron / iDQ glitch products  | NO (internal)      | YES — critical
Auxiliary channels             | Subset only        | Often required
PCal / DARM raw channels       | NO                 | Required for full audit
Filter coefficient archives    | NO                 | Required for full audit
Calibration model (CalibEnv)   | NO                 | Required for full audit
```

The key distinction:

```text
Open Data Product              != Fully reproducible measurement chain
```

---

## 7. Code Provenance, Migration, and Link Rot

Reproducibility requires not just that data exist today, but that:

```text
The code, parameters, merge requests, pipeline versions, and data products
that produced a specific published result are permanently, citably, and
publicly accessible in the exact version that was used.
```

There is documented evidence of structural provenance gaps in LIGO/LVK software:

**`bilby` code migration (LIGO GitLab → GitHub):**  
The `bilby` Bayesian inference library changelog explicitly notes that after migration
from the internal LIGO GitLab to GitHub, links were retroactively updated. The original
merge requests remain only in the LIGO GitLab and are not publicly accessible:

> "Migration from LIGO GitLab to GitHub. Old merge requests are only visible on the
> LIGO GitLab."
> — bilby CHANGELOG.md [[source]](https://github.com/bilby-dev/bilby/blob/main/CHANGELOG.md)

This is scientifically relevant because:
- Published papers cite code and pipeline versions
- If the original merge requests, issues, and review history are not public,
  external reviewers cannot fully trace the reasoning behind algorithmic decisions
- Migration without archived public access creates **link rot in the scientific record**

The broader pattern:

```text
Paper cites:   Code version X / Repo Y / Merge Request Z
Actual state:  Repo migrated, MRs internal-only, old links broken
Result:        External full-chain reproduction becomes practically impossible
```

**Scale of the data problem:**  
The O4a open data documentation notes that calibrated strain represents approximately
**4 TB/year per instrument**. The total detector data with all diagnostic channels is
**several PB/year** with hundreds of thousands of channels. Only a small, processed
subset reaches GWOSC. The channels published include explicitly pre-processed variants:
`CLEAN` (noise-subtracted), `NOLINES` (spectral lines removed), `AR` (Analysis Ready).

This means:

```text
What GWOSC releases = analysis-ready, pre-processed strain products
What was actually recorded = PB-scale raw data with 10^5+ diagnostic channels
```

For an independent audit, one needs to trace from raw to processed — and that path
is not publicly available.

**Strongest fair formulation:**

> Open Data without stable, versioned, publicly accessible provenance is not
> a complete reproducibility guarantee. When analysis code, repos, merge requests,
> or calibration artefacts are migrated, removed, or kept internally, the external
> auditability of published strain products is structurally weakened.
> This represents a material reproducibility and provenance limitation. It is a material auditability limitation.

---

## 8. The Reproducibility Standard

Ten years after GW150914, a reasonable reproducibility standard for a publicly funded,
Nobel Prize-winning experiment would include:

1. Published photon calibrator data: strain as a function of injected laser power,
   for each observing run
2. Version-controlled filter coefficient archives used to produce each public h(t) release
3. DARM error/control channels for periods containing published events
4. A documented, executable pipeline that takes publicly available inputs and reproduces
   the published strain product

None of these currently exist in the GWOSC public release.

The strongest fair formulation:

> **Ten years after GW150914, a fully independent external reconstruction of the
> calibration chain that produced the published h(t) remains practically impossible
> using publicly available data. For standard GR/CBC analyses, the released products
> are adequate. For a fundamentally independent audit of the full measurement chain,
> they are structurally insufficient.**

---

## 8. What This Project Does and Does Not Conclude

This is a reproducibility, provenance, and methodology project. It evaluates the limits of public GWOSC products for claim-level alternative-metric forward testing. It is limited to data-scope, provenance, and methodology.

### DOES conclude
- Public GWOSC data are analysis products, not raw observables
- For standard GR/CBC analyses: GWOSC products are adequate
- For anti-circular non-GR forward-model tests: missing calibration chain, aux channels,
  Omicron/iDQ, and offline DQ context are material limitations
- The public communication of LIGO data as "fully open" does not accurately reflect the
  reproducibility gap for non-standard analyses
- The calibration transparency question, raised publicly since 2016, remains unanswered
  in the form required for independent fundamental audit
- Code migration (LIGO GitLab → GitHub) left original merge requests non-public,
  creating provenance gaps in the scientific record
- GWOSC strain is ~4 TB/year per instrument; total detector data is PB-scale;
  only a small processed subset is publicly released

### Central methodological conclusion
```text
Open Data != Full Open Reproducibility

For non-GR forward-model tests: the decisive missing components are
calibration chain provenance, aux channels, Omicron/iDQ,
time-dependent filter definitions, and code/pipeline provenance.

Open Data without stable, versioned, publicly accessible provenance
is not a complete reproducibility guarantee.

This is a reproducibility, provenance, and methodology project. It evaluates the limits of public GWOSC products for claim-level alternative-metric forward testing. It is limited to data-scope, provenance, and methodology.
```

---

## 9. Primary Sources

| Source | URL |
|--------|-----|
| IGWN forum: reproducibility request | https://ask.igwn.org/t/request-for-fully-reproducible-calibration-chain-for-gwosc-strain-data/1397/2 |
| LIGO Mastodon response | https://chaos.social/deck/@LIGO@scicomm.xyz/116569194588841654 |
| Petition (3028 signatures) | https://www.change.org/p/prof-karsten-danzmann-beantworten-sie-bitte-3-fragen-%C3%BCber-das-ligo-experiment?signed=true |
| LIGO Data Management Plan | https://dcc.ligo.org/public/0009/M1000066/031/Data_Management_Plan-v31.pdf |
| LIGO Wikipedia (DE) | https://de.wikipedia.org/wiki/LIGO |
| IGWN O3 aux channels release | https://ask.igwn.org/t/new-data-release-o3-auxiliary-channels/470 |
| arXiv:1710.09973 — calibrated strain reconstruction | https://arxiv.org/abs/1710.09973 |
| arXiv:2412.04638 — iDQ performance O4 | https://arxiv.org/abs/2412.04638 |
| arXiv:1311.4898 — template mismodelling | https://arxiv.org/abs/1311.4898 |
| arXiv:2101.07743 — mismodelling parameter estimation | https://arxiv.org/abs/2101.07743 |
| arXiv:2302.03676 — O3 open data paper | https://arxiv.org/abs/2302.03676 |
| arXiv:2010.07244 — GW150914 reproduction study | https://arxiv.org/abs/2010.07244 |
| arXiv:2508.18079 — O4a open data paper | https://arxiv.org/abs/2508.18079 |
| bilby CHANGELOG — LIGO GitLab migration | https://github.com/bilby-dev/bilby/blob/main/CHANGELOG.md |
