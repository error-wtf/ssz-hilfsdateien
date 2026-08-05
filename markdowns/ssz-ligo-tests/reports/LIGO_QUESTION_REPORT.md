# LIGO Data Quality Question — GW240925 / L1 Excess

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️


**Prepared by:** SSZ-LIGO Test Pipeline  
**Date:** 2026-05-19  
**Event:** GW240925 (GPS 1411261107.984)  
**Pipeline status:** ARTIFACT_GATE_OPEN — awaiting Omicron/iDQ confirmation  
**SSZ claim status:** READY_FOR_REAL_LIGO_SSZ_CLAIM: NO

---

## 1. What We Found

Running a standalone artifact-gating pipeline on the GWOSC O4b open data for
GW240925, we observe a consistent broadband power excess in L1 relative to H1
in the 20–210 Hz band:

| Metric | H1 | L1 | L1/H1 |
|--------|----|----|-------|
| Trigger bandpower (20–210 Hz) | 2.41e-40 strain² | 3.77e-40 strain² | **1.56** |
| Off-source −500s bandpower | 4.25e-40 | 8.42e-40 | — |
| Multi-window stationarity Q (±500s) | 10.3% | **74.5%** | — |
| Trigger z-score vs off-source | −1.10 | +0.32 | — |
| Artifact score (0–24, MEDIUM=5–10) | — | — | **10/24 MEDIUM** |

H1 trigger is **below** its own median (10th percentile). L1 trigger is at the
74th percentile of its own ±500s windows — elevated but not extreme.
The key finding is concentrated in the **20–40 Hz sub-band** (see section 2).

---

## 2. What Our Diagnostics Show

### Line/Notch Test
- L1 contains clear 60/120/180 Hz power-line harmonics (known LIGO instrumental lines)
- These account for ~55% of L1 in-band power
- **After notching 10 strongest peaks: L1/H1 ratio rises to 3.08** (not falls)
- Conclusion: lines are real but do **not** explain the L1/H1 ratio; a diffuse
  broadband floor remains

### STFT Omicron-Lite
- 21.6% of trigger TF tiles are "hot" (>8 dB over off-source baseline)
- Off-source −500s window has 20.8% hot tiles and a larger maximum cluster (18 vs 2)
- No trigger-specific burst structure identified
- Verdict: **INCONCLUSIVE** — L1 excess is spatially diffuse in TF plane

### Multi-Window Stationarity (±1000s, 423 windows)
- L1 trigger at 85th percentile; 15% of random off-source windows are equally high
- No bandpower trend over time (slope ~0, R = −0.04)
- Verdict: **MILD_OUTLIER_80** — elevated but stationary

### Cross-Coherence H1/L1
- Full-band mean magnitude-squared coherence: **0.056** (INCOHERENT)
- Cross-phase mean: **+170°** (near anti-phase), stable across all sub-bands
- Phase resultant length R = 0.91 (stable, not random)
- The ~170° anti-phase is **geometrically consistent** with H1/L1 arm
  orientations for certain sky positions — it is not necessarily anomalous

### Time-Delay Scan ±20 ms
- Cross-correlation is stable at ~−1.0 across all shifts (no preferred delay)
- This is dominated by the broadband anti-phase coherence structure
- No physically preferred time delay identified

### Notch Sweep
- After removing top 10 spectral peaks: L1/H1 **rises** to 3.08
- The L1 excess is genuinely broadband and **cannot be removed by line notching**

### Sub-band Gaussianity (20–210 Hz split into 5 bands)
- 20–40 Hz: L1 excess kurtosis = **+44.9** (strongly non-Gaussian), off-source normal
- 40–80 Hz: L1 and H1 both near-Gaussian at trigger time
- 80–120 Hz: L1 trigger excess kurtosis = +3.3 (mildly elevated)
- 120–160 Hz: L1 trigger excess kurtosis = **+5.7** (elevated vs off-source)
- 160–210 Hz: L1 and H1 both near-Gaussian

Most anomalous sub-band: **20–40 Hz** (L1 trigger ex_k = +44.9, off-source −500s ex_k = +1.1,
Δ = **+43.7 — trigger-specific, not chronic**).

The 20–40 Hz band is maximally sensitive to seismic coupling, suspension modes,
and control-system transients in LIGO. This band was not separately identified
in our initial broadband analysis.

### Phase Randomization Null Test (N=200 surrogates)
- L1 bandpower at 0th percentile vs surrogates (surrogates have more BP variance)
- L1 kurtosis at 92.5th percentile vs surrogates (real signal slightly more kurtotic)
- H1 kurtosis at 96th percentile vs surrogates
- Verdict: both detectors show mild excess kurtosis vs phase-randomized surrogates
  — **not explained by phase structure alone, but also not strongly anomalous**

---

## 3. What We Did NOT Do (Open Blockers)

| Missing diagnostic | Impact |
|-------------------|--------|
| Omicron glitch catalog for L1 at T=1411261107.984 | Cannot confirm absence of glitch |
| iDQ glitch probability score | Cannot quantify glitch contamination |
| L1 auxiliary channel correlation | Cannot identify glitch source |
| Offline DQ flags beyond CBC | May miss narrow-band or transient flags |
| Spectral line database (full LIGO monitoring lines) | Known-line match is partial |

---

## 4. Concrete Questions for LIGO/DQ Team

1. **Is there a known glitch in L1 at GPS 1411261107.984 ± 5s?**  
   (Omicron, iDQ, or detector characterization logs)

2. **Are there active DQ flags at this time beyond CBC_CAT2/3?**  
   (e.g. scattering flags, environmental monitors, injection flags)

3. **Is the 20–40 Hz sub-band in L1 known to be problematic in O4b?**  
   (seismic, suspension modes, low-frequency non-stationarity)

4. **Can the L1/H1 ratio of ~1.85 in 20–210 Hz be explained by antenna
   projection for GW240925 sky localization?**  
   (Expected F+/Fx ratio from posterior sky maps would clarify this)

5. **Is the ~170° H1/L1 cross-phase physically consistent with the event
   sky position?** (Geometrically expected or anomalous for this event?)

---

## 5. What This Report Does NOT Claim

- This report makes **no SSZ (Scale + Spectral Shift) claims**
- No modified gravity posterior fitting has been done
- The L1 excess is **not interpreted as a signal of new physics**
- All findings are **purely artifact-gating diagnostics**
- We do **not** claim LIGO posteriors (ℳ, m₁, m₂, χ) are wrong —
  they are valid within their GR/CBC waveform assumptions

**On LIGO parameter posteriors:**  
Parameters such as chirp mass ℳ = (m₁m₂)^(3/5)/(m₁+m₂)^(1/5) are
well-motivated GR quantities governing the inspiral frequency evolution
(ḟ ∝ ℳ^(5/3) f^(11/3)). They are not arbitrary. However, they are
inferred **inside a GR/CBC waveform model** and are not model-independent
strain measurements. For alternative metric tests, raw strain must be used.

The gate status remains:

```
READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
BLOCKER: L1_DQ_UNRESOLVED — Omicron/iDQ/AUX channels not available
BLOCKER: GW250207_STRAIN_NOT_PUBLIC — GWOSC O4c release pending
```

---

## 6. Path Forward

If LIGO/DQ confirms:
- **No glitch at trigger time**: L1 excess is chronic broadband noise (known
  O4b issue). Pipeline can proceed with H1-only or reweighted analysis.
- **Glitch present**: L1 should be gated out. Repeat analysis H1-only.
- **Antenna projection explains L1/H1 ratio**: L1 excess is not anomalous.
  Reframe as prior-consistent power.

If GW250207 is available and cleaner: run same pipeline there as a comparison
dataset before committing to GW240925 as the SSZ test event.

**Current GW250207 status:** O4c strain not yet public on GWOSC (HTTP 404).
Comparison script is ready (`scripts/run_gw250207_comparison.py`) — will
auto-run once HDF5 files are placed in the data directory.

**Unit normalization status:** 7/7 pipeline normalization checks pass.
Bandpower values and PSD units verified correct to <0.03% error.

---

*All data: GWOSC O4b open release, 18600070.*  
*Pipeline: `error-wtf/ssz-ligo-tests`, branch `main`.*
