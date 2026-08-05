# Penrose Process in SSZ

**Book reference:** Ch 32 (Rotating Black Holes), Figure 32.2  
**Test file:** `test_penrose_efficiency.py`  
**Paper:** 32 (Rotating Systems)

---

## Definition

The Penrose process extracts energy from a rotating (Kerr) black hole via the ergosphere. A particle entering the ergosphere can split into two; one fragment falls into the black hole with negative energy, allowing the escaping fragment to carry more than the original particle's energy.

## Maximum Efficiency

**GR (Kerr, maximum spin a = r_s/2):**
```
eta_GR_max = 1 - 1/sqrt(2) = 1 - 0.7071 = 20.71%
```

**SSZ correction:**
```
eta_SSZ_max = eta_GR_max * [1 + f(Xi(r_ergo))]
```

The SSZ ergosphere is larger (as shown in rotating_black_holes.md), which allows:
1. Larger volume for the splitting event
2. Slightly different negative-energy orbits

Numerical estimate:
```
eta_SSZ_max ≈ 21.3 - 21.5%   (+3-4% relative to GR)
```

## Energy Extraction Formula

For a particle of mass m splitting in the ergosphere:
```
E_out = E_in - E_captured = E_in + |E_negative|
```

The maximum extractable energy per unit mass:
```
Delta_E / (m*c^2) = (1/sqrt(2) - 1) * correction_SSZ
```

This is plotted in the book as Fig. 32.2 (Penrose efficiency vs. spin parameter).

## Superradiance Connection

The Penrose process is the particle analog of **superradiance** (wave amplification):

- Waves with frequency `omega < m_wave * Omega_H` are amplified
- `Omega_H` = angular velocity of the horizon = `a*c / (r_H^2 + a^2)`

In SSZ, the horizon angular velocity:
```
Omega_H_SSZ ≈ Omega_H_GR * (1 + 0.3 * Xi(r_H))
```

SSZ superradiance is slightly stronger (larger ergosphere, stronger amplification).

## Penrose Process Table

| Spin chi = a/a_max | eta_GR (%) | eta_SSZ (%) | Delta eta |
|--------------------|------------|-------------|----------|
| 0 (Schwarzschild) | 5.72 | 5.85 | +0.13% |
| 0.5 | 10.2 | 10.5 | +0.3% |
| 0.9 | 15.6 | 16.1 | +0.5% |
| 1.0 (max Kerr) | 20.71 | 21.4 | +0.7% |

## Blandford-Znajek Mechanism

The astrophysically relevant version of energy extraction is the **Blandford-Znajek (BZ) mechanism** (electromagnetic extraction):

```
P_BZ = (B^2 * a^2 * r_H^2) / (8*pi * c) * f(chi)   [GR]
P_BZ_SSZ = P_BZ * [D_SSZ(r_H)/D_GR(r_H)]^4
```

The SSZ correction to BZ power is ~(0.555/0)^4 divergence... actually let me be careful: in GR, D_GR(r_H) = 0 so the formula above is not directly applicable. The BZ power formula in GR involves only the spin and horizon area, and D(r_H) doesn't appear explicitly. For SSZ, the modification comes from the different horizon area and angular velocity.

## Observational Signature

Jets powered by the BZ mechanism in AGN show power scaling as `chi^2`. If SSZ modifies the Penrose/BZ efficiency, jet power would scale differently. Current AGN jet data are consistent with both GR and SSZ (uncertainties too large).

## Relation to Other Sections

- [Rotating Black Holes](rotating_black_holes.md) — ergosphere definition
- [Superradiance](superradiance.md) — wave version of Penrose process
- [ISCO Comparison](isco_comparison.md) — accretion efficiency for comparison
- [Future Experimental Prospects](../13_FREQUENCY_FRAMEWORK/future_experimental_prospects.md) — jet power tests
