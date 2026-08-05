# Prime Directive

**Status:** ALWAYS FOLLOW — VERBINDLICH

---

## Interpretation Safety Notes

> **(1)** "Null" refers to the **geodesic type** (ds²=0), not "no effect."
> **(2)** Statements like "Ξ → 1" are **asymptotic** — Ξ saturates near 1 in the transition zone (blend), although strong-field is formally used for r_s/r < 1.8.
> **(3)** Energy rules concern **observed transformation factors** (multiplicative), not statements about global GR energy conservation.

---

## 0) THE PRIME DIRECTIVE

> **Never use a single method for all observables.**

Always classify the observable first (null vs timelike vs orbit) and select the correct method (PPN vs Ξ) accordingly.

---

## 1) Observable Classification → Method

### A) NULL / Light-Path Observables
**Examples:** Lensing, Shapiro delay, VLBI/group delay, lens time-delays

**Method:** PPN completion — multiply Ξ-only result by (1+γ)
```
result = Ξ_only × (1 + γ)
```
- For GR-equivalent: γ = 1.0 → factor 2
- Ξ-only = g_tt contribution only (half of full GR for these observables)

### B) TIMELIKE STATIC / Clock Observables
**Examples:** Time dilation, gravitational redshift, GPS, Pound-Rebka

**Method:** Ξ-based formulation directly
```
D(r) = 1/(1 + Ξ(r))
```
- Keep local c invariant by construction
- Differences are comparative (between clocks/frames)

### C) TIMELIKE ORBIT Observables
**Examples:** Perihelion advance, precession, frame dragging

**Method:** PPN orbit machinery (β, γ, ...)
- NOT Ξ-only shortcuts

---

## Quick Reference Table

```
Observable Type     → Method
─────────────────────────────────
NULL (light)        → PPN (1+γ)
TIMELIKE (clocks)   → Ξ-proxy
TIMELIKE (orbits)   → PPN (γ,β)
```

---

## 2) Factor-2 Rule (CRITICAL)

If a null-observable comes out at **50% of GR**:
- **This is NOT a bug by default**
- It indicates "Ξ-only = g_tt piece"
- Full GR requires PPN: (1+γ), γ=1

### Why the Factor 2?
```
Ξ-integration captures only g_tt (temporal)
PPN captures g_tt + g_rr (temporal + spatial)

α_total = α_tt + α_rr = r_s/b + r_s/b = 2r_s/b ✅
```

---

## 3) Regime Check (MANDATORY)

Before using any Ξ formula, determine regime via r/r_s:

| Regime | r/r_s | Operative Xi branch |
|--------|-------|---------------------|
| **very_close** | < 1.8 | g2 / inner exponential |
| **blended** | 1.8–2.2 | C² Hermite blend |
| **photon_sphere** | 2.2–3.0 | physical photon-sphere regime; g1 branch in current calculators |
| **strong** | 3.0–10.0 | physical strong-field regime; g1 branch in current calculators |
| **weak** | > 10.0 | g1 / weak field |

**Never mix multiple "strong-field Ξ" formulas without an explicit blend rule.**

```
Formula domain      → Formula
─────────────────────────────────
r/r_s > 2.2         → Ξ = r_s/(2r)
r_s/r < 1.8         → inner exponential / g2
1.8 ≤ r/r_s ≤ 2.2   → Hermite blend
```

Above `r/r_s=2.2`, "g1 branch" does not mean "physically weak everywhere": photon-sphere and compact-object strong-field contexts still extend up to `r/r_s=10`.

---

## 4) Wave-Equation Transform (No Numerical Traps)

For oscillatory fields (large k·ρ):
- **DO NOT** validate using finite-difference second derivatives
- **USE** analytic chain rule

When transforming dρ = s(r)·dr, ensure the second-derivative operator includes the extra term:
- In 1D: d²/dr² introduces an s·s' term
- In 3D: include the correct divergence/geometry term

**Missing this term is a technical error, not physics.**

---

## 5) Shapiro: One-Way vs Round-Trip

Always distinguish:
- **One-way signal delay** vs **Round-trip radar echo** (extra factor 2)

This is **separate from PPN (1+γ)**. Never conflate them.

---

## 6) Energy Accounting (Critical for QM Link)

**NEVER** add SR + GR + "extra" energies linearly (avoid triple counting).

**USE** multiplicative factor bookkeeping:
```
E_obs = E_rest × (transform factors)
```

Phase/Action links are handled via path/geometry, not "changing local laws."

---

## 7) Deprecated Ξ Formula BAN

Any deprecated/old Ξ(r) expression is **FORBIDDEN** in new derivations.

**Deprecated:**
```
❌ Ξ = (r_s/r)² × exp(-r/r_φ)  ← VERBOTEN
```

Treat as **hard fail** in any computation.

---

## 8) Paper Writing Guardrails

1. Add "Method selection & scope" text:
   - Ξ-only for timelike observables
   - PPN completion for null observables
2. Add explicit factor-2 remark for lensing/Shapiro:
   - Ξ-only = half
   - Full GR recovered with (1+γ), γ=1
3. Keep "local c invariant" explicit
4. Emphasize: effects arise from geometry/path + clock mapping, not local speed changes

---

## The Mantra

> **Observable → Class → Method → Scope → Then calculate.**

---

*This document contains the binding rules for SSZ calculations.*
*On violation: check and correct result.*

© 2025–2026 Carmen N. Wrede, Lino P. Casu
