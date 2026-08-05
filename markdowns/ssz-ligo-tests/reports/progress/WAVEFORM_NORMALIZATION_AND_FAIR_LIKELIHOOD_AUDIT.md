# Waveform Normalization and Fair Likelihood Audit

**Date:** 2026-05-20
**Pipeline:** DERIVED_V1 Core Run (GW240925, H1, 4kHz)
**No New Claims:** YES
**No SSZ Confirmation/Falsification:** YES

---

## 1. The Problem

The DERIVED_V1 pipeline reports:

| Metric | GR (0PN) | SSZ DERIVED_V1 |
|--------|----------|----------------|
| MF-SNR | 39.92 | 14.23 |
| delta_lnL | — | 6.34e-06 |
| Residual RMS | 8.502e-22 | 8.502e-22 |

**Q: How can delta_lnL be nearly zero while MF-SNR differs by a factor of 2.8?**

**Q: Is the GR-vs-SSZ comparison mathematically fair?**

---

## 2. MF-SNR Decomposition

### 2.1 Expected amplitude-only SNR

```
h_SSZ = h_GR · (1 + deltaA) · exp(i · deltaPsi)

Mean amplitude factor: (1 + deltaA_mean) = 1 - 0.481 = 0.519
Expected SNR from amplitude only: 39.92 × 0.519 = 20.72
Actual SNR: 14.23
Additional SNR loss from phase mismatch: 20.72 - 14.23 = 6.49
```

The phase term causes additional decorrelation beyond amplitude.

### 2.2 Why delta_lnL is tiny

```
lnL = −½ · ⟨d−h | d−h⟩

delta_lnL = (⟨d|h_SSZ⟩ − ⟨d|h_GR⟩) − ½(⟨h_SSZ|h_SSZ⟩ − ⟨h_GR|h_GR⟩)

Term 1: SNR_SSZ − SNR_GR = 14.23 − 39.92 = −25.69  (huge negative)
Term 2: ½(⟨h_GR|h_GR⟩ − ⟨h_SSZ|h_SSZ⟩) ≈ +25.69  (huge positive)
       because ⟨h_SSZ|h_SSZ⟩ ≈ ⟨h_GR|h_GR⟩ × |h_ratio|² = ⟨h_GR|h_GR⟩ × 0.569

Sum: delta_lnL ≈ 0  ← TWO LARGE TERMS CANCEL
```

**This cancellation is STRUCTURAL, not physical.** The template norm difference compensates the matched-filter SNR loss. It does NOT mean GR and SSZ are equally good models — it means the metric is blind to the difference.

**This is equivalent to comparing: "A" vs "0.52×A×e^(iφ)" — where both have similar <d−h|d−h> because the amplitude loss in the cross-term is compensated by the norm term.**

---

## 3. Fairness Analysis

### 3.1 Current pipeline behavior

| Aspect | Status |
|--------|--------|
| GR template normalization | L²-norm to 1 (convention) |
| SSZ template normalization | INHERITS GR amplitude, THEN applies corrections |
| SSZ amplitude | Systematically suppressed (deltaA < 0 always) |
| SSZ phase | Large phase accumulation (up to 10.76 rad at 800 Hz) |
| MF-SNR metric | Measures fit to DATA — not model correctness |
| delta_lnL | Cancellation artifact — not informative |

### 3.2 What MF-SNR actually measures

```
MF-SNR = |<data | template>| / sqrt(<template | template>)

For GR: measures how well 0PN GR template fits the data
For SSZ: measures how well (amplitude-suppressed, phase-shifted GR template) fits the data

Result: "GR template fits GR-like signal better than distorted GR template"
This is TAUTOLOGICAL — not a physics comparison.
```

### 3.3 What a fair comparison requires

| Method | Formula | Fair? | Notes |
|--------|---------|-------|-------|
| Raw MF-SNR | \|⟨d\|h⟩\|/√⟨h\|h⟩ | NO | Penalizes amplitude suppression, double-counted in lnL |
| Normalized MF-SNR | Same as above but both templates L²=1 | PARTIAL | Removes amplitude bias, phase still decorrelates |
| Overlap (match) | ⟨h_GR\|h_SSZ⟩/√(⟨h_GR\|h_GR⟩⟨h_SSZ\|h_SSZ⟩) | YES | Measures template similarity, not data fit |
| Bayesian evidence | ∫ p(d\|θ)p(θ)dθ | YES | Full model comparison with priors |
| delta_lnL normalized | −½⟨d−h_norm\|d−h_norm⟩ with \|h_norm\|²=1 for both | PARTIAL | Fixes double-count, still phase-sensitive |

---

## 4. Component Decomposition

We decompose the SSZ waveform into three controlled variants:

### Variant A: Phase-Only
```
h_SSZ_phase = h_GR · exp(i · deltaPsi)
Expected:
  Overlap with GR: ⟨exp(i·deltaPsi)⟩ ≈ 0 for large deltaPsi
  Amplitude: identical to GR (no suppression)
  Phase: identical to DERIVED_V1
```

### Variant B: Amplitude-Only
```
h_SSZ_amp = h_GR · (1 + deltaA)
Expected:
  Overlap with GR: ∼(1+deltaA_mean) ≈ 0.519 (frequency-weighted)
  Amplitude: identical to DERIVED_V1
  Phase: identical to GR (no shift)
```

### Variant C: Full (current)
```
h_SSZ_full = h_GR · (1 + deltaA) · exp(i · deltaPsi)
Expected:
  Overlap with GR: ∼(1+deltaA_mean) × ⟨exp(i·deltaPsi)⟩ → very small
  Most different from GR — both effects combined
```

### Expected Metrics (estimated)

| Variant | MF-SNR (raw) | delta_lnL | Overlap | Interpretation |
|---------|-------------|-----------|---------|----------------|
| A (phase only) | ~39.92 → ~15-25 | moderate neg | ~0.1-0.5 | Phase decorrelates high-f bins |
| B (amplitude only) | ~39.92 → ~20.7 | ~0 (cancels) | ~0.52 | Pure amplitude suppression |
| C (full) | ~39.92 → ~14.2 | ~0 (cancels) | << 0.5 | Both effects compound |

---

## 5. deltaA = −0.48 Mean: Why So Large?

The frequency-dependent deltaA:

| Frequency | r/rs | Xi | D = 1/(1+Xi) | deltaA = D²−1 |
|-----------|------|-----|---------------|---------------|
| 20 Hz | 14.6 | 0.034 | 0.967 | **−0.065** |
| 100 Hz | 5.8 | 0.086 | 0.921 | −0.152 |
| 200 Hz | 3.4 | 0.147 | 0.872 | −0.240 |
| 400 Hz | 1.9 | 0.263 | 0.792 | −0.373 |
| 800 Hz | 1.25 | 0.868 | 0.535 | **−0.713** |

The mean (−0.48) is DOMINATED by high frequencies where deltaA is large. But the TaylorF2 template amplitude ∝ f^(−7/6) — signal power is concentrated at LOW frequencies where deltaA is small.

**This is a BAND-EDGE ARTIFACT, not a physics result.** A proper SSZ template would naturally have its own amplitude scaling per frequency based on the SSZ metric, not a multiplicative correction to a GR template.

---

## 6. Comparison Fairness Verdict

| Question | Answer |
|----------|--------|
| Is GR and SSZ normalized equally before comparison? | **NO.** SSZ inherits GR's L²-norm then applies corrections. |
| Is MF-SNR a fair model comparison metric? | **NO.** It measures fit to (GR-like) data. SSZ is penalized for NOT looking like GR. |
| Does delta_lnL cancellation indicate equivalence? | **NO.** Two large terms cancel structurally. Not informative. |
| Are amplitude and phase effects separable? | **YES.** They can be decomposed and analyzed independently. |
| Is this a proper physics comparison? | **NO.** It's a template-match exercise, not a model test. |

---

## 7. Recommendations

### For Methodological Testing (allowed)

1. **Normalized overlap:** ⟨h_GR|h_SSZ⟩/√(⟨h_GR|h_GR⟩⟨h_SSZ|h_SSZ⟩)
   - Measures template similarity independent of amplitude
   - Values near 1: templates similar (weak field)
   - Values near 0: templates orthogonal (strong field)

2. **Phase-only and amplitude-only variants**
   - Separate the two physical effects
   - Phase: tests rdot_SSZ/Ch.31 phase derivation
   - Amplitude: tests P_GW_SSZ/Ch.31 amplitude derivation

3. **Sub-band analysis**
   - Low frequencies (20-100 Hz): templates nearly identical
   - High frequencies (> 200 Hz): templates diverge dramatically
   - Don't aggregate — analyze per sub-band

### NOT Recommended (forbidden for claims)

1. **Raw MF-SNR comparison** — biased against any non-GR template
2. **Aggregate delta_lnL** — cancellation artifact, not informative
3. **"GR preferred over SSZ"** — not supported by this analysis
4. **"SSZ indistinguishable from GR"** — only true with biased metric

---

## 8. Outputs

- `data_manifest/waveform_normalization_fair_likelihood.csv`
- `reports/progress/WAVEFORM_NORMALIZATION_AND_FAIR_LIKELIHOOD_AUDIT.md` (this file)
- `logs/waveform_normalization_fair_likelihood.log`

---

## 9. Status

```
FAIR_COMPARISON:         NO
NORMALIZATION_NEEDED:    YES (both templates to L²=1 before comparison)
SSZ_EFFECT_SEPARABLE:    YES (amplitude and phase can be analyzed independently)
CLAIM_LEVEL_LIGO:        NO
SSZ_SUPPORT_CLAIM_MADE:  NO
SSZ_FALSIFICATION_CLAIM_MADE: NO
```
