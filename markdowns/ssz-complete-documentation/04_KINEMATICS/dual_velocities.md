# Dual Velocities

**Status:** CANONICAL
**Paper:** 02 — Dual Velocities in Segmented Spacetime

---

## The Dual Velocity Pair

SSZ defines two fundamental velocities at any radius r from a gravitating mass:

### Escape Velocity
```
v_esc(r) = c · √(r_s / r)
```
The velocity needed to escape the gravitational well from radius r.

### Fall Velocity
```
v_fall(r) = c · √(r / r_s) = c² / v_esc(r)
```
The velocity acquired by infalling matter at radius r (from rest at infinity).

---

## The Kinematic Closure Invariant

```
v_esc(r) × v_fall(r) = c²    for ALL r, independent of M
```

This is a **universal invariant**:
- Mass-independent
- Holds at every radius
- Connects escape and infall dynamics
- Not present in standard GR treatments (but consistent with GR)

### Proof
```
v_esc × v_fall = c·√(r_s/r) × c·√(r/r_s) = c² · √(r_s/r · r/r_s) = c² · √1 = c²  ✓
```

---

## Physical Interpretation

| Property | v_esc | v_fall |
|----------|-------|--------|
| At r → ∞ | 0 | ∞ (unphysical limit) |
| At r = r_s | c | c |
| At r = 4r_s | c/2 | 2c (coordinate) |
| Direction | Outward | Inward |
| Role | Energy barrier | Free-fall gain |

At the Schwarzschild radius, both velocities equal c. This is the natural "exchange point" where the two descriptions meet.

---

## Connection to Time Dilation

The dual velocities connect to the time-dilation factor:
```
v_esc²/c² = r_s/r = 2·Ξ_weak(r)
```

So in the weak field:
```
D_SSZ ≈ 1 - Ξ ≈ 1 - v_esc²/(2c²)
```
This recovers the standard gravitational time dilation.

---

## Infalling Matter

For matter with its own velocity v_eigen falling into a gravitational well:
```
v_total = v_fall + v_eigen
```

The total velocity determines the effective regime and the segmentation experienced by the infalling object.

---

## Tests

| Test | Repository |
|------|------------|
| test_dual_velocities.py | segmented-calculation-suite |
| test_vfall_duality.py | segmented-calculation-suite |

---

© 2025–2026 Carmen N. Wrede, Lino P. Casu
