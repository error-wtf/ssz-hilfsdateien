# Lorentz Indeterminacy at v=0

**Status:** CANONICAL
**Paper:** 19 — Geometric Resolution of the Lorentz Indeterminacy at v=0

---

## The Problem

In standard Special Relativity, the Lorentz factor at v=0 is trivially:
```
γ_SR(v=0) = 1/√(1-0) = 1
```

This says "nothing happens at zero velocity." But in a gravitational field, a stationary clock still experiences time dilation — the Lorentz factor misses this gravitational encoding.

---

## SSZ Resolution

SSZ introduces a modified Lorentz factor that includes gravitational segmentation:

```
γ_SSZ(v) = exp(Ξ · v²/c²)
```

At v=0:
```
γ_SSZ(v=0) = exp(0) = 1
```

The result is still 1 at v=0, but the **functional form** carries gravitational information through Ξ. This means:
- The v-dependence is Ξ-modulated
- Gravitational effects are encoded in the velocity-dependence curve, not just the v=0 limit
- The expression is regular (no singularity, no indeterminacy)

---

## Why This Matters

The standard Lorentz factor γ = 1/√(1-v²/c²) treats gravity and velocity as separate phenomena. SSZ's formulation unifies them:

| Property | Standard SR | SSZ |
|----------|------------|-----|
| γ(v=0) | 1 (trivial) | 1 (with Ξ encoding) |
| γ(v→c) | ∞ | exp(Ξ) (bounded) |
| Gravity included | No | Yes (through Ξ) |
| Singularity | At v=c | None |

---

## Test

| Test | Repository |
|------|------------|
| test_lorentz_limit.py | segmented-calculation-suite |

---

© 2025–2026 Carmen N. Wrede, Lino P. Casu
