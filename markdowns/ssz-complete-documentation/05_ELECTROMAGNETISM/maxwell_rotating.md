# Maxwell Waves as Rotating Space

**Status:** CANONICAL
**Paper:** 22 — Maxwell Waves as Rotating Space

---

## Core Concept

Paper 22 reinterprets electromagnetic wave propagation in segmented spacetime as a manifestation of "rotating space" — the wave equation in the scaled coordinates dρ = s(r)·dr has the form of propagation through a medium with a position-dependent refractive index.

---

## The Wave Equation

In segmented spacetime, the Maxwell wave equation becomes:
```
(1/s) ∂/∂r [(1/s) ∂E/∂r] - (1/c²) ∂²E/∂t² = 0
```

with s(r) = 1 + Ξ(r).

This is NOT the standard wave equation in curved spacetime. The key difference is the explicit s(r) dependence, which introduces:
- Modified dispersion
- Position-dependent phase velocity
- Additional coupling between field components

---

## Technical Warning

For oscillatory fields (large k·ρ):
- **DO NOT** validate using finite-difference second derivatives
- **USE** analytic chain rule

The second-derivative operator in transformed coordinates:
```
d²/dρ² = (1/s²) d²/dr² - (s'/s³) d/dr
```

Missing the s'/s³ term is a **technical error**, not physics.

---

## Connection to Radial Scaling

The "rotating space" picture is equivalent to the radial scaling gauge (Paper 01):
- s(r) = effective refractive index
- E' = s·E, B' = s·B
- ∇·(s²E) = 0

The rotation metaphor captures how the scaled coordinates introduce a spiral-like structure in the field propagation.

---

© 2025–2026 Carmen N. Wrede, Lino P. Casu
