# TWIST_BRANCH Real H1/L1 Exploratory Report

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️


Generated: 2026-05-18 23:05:01  
Event: GW240925 (trigger GPS 1411261107.984)  
Branch: TWIST_BRANCH / SOURCE_PROPAGATION  
Status: EXPLORATORY_DIAGNOSTIC — no claim

**No fitting. No claim. Theta scan is a sensitivity/exploratory diagnostic.**

## Model

```
h_det(f) = F+ h+^SSZ(f) + Fx hx^SSZ(f)

h+^SSZ = S(f) * [cos θ * h+^GR - sin θ * hx^GR]
hx^SSZ = S(f) * [sin θ * h+^GR + cos θ * hx^GR]

S(f): SSZ V0 amplitude+phase (g2_decay branch)
θ:    constant polarisation twist [rad] — sensitivity scan
```

Antenna patterns (approximate, sky-position proxy only, not PE posterior):
- H1: F+ = 0.592, Fx = 0.344
- L1: F+ = 0.437, Fx = 0.683

## H1 Results

GR baseline: SNR = 40.52  
Scale-only:  SNR = 10.43, ΔlnL vs GR = 3.6433e-06  
Robust PSD band_median: 2.8434e-47

| theta [rad] | SNR_twist | lnL_twist | Δ_vs_GR | Δ_vs_scale |
|------------|-----------|-----------|---------|------------|
| 0.000 | 10.43 | -3.2918e+07 | 3.6433e-06 | 0.0000e+00 |
| 0.001 | 10.43 | -3.2918e+07 | 3.6433e-06 | 0.0000e+00 |
| 0.003 | 10.44 | -3.2918e+07 | 3.6433e-06 | 0.0000e+00 |
| 0.010 | 10.45 | -3.2918e+07 | 3.6471e-06 | 3.7253e-09 |
| 0.030 | 10.48 | -3.2918e+07 | 3.6471e-06 | 3.7253e-09 |
| 0.100 | 10.55 | -3.2918e+07 | 3.6508e-06 | 7.4506e-09 |

Exploratory best theta (lnL scan): 0.100 rad — **DIAGNOSTIC ONLY**

## L1 Results

GR baseline: SNR = 277.54  
Scale-only:  SNR = 21.00, ΔlnL vs GR = 2.4796e-05  
Robust PSD band_median: 1.9212e-47

| theta [rad] | SNR_twist | lnL_twist | Δ_vs_GR | Δ_vs_scale |
|------------|-----------|-----------|---------|------------|
| 0.000 | 21.00 | -1.5718e+10 | 2.4796e-05 | 0.0000e+00 |
| 0.001 | 20.77 | -1.5718e+10 | 2.4796e-05 | 0.0000e+00 |
| 0.003 | 20.32 | -1.5718e+10 | 2.4796e-05 | 0.0000e+00 |
| 0.010 | 18.73 | -1.5718e+10 | 2.6703e-05 | 1.9073e-06 |
| 0.030 | 14.20 | -1.5718e+10 | 2.6703e-05 | 1.9073e-06 |
| 0.100 | 1.71 | -1.5718e+10 | 2.6703e-05 | 1.9073e-06 |

Exploratory best theta (lnL scan): 0.010 rad — **DIAGNOSTIC ONLY**

## H1/L1 Coherence

| Quantity | Value |
|---------|-------|
| H1 best theta (exploratory) | 0.100 rad |
| L1 best theta (exploratory) | 0.010 rad |
| H1 SNR GR | 40.52 |
| L1 SNR GR | 277.54 |
| COHERENCE_STATUS | TWIST_PARTIAL_L1_SNR_ANOMALY |

## Physical Interpretation

The twist branch adds an SO(2) rotation of (h+, hx) before projection:

- If θ = 0: reduces to scale-only model
- If θ > 0: h+ leaks into hx and vice versa; different (F+, Fx) at H1 vs L1
  means the two detectors see DIFFERENT amounts of twist
- This is the key observable: scale-only modifies both equally;
  twist produces a differential F+/Fx projection shift

If L1 has SNR anomaly (known from robust PSD recheck), its lnL values
are not reliable. H1 results are the primary diagnostic in that case.

The exploratory best theta is NOT a measurement. It is the theta value
that maximises lnL in the scan. Without proper null-hypothesis testing
and confidence intervals, this cannot be interpreted as a detection.

## Next Required Step

```
1. L1 DQ flag check (is L1 trigger window under known DQ flag?)
2. If L1 is flagged: H1-only analysis becomes primary
3. If L1 is clean: repeat with longer off-source window (1000s+ pre-merger)
4. Only after stable PSD: compare twist vs scale-only residual structure
```

## Gate Status

```
TWIST_REAL_DATA_STATUS:         TWIST_PARTIAL_L1_SNR_ANOMALY
H1_SNR_ANOMALY:                 NO
L1_SNR_ANOMALY:                 YES
ANTENNA_PATTERNS_FROM_POSTERIOR: NO (approximate sky-position proxy)
THETA_FIT_TO_DATA:              NO (scan only)
EXPLORATORY_DIAGNOSTIC_ONLY:    YES
READY_FOR_REAL_LIGO_SSZ_CLAIM:  NO
SSZ_SUPPORT_CLAIM_MADE:         NO
SSZ_FALSIFICATION_CLAIM_MADE:   NO
```
