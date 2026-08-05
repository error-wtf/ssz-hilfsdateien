# Method Assignment

**Status:** CANONICAL — ALWAYS FOLLOW

---

## The Assignment Table

| Observable | Type | Method | Formula |
|-----------|------|--------|---------|
| Time dilation | Timelike (clock) | Ξ | D = 1/(1+Ξ) |
| Gravitational redshift | Timelike (clock) | Ξ | z = Ξ(r) |
| Frequency shift | Timelike (clock) | Ξ | ν_obs = ν_emit × D |
| GPS correction | Timelike (clock) | Ξ | ΔD × t |
| Pound-Rebka | Timelike (clock) | Ξ | Δν/ν = ΔΞ |
| **Lensing deflection** | **Null (light)** | **PPN** | **α = (1+γ)r_s/b = 2r_s/b** |
| **Shapiro delay** | **Null (light)** | **PPN** | **Δt = (1+γ)(r_s/c)ln(...)** |
| **VLBI delay** | **Null (light)** | **PPN** | **(1+γ) factor** |
| Perihelion precession | Timelike (orbit) | PPN | Δω = 6πGM/[a(1-e²)c²] |
| Frame dragging | Timelike (orbit) | PPN | Standard Lense-Thirring |
| Geodetic precession | Timelike (orbit) | PPN | Standard PPN |

---

## Why This Matters

Using the wrong method produces the wrong answer:

| Observable | Wrong method (Ξ-only) | Right method | Error |
|-----------|----------------------|-------------|-------|
| Lensing | α = r_s/b | α = 2r_s/b | **50% too low** |
| Shapiro | Δt_Ξ | 2×Δt_Ξ | **50% too low** |
| Time dilation | D_PPN (overcounted) | D_Ξ | Overcounted |

The factor-2 discrepancy is NOT a bug — it's the difference between g_tt-only (Ξ) and g_tt+g_rr (PPN).

---

## PPN Parameters

```
β = 1 (exact in SSZ)
γ = 1 (exact in SSZ)
```

Confirmed: Cassini (2003): γ = 1.000021 ± 0.000023

---

## Decision Flowchart

```
1. Identify the observable
2. Classify: Does it involve LIGHT PATH or CLOCK/ORBIT?
   → Light path (null geodesic) → PPN with (1+γ)
   → Clock comparison (static) → Ξ directly
   → Orbital dynamics → PPN (β,γ) machinery
3. Determine regime (r/r_s)
4. Select correct Ξ formula for that regime
5. Calculate
```

---

© 2025–2026 Carmen N. Wrede, Lino P. Casu
