# SSZ Quick Reference Card

**Status:** CANONICAL — Laminate and keep handy!

---

## Core Formulas

```
Ξ_weak(r)   = r_s / (2r)                  [outer/g1 branch]
Ξ_decay(r)  = 1 - exp(-φ·r_s/r)            [inner/g2 branch in segcalc]
Ξ_sat(r)    = min(1 - exp(-φ · r_s / r), Ξ_max) [local saturation form]
D(r)        = 1 / (1 + Ξ(r))
s(r)        = 1 + Ξ(r) = 1/D(r)
z(r)        = Ξ(r)
r_s         = 2GM/c²
```

## Key Values

```
Ξ(r_s) = 0.802    D(r_s) = 0.555    z(r_s) = 0.802
r*/r_s = 1.594811 (decay/global) / 1.386562 (saturation/local)
φ = 1.618          φ/2 = 0.809
β = 1              γ = 1
```

## Method Assignment

```
NULL (light)      → PPN (1+γ) = ×2
TIMELIKE (clocks) → Ξ directly
TIMELIKE (orbits) → PPN (β,γ)
```

## Regime Boundaries

```
very_close:    r_s/r < 1.8    → g2 / inner exponential
blended:       1.8 – 2.2      → Hermite C²
photon_sphere: 2.2 – 3.0      → physical regime, g1 branch
strong:        3.0 – 10.0     → physical regime, g1 branch
weak:          > 10.0         → g1 / weak field
```

## PPN Formulas

```
α_lens = (1+γ)r_s/b = 2r_s/b
Δt_Shapiro = (1+γ)(r_s/c)ln(4r₁r₂/d²)
Δω = 6πGM/[a(1-e²)c²]
```

## Kinematic Closure

```
v_esc × v_fall = c²   (always, mass-independent)
v_esc = c·√(r_s/r)    v_fall = c·√(r/r_s)
```

## FORBIDDEN

```
❌ Ξ = (r_s/r)² × exp(-r/r_φ)   — DEPRECATED, NEVER USE
❌ 90/110 as regime boundaries    — Those are probe radii
```

---

© 2025–2026 Carmen N. Wrede, Lino P. Casu
