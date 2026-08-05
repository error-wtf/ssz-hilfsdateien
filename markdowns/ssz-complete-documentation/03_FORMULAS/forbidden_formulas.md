# Forbidden Formulas (Anti-Patterns)

---

## 1. Old Strong-Field Formula (DEPRECATED)

```python
# BANNED — do not use:
Xi = (r_s/r)**2 * exp(-r/r_phi)    # DEPRECATED!

# CORRECT:
Xi_strong = min(1 - exp(-phi * r_s / r), Xi_max)  # CANONICAL (saturation form)
```

---

## 2. Ξ-Inversion Trap

```python
# MISLEADING — this is an identity, not a calculation:
z_ssz = 1/D_ssz - 1   # = Ξ(r), no new information!

# CORRECT understanding:
z_ssz = 1/D_ssz - 1 = Ξ(r)   # Identity, not derivation
```

---

## 3. Δ(M) in Weak Field (FORBIDDEN)

```python
# WRONG:
if regime == "weak":
    z_ssz = z_gr * (1 + delta_m/100)   # NO!

# CORRECT:
if regime == "weak":
    z_ssz = z_gr   # EXACT, no modification!
```

---

## 4. PPN for Time Dilation (WRONG METHOD)

```
# WRONG:
D(r) = 1 - (1+γ)·r_s/(2r)   # NO!

# CORRECT:
D(r) = 1/(1 + Ξ(r))          # ALWAYS
```

---

## 5. Wrong Schwarzschild Radius

```
# WRONG (missing factor 2):
r_s = GM/c²

# CORRECT:
r_s = 2GM/c²
```

---

## 6. Wrong D Definition

```
# WRONG:
D = 1/(1 + 2Ξ)

# CORRECT:
D = 1/(1 + Ξ)    # No factor 2!
```

---

## 7. Mixing Regimes Without Blend

```python
# WRONG — creates discontinuity:
if r/r_s > 2.0:
    xi = r_s/(2*r)     # weak
else:
    xi = min(1 - exp(-phi*r_s / r), Xi_max)  # strong (saturation)

# CORRECT — use C² blend zone:
if r/r_s > 2.2:
    xi = r_s/(2*r)
elif r_s/r < 1.8:
    xi = min(1 - exp(-phi*r_s / r), Xi_max)
else:
    xi = hermite_c2_blend(r, r_s)  # smooth transition
```

---

## 8. Using 90/110 as Regime Boundaries

The values 90 and 110 in `unified_validation.py` are **PROBE_RADII** (test sampling points), NOT physical regime thresholds. The actual boundaries are **1.8** and **2.2** (r/r_s).
