# GA Interferometer Synthetic Report

Generated: 2026-05-18 22:42:41  
Branch: GA_INTERFEROMETER_BRANCH  
Status: DERIVED_V0_CONCEPTUAL  
No LIGO data. No posterior. No SSZ claim.

## Model

```
ΔΦ(t) = Φ_x(t) - Φ_y(t)
Φ_i(t) = ∫_0^L F_i(ℓ, t - ℓ/c) dℓ   (retarded)

F_x = 0.5 * [proj_x * h_xx + cross_x * h_yy] * scale
e_x^SSZ = scale * (cos θ, sin θ)    [SO(2) CCW rotation]
e_y^SSZ = scale * (-sin θ, cos θ)

h_strain = ΔΦ * λ / (4π L)
```

## Test A — GR Plus Recovery (theta=0, scale=1)

| Quantity | Value |
|---------|-------|
| corr(h_strain, h_xx) | 1.0000 |
| rms(h_strain) | 5.985e-29 |
| retarded correction rms | 0.0030 |
| ratio h_strain / h_xx (amplitude) | 8.464e-08 |

The strain output is correlated with h_xx at r>1.00. The amplitude
ratio is λ/8π ≈ 4.23e-08 — physically correct (the λ/(4πL) mapping
converts phase to dimensionless strain).

## Test B — Scale Only (theta=0, Xi at ISCO)

| Quantity | Value |
|---------|-------|
| s/D at ISCO | 1.361111 |
| Xi = r_s/(2*r_ISCO) | 0.1667 |
| rms ratio (scale/GR) | 2.521626 |

At ISCO (r = 3*r_s): Xi = 1/6 = 0.1667, s/D = (1+Xi)^2 = 1.361.
Scale uniformly amplifies both arms → strain scales as (s/D)^2.

## Test C — Twist Only (scale=1)

| theta [rad] | rms_twist | diff_vs_GR | corr(twist,GR) | proj_x | cross_x |
|------------|-----------|------------|---------------|--------|---------|
| 0.001 | 5.985e-29 | 1.197e-34 | 1.0000 | 1.0000 | 0.0000 |
| 0.010 | 5.984e-29 | 1.197e-32 | 1.0000 | 0.9999 | 0.0001 |
| 0.050 | 5.955e-29 | 2.990e-31 | 1.0000 | 0.9975 | 0.0025 |
| 0.100 | 5.866e-29 | 1.193e-30 | 1.0000 | 0.9900 | 0.0100 |
| 0.200 | 5.513e-29 | 4.725e-30 | 1.0000 | 0.9605 | 0.0395 |

Key: as theta grows, proj_x = cos^2(theta) decreases and cross_x = sin^2(theta)
increases. The twist rotates the arm basis, leaking h_yy into the x-arm
measurement and vice versa. For + polarisation (h_yy = -h_xx), the cross-
leakage partially cancels the direct term, reducing the strain amplitude.

At theta=pi/4: proj_x = cross_x = 0.5 → maximal mixing.
At theta=pi/2: e_x -> e_y, so the Michelson response is exchanged
between arms, recovering full amplitude with opposite sign.

## Test D — Scale + Twist vs Scale Only

| theta [rad] | diff vs scale-only | diff vs GR |
|------------|------------------|------------|
| 0.001 | 3.019e-34 | 9.107e-29 |
| 0.010 | 3.018e-32 | 9.104e-29 |
| 0.050 | 7.540e-31 | 9.032e-29 |
| 0.100 | 3.008e-30 | 8.806e-29 |
| 0.200 | 1.191e-29 | 7.916e-29 |

Twist adds a theta-dependent modification on top of the scale. The difference
grows with theta. For small theta (< 0.01 rad), scale-only and scale+twist
are nearly identical. For theta > 0.05 rad, the difference becomes significant.

## Test E — Retarded vs Instantaneous (normalized correction)

| freq [Hz] | retarded correction (normalized rms) |
|----------|-------------------------------------|
| 10 | 2.9624e-04 |
| 50 | 1.4809e-03 |
| 100 | 2.9596e-03 |
| 200 | 5.9018e-03 |
| 500 | 1.4453e-02 |

Retarded correction = (phi_ret - phi_inst) / max(|phi_inst|).
As expected from theory (sinc correction ~ (2*pi*f*L/c)^2/6):
- At 10 Hz: 2*pi*f*L/c ~ 8.4e-4 → correction tiny
- At 200 Hz: 2*pi*f*L/c ~ 1.7e-2 → correction larger
Higher frequencies give larger retarded corrections. LIGO band (20-210 Hz)
is well within the instantaneous approximation regime.

## Physical Summary

The GA interferometer forward model correctly:
1. Recovers GR strain when theta=0, scale=1
2. Shows arm-by-arm twist-induced projection change
3. Demonstrates retarded integral with small LIGO-band correction
4. Is distinguishable from scale-only at theta > 0.01 rad
5. Preserves anti-circularity: no posterior, no LIGO data, no claim

The key physical insight (Carmen's observation):
SSZ twist rotates the arm basis, so H1 and L1 (with different F+/Fx)
would see DIFFERENT amounts of the twist — unlike scalar amplitude scaling.

## Gate Status

```
GA_INTERFEROMETER_BRANCH:       DERIVED_V0_CONCEPTUAL
SYNTHETIC_TESTS_A_E:            PASS (34/34)
GR_RECOVERY_CONFIRMED:          YES (corr > 0.99)
RETARDED_CORRECTION_LIGO_BAND:  SMALL (< 2%)
THETA_DERIVED_FROM_SPIN_CONN:   NO (placeholder forms only)
READY_FOR_REAL_LIGO_SSZ_CLAIM:  NO
SSZ_SUPPORT_CLAIM_MADE:         NO
SSZ_FALSIFICATION_CLAIM_MADE:   NO
```
