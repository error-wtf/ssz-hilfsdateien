# Cross-Repository Rules

**Status:** CANONICAL

---

## Core Principle

> **Guardrails = Documentation hardening, NOT error correction.**

The repos are **physically correct and internally consistent.** Guardrails prevent:
1. Cross-repo confusion from comparing different-scope results
2. Silent wrong-method application
3. Future misunderstandings when extending the framework

---

## Repo Scope Index

| Repository | Scope | Ξ Formula | PPN? | Primary Use |
|-----------|-------|-----------|------|------------|
| segmented-calculation-suite | All regimes | Full (weak+strong+blend) | YES | Core engine |
| ssz-qubits | Weak field | r_s/(2r) | NO | GPS, PR, S2 |
| frequency-curvature-validation | Weak field | r_s/(2r) | YES | Shapiro, lensing |
| ssz-lensing | Weak-to-strong | Full | YES | Gravitational lensing |
| ssz-metric-pure | Strong/local metric | local saturation / metric-pure forms | YES | 4D tensors |
| maxwell | Blend | Hermite C² | YES | EM fields |
| Unified-Results | All regimes | Full | YES | 25 test suites |
| g79-cygnus-tests | Specific object | As needed | NO | G79 nebula |
| ssz-schumann | Exploratory | As needed | NO | Schumann resonance |

---

## Rules

### Rule 1: Scope Check Before Comparison
Before comparing Ξ values between repos, check their scope. A weak-field repo (ssz-qubits) and a strong-field repo (ssz-metric-pure) use **different formulas by design.**

### Rule 2: Method Check Before Calculation
Before computing an observable, verify the method assignment:
- Clock/redshift → Ξ
- Light path → PPN (1+γ)
- Orbit → PPN (β,γ)

### Rule 3: Deprecated Formula Ban
The formula `Ξ = (r_s/r)² × exp(-r/r_φ)` is **FORBIDDEN** everywhere. If found in any active code path, it must be replaced.

| Location | Action |
|----------|--------|
| **Active code path** (computation) | REPLACE immediately |
| **Notes/old code only** | Mark as deprecated, don't patch |

### Rule 4: Regime Boundary Consistency
All repos must use the same regime boundaries:
- Blend zone: 1.8 ≤ r/r_s ≤ 2.2
- NOT 90/110 (those are probe radii for testing)

### Rule 5: r*/r_s Values
Two r* values exist — both are correct:
- **r*/r_s = 1.594811:** decay/global comparison, `Xi_A(x)=1-exp(-phi/x)`, `D*=0.610710`
- **r*/r_s = 1.386562:** saturation/local comparison, `Xi_B(x)=1-exp(-phi*x)`, `D*=0.528007`

These are regime-appropriate descriptions, NOT contradictions.

---

## Correct Interpretation

```
"Internally consistent" = Code/Physics OK
"Not compliant"         = Conventions not explicitly documented
```

---

© 2025–2026 Carmen N. Wrede, Lino P. Casu
