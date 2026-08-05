# Segment-Based Group Velocity

**Status:** CANONICAL
**Paper:** 08 — Segment-Based Group Velocity

---

## Definition

In segmented spacetime, the group velocity of a wave packet is:
```
v_group = L_seg · f / N
```

where:
- L_seg = segment length (determined by Ξ)
- f = frequency
- N = number of segments traversed

---

## Physical Interpretation

In standard physics, group velocity is dω/dk. In SSZ, the segmentation introduces a discrete-like structure:

- Each segment has a characteristic length L_seg that depends on local Ξ
- A wave propagating through N segments carries frequency f
- The effective group velocity is modified by the segmentation density

In the weak field (Ξ → 0), L_seg → continuous and v_group → c (standard result).

In the strong field, the modified group velocity produces:
- Modified dispersion relations
- Frequency-dependent propagation effects
- Additional delay terms beyond standard Shapiro

---

## Connection to Light Travel Time

The segment-based group velocity contributes to the additive light-travel time decomposition:
```
Δt_total = Δt_flat + Δt_grav
Δt_grav = ∫ (s(r) - 1) dr/c = ∫ Ξ(r) dr/c
```

The gravitational delay is the integral of Ξ along the path — a direct consequence of the modified group velocity through segmented spacetime.

---

## Tests

| Test | Repository |
|------|------------|
| test_group_velocity.py | frequency-curvature-validation |

---

© 2025–2026 Carmen N. Wrede, Lino P. Casu
