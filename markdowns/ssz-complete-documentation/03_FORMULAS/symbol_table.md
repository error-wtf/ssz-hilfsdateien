# Complete Symbol Table & Notation Key

---

## Greek Symbols

| Symbol | LaTeX | Name | Definition | Unit | Paper |
|--------|-------|------|------------|------|-------|
| Ξ | `\Xi` | Segment density | g1: r_s/(2r); decay form: 1-exp(-φr_s/r); local saturation form: min(1-exp(-φr_s / r), Ξ_max) | dimensionless | 01, 03 |
| φ | `\varphi` | Golden ratio | (1+√5)/2 = 1.618... | dimensionless | All |
| α | `\alpha` | Fine-structure const. | e²/(4πε₀ℏc) = 1/137.036 | dimensionless | 15 |
| α_lens | `\alpha_{\text{lens}}` | Lensing deflection | (1+γ)r_s/b | rad | 01 |
| β | `\beta` | PPN parameter | β = 1 (exact in SSZ) | dimensionless | 01 |
| γ | `\gamma` | PPN parameter | γ = 1 (exact in SSZ) | dimensionless | 01 |
| γ_seg | `\gamma_{\text{seg}}` | Segment Lorentz factor | exp(Ξv²/c²) | dimensionless | 19 |
| Δω | `\Delta\omega` | Perihelion precession | 6πGM/[a(1-e²)c²] | rad/orbit | PPN |
| Δ(M) | `\Delta(M)` | Mass-dependent correction | From φ-geometry | dimensionless | 18 |
| π | `\pi` | Pi | 3.141592653589793 | dimensionless | 13 |

---

## Latin Symbols

| Symbol | Name | Definition | Unit | Paper |
|--------|------|------------|------|-------|
| c | Speed of light | 299,792,458 | m/s | Const. |
| D | Time dilation factor | 1/(1+Ξ) | dimensionless | 03 |
| D* | D at intersection | D_SSZ(r*) = D_GR(r*), value depends on Xi form | dimensionless | 04 |
| G | Gravitational constant | 6.67430e-11 | m³/(kg·s²) | Const. |
| ℏ | Reduced Planck constant | 1.054571817e-34 | J·s | Const. |
| M | Central mass | variable | kg | — |
| M☉ | Solar mass | 1.98892e30 | kg | Const. |
| r | Radial coordinate | Distance from center | m | — |
| r_s | Schwarzschild radius | 2GM/c² | m | GR |
| r* | D-intersection comparison radius | r*/r_s = 1.594811 (decay/global) or 1.386562 (saturation/local) | m | 04 |
| r_φ | Coupling radius | (φ/2)r_s[1+βΔ(M)] | m | 17 |
| s | Scaling factor | 1 + Ξ(r) = 1/D(r) | dimensionless | 01 |
| z | Redshift | 1/D - 1 = Ξ(r) | dimensionless | 21 |
| b | Impact parameter | Closest approach | m | PPN |

---

## Velocities

| Symbol | Name | Definition | Paper |
|--------|------|------------|-------|
| v_esc | Escape velocity | c√(r_s/r) | 02 |
| v_fall | Fall velocity | c√(r/r_s) = c²/v_esc | 02 |
| v_group | Group velocity | L_seg·f/N | 08 |

**Invariant:** v_esc × v_fall = c² (Paper 07)

---

## Canonical Key Values

| Constant | Value | Description |
|----------|-------|-------------|
| Ξ(r_s) | 0.80171 | Ξ at Schwarzschild radius |
| D(r_s) | 0.55503 | D at r_s (FINITE!) |
| r*/r_s | 1.594811 / 1.386562 | `D_SSZ=D_GR` comparison radius; specify Xi form |
| D* | 0.610710 / 0.528007 | D at intersection for decay / saturation form |
| φ/2 | 0.80902 | Coupling factor |
| γ_PPN | 1.0000 | PPN gamma (exact) |
| β_PPN | 1.0000 | PPN beta (exact) |

---

## Method Assignment

| Observable | Method | Formula | Why |
|-----------|--------|---------|-----|
| Time dilation | Ξ-proxy | D = 1/(1+Ξ) | Only g_tt |
| Frequency shift | Ξ-proxy | ν_obs = ν_emit × D | Same as dilation |
| Light deflection | PPN (1+γ) | α = 2r_s/b | Needs g_tt + g_rr |
| Shapiro delay | PPN (1+γ) | Δt = 2(r_s/c)ln(...) | Needs g_tt + g_rr |
| Perihelion | PPN | Standard formula | Standard PPN |

---

## Forbidden Symbols & Formulas

| Formula | Status | Replacement |
|---------|--------|-------------|
| Ξ = (r_s/r)² exp(-r/r_φ) | **DEPRECATED** | Use the documented g1/g2/blend branch for the regime |
| r/r_s = 90 or 110 as boundary | **WRONG** | 1.8 and 2.2 |
| r_s = GM/c² | **WRONG** | r_s = 2GM/c² |
| D = 1/(1+2Ξ) | **WRONG** | D = 1/(1+Ξ) |
