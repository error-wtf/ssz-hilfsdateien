# chord-partition

**SSZ Chord-Partition Eigenmodes** — parametric curves with golden ratio φ resonance.

**Authors:** Carmen N. Wrede & Lino P. Casu  
**License:** Anti-Capitalist Software License v1.4  
**Status:** [![CI](https://github.com/error-wtf/chord-partition/actions/workflows/ci.yml/badge.svg)](https://github.com/error-wtf/chord-partition/actions/workflows/ci.yml) ![Tests](https://img.shields.io/badge/tests-103%2F103-brightgreen) ![Pass Rate](https://img.shields.io/badge/pass_rate-100%25-brightgreen)

---

## What This Repository Does

Implements and tests **parametric chord-partition curves** with golden-ratio φ scaling:

```
C(t; p, k, R) = (R·cos(p·t), R·sin(k·t))
```

These curves encode fundamental SSZ (Segmented Spacetime) constants — particularly φ, Ξ_max, and D_min — through their geometric and eigenmode structure.

---

## Quick Start

```bash
git clone https://github.com/error-wtf/chord-partition.git
cd chord-partition
pip install -r requirements.txt
pytest test_chord_partition_modes.py -v
```

Expected output: **103 passed, 0 failed**

---

## SSZ Constants Verified

| Constant | Value | Derivation | Meaning |
|----------|-------|------------|---------|
| φ (phi) | 1.6180339887498949 | (1+√5)/2 | Golden ratio — SSZ saturation growth function |
| Ξ_max | 0.80171 | 1 − e^−φ | Maximum segment density at horizon |
| D_min | 0.55503 | 1/(1+Ξ_max) | Minimum time dilation factor (FINITE at r_s) |
| r*/r_s | 1.387 | Ξ_strong = Ξ_weak intersection | Universal strong-field regime boundary |
| φ² = φ+1 | — | defining property | Structural self-similarity |
| 1/φ = φ−1 | — | defining property | Reciprocal identity |

**Critical invariant:** GR predicts D(r_s) = 0 (singularity). SSZ predicts D(r_s) = **0.55503** (finite). This is the central falsifiable prediction.

---

## Chord-Partition Theory

### Parametric Curve

```
C(t; p, k, R) = (R·cos(p·t), R·sin(k·t))
```

| Parameter | Definition |
|-----------|------------|
| p, k | winding numbers (integers ≥ 1) |
| R | characteristic radius |
| Period | T = 2π·lcm(p,k)/p |
| Eigenmode index | n = lcm(p,k)/gcd(p,k) |
| φ-resonance | Fibonacci pairs (5,8), (8,13), (13,21) → φ |

### φ-Resonance

Consecutive Fibonacci pairs approach φ monotonically:

| Pair (p,k) | k/p | Distance to φ |
|------------|-----|---------------|
| (3,5) | 1.6667 | 0.049 |
| (5,8) | 1.6000 | 0.018 |
| (8,13) | 1.6250 | 0.007 |
| (13,21) | 1.6154 | 0.003 |

### Eigenmode Index

```
n = lcm(p,k) / gcd(p,k)
```

Physical interpretation: number of independent spacetime segments per closed orbit.

---

## Test Suite Structure (103 tests)

| Class | Tests | What is tested |
|-------|-------|----------------|
| `TestClosure` | 19 | Curve closes after one period; period formula; origin pass |
| `TestDerivatives` | 19 | Derivative finite; curvature scaling; periodic derivative |
| `TestEigenmodes` | 12 | Eigenmode index; winding numbers; consistency |
| `TestPhiResonance` | 9 | φ value; Fibonacci convergence; resonance ordering |
| `TestPerimeter` | 12 | Arc length; R-scaling; positivity |
| `TestStability` | 8 | Stability score; circle most stable; complexity ordering |
| `TestNumerical` | 10 | Large winding; coprime closure; radius scaling |
| `TestSSZConstants` | 14 | φ², 1/φ, Ξ_max, D_min, r*/r_s — all SSZ invariants |

Run individually:
```bash
pytest test_chord_partition_modes.py::TestSSZConstants -v
pytest test_chord_partition_modes.py::TestPhiResonance -v
```

---

## Part of the SSZ Test Ecosystem

This repo is included in [ssz-all-tests](https://github.com/error-wtf/ssz-all-tests) as the `chord-partition` suite:

| Repository | Tests | Status | Domain |
|-----------|-------|--------|--------|
| [ssz-all-tests](https://github.com/error-wtf/ssz-all-tests) | 1296 | ✅ 100% | Complete SSZ validation |
| **chord-partition** *(this repo)* | **103** | **✅ 100%** | **Eigenmodes, golden ratio φ** |

---

## Dependencies

Minimal — only standard scientific Python:

```
numpy>=1.21.0
scipy>=1.7.0
pytest>=7.0.0
```

Install: `pip install -r requirements.txt`

---

## License

Anti-Capitalist Software License v1.4  
Copyright © 2025–2026 Carmen N. Wrede & Lino P. Casu
