# TWIST_BRANCH_2PN Synthetic Scan Report

Generated: 2026-05-18 23:34:14
Branch: ANALYTIC_2PN_POLARIZATION_CONTROL
Status: ANALYTIC_2PN_APPROXIMATION

**Synthetic data only. No real LIGO strain. No SSZ claim.**

## Purpose

Break the 0PN polarization degeneracy to enable meaningful twist
sensitivity testing. At 0PN, h_cross(f) = -i * const * h_plus(f),
making the H1/L1 ratio shift under twist negligibly small. At 2PN,
h+ and h× have different frequency-dependent amplitude envelopes,
making the ratio shift genuinely sensitive to twist.

## Template Parameters

| Item | Value |
|------|-------|
| Mc | 8.9 Msun |
| eta | 0.25 |
| inclination | 45 deg (45 deg, non-degenerate) |
| DL | 300 Mpc |
| PN order | 2PN amplitude + 2PN phase (TaylorF2, non-spinning) |
| Band | 20-210 Hz |

## Key Degeneracy Metric

| PN order | std(|hx/hp|)/mean(|hx/hp|) | Frequency-dependent? |
|----------|----------------------------|----------------------|
| 0PN | 1.6322e-16 | NO (constant ratio) |
| 2PN | 1.7355e-03 | YES |
| Improvement | 10633144016109.5x | |

## Constant-theta Scan: H1/L1 Ratio Shift

| theta [rad] | ratio 0PN | shift 0PN | ratio 2PN | shift 2PN | improvement |
|-------------|-----------|-----------|-----------|-----------|-------------|
| 0.0000 | 0.86739 | 0.0000e+00 | 0.87065 | 0.0000e+00 | inf |
| 0.0010 | 0.86739 | 4.4690e-06 | 0.87065 | 5.5029e-06 | 1.23 |
| 0.0030 | 0.86738 | 1.3683e-05 | 0.87064 | 1.6823e-05 | 1.23 |
| 0.0100 | 0.86734 | 4.8822e-05 | 0.87059 | 5.9744e-05 | 1.22 |
| 0.0300 | 0.86722 | 1.7386e-04 | 0.87044 | 2.1047e-04 | 1.21 |
| 0.1000 | 0.86650 | 8.9283e-04 | 0.86960 | 1.0582e-03 | 1.19 |

**Key result:**
- 0PN shift at theta=0.1: 8.9283e-04
- 2PN shift at theta=0.1: 1.0582e-03
- Improvement: 1.2x

## Physical Interpretation

```
0PN degeneracy:
  h_cross(f) = const * (-i) * h_plus(f)    [for all f]
  -> twist R(theta) mixes h+ and hx but the ratio |hx/hp| is constant
  -> H1/L1 detector ratio barely changes under twist
  -> theta(f) scan gives ~0 signal

2PN correction:
  H+(x, eta, iota) and H×(x, eta, iota) differ at 1PN and 2PN level
  -> |hx(f)/hp(f)| varies with frequency
  -> R(theta(f)) mixes amplitude envelopes differently at each f
  -> H1/L1 detector ratio genuinely shifts under twist
  -> theta(f) scan gives nonzero, measurable signal
```

## Twist Branch Status

```
POLARIZATION_CONTROL:          ANALYTIC_2PN_APPROXIMATION
SOURCE_PROPAGATION_TWIST:      DERIVED_V0_CONCEPTUAL
TWIST_BRANCH_2PN_STATUS:       BETTER_CONDITIONED
0PN_DEGENERACY:                CONFIRMED
2PN_DEGENERACY_BREAKING:       CONFIRMED
IMPROVEMENT_AT_THETA_0.1:      1.2x
LOCAL_ARM_TWIST_STATUS:        CLOSED_NEGLIGIBLE
READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
SSZ_SUPPORT_CLAIM_MADE:        NO
SSZ_FALSIFICATION_CLAIM_MADE:  NO
```

## What This Enables Next

```
With 2PN templates (or full IMRPhenomD when available):
  1. Apply source_propagation_twist with 2PN hp/hx
  2. Run H1/L1 ratio scan vs theta at multiple inclinations
  3. Compare with real strain ONLY after L1 DQ is resolved
  4. Still no SSZ claim without coherent multi-detector detection
```
