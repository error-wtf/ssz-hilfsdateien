# Kinematic Closure

**Status:** CANONICAL
**Paper:** 07 — Kinematische Schließung: Escape vs. Fall

---

## The Closure Relation

```
v_esc(r) × v_fall(r) = c²
```

This holds for ALL r and is independent of mass M. It is a purely geometric identity that connects the two fundamental gravitational velocities.

---

## Components

```
v_esc(r) = c · √(r_s / r)     (escape velocity)
v_fall(r) = c · √(r / r_s)     (free-fall velocity from infinity)
```

Product:
```
v_esc × v_fall = c · √(r_s/r) × c · √(r/r_s) = c²
```

---

## Significance

1. **Mass-independence:** The product c² does not depend on M, r_s, or any object property
2. **Universality:** Holds at every radius, from r → ∞ to r = r_s
3. **Duality:** v_esc and v_fall are reciprocals in units of c
4. **At r = r_s:** Both velocities equal c (the "mirror point")
5. **Conservation-like:** The product is conserved along any radial trajectory

---

## Connection to SSZ Observables

The kinematic closure connects to:
- **Time dilation:** v_esc²/c² = r_s/r = 2Ξ_weak
- **Redshift:** z ≈ v_esc²/(2c²) in the weak field
- **Energy:** E_kin = ½mv_fall² maps to the gravitational potential

---

## Test

| Test | Repository |
|------|------------|
| test_vfall_duality.py | segmented-calculation-suite |

---

© 2025–2026 Carmen N. Wrede, Lino P. Casu
