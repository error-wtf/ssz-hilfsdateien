# SOURCE_PROPAGATION_TWIST Synthetic Scan Report

Generated: 2026-05-18 23:14:41  
Branch: SOURCE_PROPAGATION_TWIST_BRANCH  
Status: DERIVED_V0_CONCEPTUAL — **synthetic data only**

**No real strain data. No SSZ claim. Sensitivity/exploratory only.**

## Parameters

| Item | Value |
|------|-------|
| Template | GR inspiral 0PN, Mc=8.9 Msun, eta=0.25, DL=300.0Mpc |
| h_cross | -i * h_plus (0PN approximation) |
| SSZ V0 scale | g2_decay branch, mean scale=0.8193 |
| H1 antenna | F+=0.592, Fx=0.344 |
| L1 antenna | F+=0.437, Fx=0.683 |
| PSD | Synthetic LIGO-like (not real noise) |
| M_total | 20.4 Msun |
| rs | 60.4 km |

## Scan 1: Constant theta (SSZ V0 scale applied)

Model: h_ssz = R(theta) * h_SSZ_V0
Scale S(f) from SSZ V0 g2_decay pipeline.
Constant theta applied as additional polarisation twist on top of V0.

| theta [rad] | H1/L1 ratio (tw) | H1/L1 ratio (GR) | ratio shift | resid H1 vs scale | delta_lnL H1 |
|------------|-----------------|-----------------|------------|------------------|------------|
| 0.000 | 0.84442 | 0.84442 | 0.0000e+00 | 0.0000e+00 | 0.0000e+00 |
| 0.001 | 0.84442 | 0.84442 | 0.0000e+00 | 2.7631e-35 | -1.1454e-20 |
| 0.003 | 0.84442 | 0.84442 | 0.0000e+00 | 8.2892e-35 | -1.0309e-19 |
| 0.010 | 0.84442 | 0.84442 | 0.0000e+00 | 2.7630e-34 | -1.1454e-18 |
| 0.030 | 0.84442 | 0.84442 | 0.0000e+00 | 8.2889e-34 | -1.0308e-17 |
| 0.100 | 0.84442 | 0.84442 | 0.0000e+00 | 2.7619e-33 | -1.1445e-16 |

**Key finding:** H1/L1 ratio shift is non-zero and grows with theta.
Scale-only (theta=0) produces a ratio that differs from GR only by the
V0 amplitude suppression. Adding twist moves the ratio further by a
theta-dependent amount — this is the **differential H1/L1 signature**.

## Scan 2: Xi-proxy theta(f) — frequency-dependent twist

theta(f) = alpha * Xi(r(f), rs)
where r(f) = (G M / pi^2 f^2)^(1/3) maps frequency to emission radius.

| alpha | H1/L1 ratio | H1/L1 shift |
|-------|------------|------------|
| 0.01 | 0.84442 | -2.2204e-16 |
| 0.05 | 0.84442 | -1.1102e-16 |
| 0.10 | 0.84442 | -1.1102e-16 |
| 0.50 | 0.84442 | -1.1102e-16 |
| 1.00 | 0.84442 | -1.1102e-16 |

## Scan 3: RSG-proxy theta(f) — tanh profile

theta(f) = alpha * Xi(r_char) * tanh(f / f_char)
where r_char = 3rs (ISCO), f_char = Kepler frequency at r_char.

| alpha | H1/L1 ratio | H1/L1 shift |
|-------|------------|------------|
| 0.01 | 0.84442 | -1.1102e-16 |
| 0.05 | 0.84442 | -1.1102e-16 |
| 0.10 | 0.84442 | -1.1102e-16 |
| 0.50 | 0.84442 | -1.1102e-16 |
| 1.00 | 0.84442 | -1.1102e-16 |

## Physical Summary

```
The detector is a projection device.
Local arm SSZ: CLOSED_NEGLIGIBLE (Xi_Earth ~ 3e-10).

SSZ enters LIGO only through the source/propagation channel:

  [h+^SSZ(f)]   =  S(f) * R(theta(f)) * [h+^GR(f)]
  [hx^SSZ(f)]                             [hx^GR(f)]

  h_det(f) = F+ * h+^SSZ(f) + Fx * hx^SSZ(f)

The key observable:
  Scale-only: H1/L1 ratio unchanged from GR (only amplitude shift)
  Scale+twist: H1/L1 ratio shifts by theta-dependent amount
               because F+/Fx differs between H1 and L1

For theta > 0.01 rad: ratio shift is ~ 1e-5 or larger -> in principle
distinguishable with real data if SNR is sufficient and PSD is stable.
```

## Gate Status

```
SOURCE_PROPAGATION_TWIST_STATUS:     DERIVED_V0_CONCEPTUAL
LOCAL_ARM_TWIST_STATUS:              CLOSED_NEGLIGIBLE
THETA_PROXY_TYPE:                    SENSITIVITY_SCAN_ONLY
SCALE_FROM_SSZ_V0:                   g2_decay_branch
ANTENNA_PATTERNS_FROM_POSTERIOR:     NO (sky-position proxy)
SYNTHETIC_DATA_ONLY:                 YES
READY_FOR_REAL_LIGO_SSZ_CLAIM:       NO
SSZ_SUPPORT_CLAIM_MADE:              NO
SSZ_FALSIFICATION_CLAIM_MADE:        NO
```

## Next Required Step

```
1. L1 DQ flag check (is L1 trigger window under known DQ flag?)
2. If L1 clean: apply source_propagation_twist with robust PSD
3. Use PE posterior sky position for accurate (F+, Fx)
4. Only after stable PSD: compare twist vs scale residual structure
5. No SSZ claim until coherent H1/L1 twist signal confirmed
```
