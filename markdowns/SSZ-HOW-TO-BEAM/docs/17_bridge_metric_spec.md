# Bridge Metric Specification

**Status:** CANONICAL for BEAM-SSZ v0.6
**Module:** `src/beam_ssz/bridge_metric.py`

---

## Core Solution

The mathematical solution for real-beaming is:

> **Not moving Carmen through space. Not copying. Not scanning.
> But modeling A and B as two boundary surfaces of a common bridge metric.**

Not transport through normal distance (L), but a **new effective transfer corridor** with its own coordinate (u).

---

## Bridge Coordinate System

We define two real locations:

```
A = (r_A, t_A)
B = (r_B, t_B)
```

Introduce bridge coordinate:

```
u ∈ [-1, 1]

u = -1  ⇒  A
u = +1  ⇒  B
```

The person moves not along normal spatial distance L(A,B), but along a continuous worldline in the bridge channel:

```
x^μ(τ) = (t(τ), u(τ), θ₀, φ₀)

with:
  u(τ₁) = -1
  u(τ₂) = +1
  τ₂ > τ₁
```

**Key point:** One worldline, no copying.

---

## The Metric

First hard approach:

```
ds² = -D_B²(u)c²dt² + A_B²(u)du² + R_B²(u)dΩ²
```

where:

```
D_B(u) = 1/(1 + Ξ_B(u))
A_B(u) = 1 + Ξ_B(u) = 1/D_B(u)
```

Thus SSZ-like:

```
s_B(u) = 1 + Ξ_B(u) = 1/D_B(u)
```

The bridge is an SSZ extension:

```
ds² = -D_B²c²dt² + s_B²du² + R_B²dΩ²
```

This is the mathematical beam-metric.

---

## Bridge Segment Density

We need Ξ_B(u). Not arbitrary fantasy, but smooth coupling between A and B:

```
Ξ_B(u) = (1-w(u))Ξ_A + w(u)Ξ_B + λ·q(u)
```

with:

```
w(u) = ½(1+u)
q(u) = (1-u²)²
```

Properties:

```
q(-1) = 0
q(+1) = 0
q(0) = 1
```

At start and end, the bridge fits cleanly to A and B. In the middle, the actual coupling zone forms.

λ is the free mathematical coupling parameter.

- λ = 0: pure interpolation
- λ > 0: genuine segment condensation in bridge throat

---

## Effective Distance

Normal distance:

```
L_normal(A,B)
```

Bridge distance:

```
L_bridge = ∫_{-1}^{1} s_B(u)·ℓ₀ du
```

ℓ₀ is the physical scale of the bridge channel.

For beaming foundations, we need:

```
L_bridge ≪ L_normal

η = L_bridge / L_normal → 0
```

This is the mathematical beam effect:

- Not superluminal
- Not copy
- But: different effective distance

---

## Worldline Condition

For a massive person:

```
g_μνu^μu^ν = -c²
```

with:

```
u^μ = dx^μ/dτ
```

For pure motion through bridge channel:

```
-D_B²c²(dt/dτ)² + s_B²(du/dτ)² = -c²
```

Rearranged:

```
(dt/dτ)² = (1/D_B²)[1 + (s_B²/c²)(du/dτ)²]
```

Since D_B > 0, proper time remains well-defined.

Hard conditions:

```
D_B(u) > 0
s_B(u) > 0
dτ/dt > 0
```

If satisfied, worldline remains timelike.

---

## No-Copy Condition

Identity not modeled as data copy, but as continuity:

```
C_A ≡ C_B
```

More precisely:

```
C(τ₁) = A
C(τ₂) = B
C(τ) continuous for all τ ∈ [τ₁, τ₂]
```

This is mathematically cleaner than any scan idea.

---

## Tidal Condition

Body must not be torn apart:

```
Δa^μ = -R^μ_{ νρσ}u^νξ^ρu^σ
```

must remain small.

First test:

```
|Δa| < a_max
```

Initially set conservatively:

```
a_max = 10g
```

for theoretical limit. Later can be made stricter.

---

## Causality Condition

No closed timelike curves:

```
CTC = 0
```

Practical first repo test:

```
g_tt < 0
g_uu > 0
D_B(u) > 0
det(g_μν) ≠ 0
t(τ) strictly monotonic
```

Thus:

```
dt/dτ > 0
```

---

## Energy Back-Calculation

Hard part: from bridge metric compute:

```
G_μν
```

and from that:

```
T_μν^eff = (c⁴/8πG) G_μν
```

Then test:

```
T_μνk^μk^ν ≥ 0  ?
```

If:

```
T_μνk^μk^ν ≥ 0  →  NEC satisfied
```

If:

```
T_μνk^μk^ν < 0  →  not canonical SSZ anymore, but:
```

```
GR_EXOTIC
```

Mathematically allowed to continue testing.

This is the desired line:

> Not forbid — classify.

---

## Mathematical Test Plan

For each candidate:

### 1. Regularity

```
D(u) > 0
s(u) > 0
R(u) > 0
det(g) ≠ 0
```

### 2. Worldline

```
g_μνu^μu^ν = -c²
```

### 3. Distance Reduction

```
η = L_bridge / L_normal
```

Target: η ≪ 1

### 4. Tidal

```
|Δa| < a_max
```

### 5. Causality

```
dt/dτ > 0
CTC = 0
```

### 6. Energy Class

```
T_μν^eff = (c⁴/8πG) G_μν
```

Then classify:

```
SSZ_CANONICAL
SSZ_EXTENSION
GR_EXOTIC
TOY_MODEL
INCONSISTENT
```

---

## Result

The solution is:

> **Real-beaming mathematically as continuous worldline through an SSZ-bridge-metric.**

Not:

> Matter scanning

Not:

> Quantum state copying

But:

> **A and B become boundary surfaces of a common effective metric space.**

This is the best approach because it:

- Does not copy identity
- Preserves proper time
- Is mathematically testable
- Can be formulated SSZ-compatibly
- Does not forbid exotic cases but classifies them
- Can be directly cast into code

---

## Module Interface

```python
from beam_ssz.bridge_metric import SSZBridgeMetric, create_canonical_bridge, test_bridge_candidate

# Create bridge
bridge = create_canonical_bridge(
    xi_a=0.1,
    xi_b=0.2,
    lambda_bridge=0.3,
    ell0=1e-3,  # 1mm scale
    throat_radius=1e-2,  # 1cm
)

# Test candidate
passed = test_bridge_candidate(
    bridge,
    l_normal=1.0,  # 1 meter normal distance
    verbose=True,
)
```

---

© 2025–2026 Carmen N. Wrede, Lino P. Casu
