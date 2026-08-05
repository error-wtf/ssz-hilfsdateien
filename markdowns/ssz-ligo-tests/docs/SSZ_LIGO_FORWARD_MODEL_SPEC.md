# SSZ-LIGO Forward Model Specification v0.1

## 1. Purpose

Forward model from SSZ theory to LIGO detector strain h(t).

## 2. Core Equations (LOCKED)

- D_SSZ(r) = 1/(1 + Ξ(r))
- Ξ_weak(r) = r_s/(2r)
- Ξ_strong(r) = min(1 - exp(-φr_s / r), Ξ_max)
- Ξ_max = 1 - exp(-φ) ≈ 0.802
- D_min = 0.555

## 3. Forward Model Chain

SSZ(D,Ξ) → δΨ, δA, δf_220 → h_SSZ(f) → h_I(f) → residual

## 4. Anti-Circularity

FORBIDDEN:
- Posterior f,m,χ as observables
- Kerr as SSZ reference

REQUIRED:
- Model lock before data
- Strain only

## 5. Status

LOCKED: Core equations
MISSING: δΨ, δA, ε_220, η_220
STATUS: PARTIAL - NOT READY
