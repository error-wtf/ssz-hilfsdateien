# SSZ Schumann Theory

**Theoretical foundations for SSZ analysis of Schumann resonances**

---

## 1. Classical Schumann Resonances

### 1.1 Physical Background

The Earth-ionosphere cavity forms a natural electromagnetic resonator. Lightning discharges excite extremely low frequency (ELF) waves that propagate around the globe in this waveguide. The resonant frequencies are called Schumann resonances.

### 1.2 Ideal Spherical Cavity

For an ideal conducting sphere of radius R, the resonant frequencies are:

```
f_n = c / (2*pi*R) * sqrt(n*(n+1))
```

where:
- n = mode number (1, 2, 3, ...)
- c = speed of light
- R = Earth radius

For Earth (R = 6371 km):
- f1_ideal = 10.59 Hz
- f2_ideal = 18.35 Hz
- f3_ideal = 25.95 Hz

### 1.3 Real Earth-Ionosphere System

The observed frequencies are lower due to:
- Finite ionospheric conductivity
- Non-zero ground conductivity
- Ionospheric height variations
- Day/night asymmetry

This is captured by an effective slowdown factor eta:

```
f_n = eta * c / (2*pi*R) * sqrt(n*(n+1))
```

With eta ≈ 0.74, we get:
- f1 ≈ 7.83 Hz
- f2 ≈ 14.3 Hz
- f3 ≈ 20.8 Hz

---

## 2. SSZ Theory Application

### 2.1 Segmented Spacetime

The Segmented Spacetime (SSZ) theory proposes that spacetime is divided into discrete segments, with segment density depending on local conditions. The key parameter is:

```
Xi(r) = 1 - exp(-phi * r_s / r)
```

where:
- phi = golden ratio ≈ 1.618
- r_s = characteristic scale

### 2.2 SSZ Correction Factor

The SSZ theory predicts an additional time dilation effect:

```
D_SSZ = 1 + delta_seg
```

where delta_seg is the effective segmentation parameter.

The corrected frequency is:

```
f_n^(SSZ) = f_n^(classical) / D_SSZ
```

### 2.3 Key SSZ Signature

**The relative frequency shift is identical for all modes:**

```
Delta_f_n / f_n = -delta_seg / (1 + delta_seg) ≈ -delta_seg
```

This is fundamentally different from classical effects:
- **Classical:** Mode-dependent shifts (dispersion)
- **SSZ:** Uniform relative shift (no dispersion)

---

## 3. Layered SSZ Model

### 3.1 Atmospheric Layers

We model three layers:

1. **Ground (j = g):** Solid Earth boundary
2. **Atmosphere (j = atm):** Neutral atmosphere (0-50 km)
3. **Ionosphere (j = iono):** Conducting layer (50-300 km)

### 3.2 Layer Weights

Each layer contributes to the effective wave path:

```
D_SSZ = 1 + sum_j(w_j * sigma_j)
```

Default weights based on waveguide physics:
- w_g = 0.0 (hard boundary, no contribution)
- w_atm = 0.2 (small contribution)
- w_iono = 0.8 (main waveguide boundary)

### 3.3 Ionosphere Dominance

Since w_iono >> w_atm, the model simplifies to:

```
D_SSZ ≈ 1 + w_iono * sigma_iono
      = 1 + 0.8 * sigma_iono
```

### 3.4 Time-Varying Model

The ionosphere segmentation can vary with solar/geomagnetic activity:

```
sigma_iono(t) = beta_0 + beta_1 * F_iono(t)
```

where:
- beta_0 = baseline segmentation
- beta_1 = coupling to ionospheric proxy
- F_iono = normalized proxy (F10.7, Kp, etc.)

---

## 4. Testable Predictions

### 4.1 Mode Consistency

If SSZ effects are present:

```
delta_seg_1 ≈ delta_seg_2 ≈ delta_seg_3
```

This is quantified by the mode correlation:

```
r_12 = corr(delta_seg_1, delta_seg_2)
r_13 = corr(delta_seg_1, delta_seg_3)
r_23 = corr(delta_seg_2, delta_seg_3)

mean_correlation = (r_12 + r_13 + r_23) / 3
```

**SSZ signature:** mean_correlation > 0.7

### 4.2 Frequency Shift Magnitude

For 1% segmentation (delta_seg = 0.01):

```
Delta_f1 = f1 * (-0.01) / (1.01) ≈ -0.08 Hz
Delta_f2 ≈ -0.14 Hz
Delta_f3 ≈ -0.19 Hz
```

This is within the typical observed variation range (±0.1-0.2 Hz).

### 4.3 Correlation with Proxies

If SSZ is driven by ionospheric conditions:

```
corr(delta_seg, F10.7) ≠ 0
corr(delta_seg, Kp) ≠ 0
```

The sign indicates:
- Positive: Higher activity → more segmentation
- Negative: Higher activity → less segmentation

---

## 5. Distinguishing SSZ from Classical Effects

### 5.1 Classical Dispersive Effects

Classical ionospheric effects produce mode-dependent shifts:

```
Delta_f_n / f_n = A_n * Delta_h + B_n * Delta_sigma + ...
```

where A_n, B_n depend on mode number.

### 5.2 SSZ Non-Dispersive Effect

SSZ produces uniform relative shifts:

```
Delta_f_n / f_n = -delta_seg  (same for all n)
```

### 5.3 Diagnostic Test

Calculate the standard deviation of relative shifts:

```
std_rel = std([Delta_f_1/f_1, Delta_f_2/f_2, Delta_f_3/f_3])
```

- **SSZ dominant:** std_rel << mean_rel
- **Classical dominant:** std_rel ~ mean_rel

---

## 6. Connection to SSZ Core Theory

### 6.1 Segment Density

From ssz-metric-pure:

```
Xi(r) = 1 - exp(-phi * r_s / r)
```

### 6.2 Time Dilation

```
D(r) = 1 / (1 + Xi(r))
```

### 6.3 Effective Speed

```
c_eff = c / D(r)
```

### 6.4 Application to Schumann

For the Earth-ionosphere cavity:

```
sigma_iono = lambda * (Xi(r_iono) / Xi(r_0) - 1)
```

where:
- r_iono = ionosphere radius
- r_0 = reference radius
- lambda = coupling parameter

---

## 7. Expected Results

### 7.1 If SSZ is Present

- High mode correlation (>0.7)
- Low std across modes
- Correlation with ionospheric proxies
- Systematic frequency shifts

### 7.2 If SSZ is Absent

- Low mode correlation (<0.5)
- High std across modes
- Mode-dependent shifts
- Classical dispersive behavior

---

## 8. References

### SSZ Theory
1. Wrede, C. & Casu, L. (2025). Segmented Spacetime Theory.
2. SSZ Metric Pure: https://github.com/error-wtf/ssz-metric-pure

### Schumann Resonances
1. Schumann, W.O. (1952). Z. Naturforsch., 7a, 149-154.
2. Nickolaenko, A.P. & Hayakawa, M. (2002). Resonances in the Earth-Ionosphere Cavity.
3. Salinas, A. et al. (2022). Computers & Geosciences, 165, 105148.

### Ionospheric Physics
1. Kelley, M.C. (2009). The Earth's Ionosphere.
2. Rishbeth, H. & Garriott, O.K. (1969). Introduction to Ionospheric Physics.

---

**© 2025 Carmen Wrede & Lino Casu**
