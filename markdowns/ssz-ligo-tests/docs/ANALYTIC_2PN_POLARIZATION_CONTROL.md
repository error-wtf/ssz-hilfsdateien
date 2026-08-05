# ANALYTIC_2PN_POLARIZATION_CONTROL

**Version:** 1.0  
**Date:** 2026-05-18  
**Status:** ANALYTIC_2PN_CONTROL_APPROXIMATION  
**Purpose:** Break 0PN polarization degeneracy for twist-branch testing

**NOT a final GR PE waveform. Not fitted to data. No posterior used.**  
**READY_FOR_REAL_LIGO_SSZ_CLAIM: NO**

---

## 1. The 0PN Degeneracy Problem

At 0PN (leading order), the two GW polarisations for a quasi-circular
inspiral are:

```
h_+(f) = A(f) * (1 + cos²i) / 2  *  exp(i Psi(f))
h_×(f) = A(f) *   cos(i)          *  exp(i Psi(f) - i pi/2)
```

The cross polarisation is exactly `-i` times the plus polarisation
(at fixed inclination), scaled by `2 cos(i) / (1 + cos²i)`:

```
h_×(f) = -i * [2 cos(i) / (1 + cos²i)] * h_+(f)

=> h_× / h_+ = constant (independent of f) at 0PN
```

This means at 0PN the SO(2) rotation R(theta) acting on (h+, h×)
**does not change the norm of the pair** AND produces a frequency-
independent phase shift — which is equivalent to a constant rotation
of the (complex) polarisation state. Because the frequency structure
is identical in h+ and h×, any theta(f) twist integrates to the same
result as a constant theta at the level of RMS amplitudes.

**Consequence:** The H1/L1 projection ratio

```
rms(F+^H1 h+^SSZ + Fx^H1 hx^SSZ) / rms(F+^L1 h+^SSZ + Fx^L1 hx^SSZ)
```

does NOT shift under a frequency-dependent twist theta(f) when applied
to 0PN templates, because the frequency structure of h+ and h× are
identical up to a global phase factor.

---

## 2. Why 2PN Breaks the Degeneracy

At 2PN order, the amplitude corrections (beyond leading order) enter
asymmetrically in h+ and h×. The standard analytic TaylorF2 waveform
(see Arun et al. 2004, PRD 71 084008; Blanchet et al. reviews) gives:

```
h+(f) = A_0(f) * H+(f,Mc,eta,iota) * exp(i Psi_2PN(f))
h×(f) = A_0(f) * H×(f,Mc,eta,iota) * exp(i Psi_2PN(f))
```

where H+ and H× are **distinct amplitude series in (pi M f)^{1/3}**:

```
H+(f) = H+_0 + H+_1PN * x + H+_1.5PN * x^{3/2} + H+_2PN * x^2
H×(f) = H×_0 + H×_1PN * x + H×_1.5PN * x^{3/2} + H×_2PN * x^2

x = (pi M_total f G/c^3)^{2/3}   [PN expansion parameter]
```

The 1.5PN and 2PN coefficients of H+ and H× are **different** because
they encode different spin-orbit and mass-ratio effects. At face-on
inclination (iota=0), H× = 0 exactly, but at generic iota the two
polarisations have different frequency-dependent amplitudes.

**Consequence for twist:** With 2PN templates, h+(f) and h×(f) have
different frequency envelopes. A frequency-dependent twist theta(f)
will mix them in a frequency-dependent way that **cannot** be absorbed
into a global phase. This makes the H1/L1 amplitude ratio genuinely
sensitive to theta(f).

---

## 3. Formulas Implemented

### Leading order (0PN)

```
A_0(f) = C * (pi Mc)^{5/6} * f^{-7/6}   [Fourier amplitude]

H+_0 = (1 + cos²iota) / 2
H×_0 = cos(iota)

Psi_0(f) = 2 pi f t_c - phi_c - pi/4
           + (3/(128 eta)) * (pi Mc^{5/3} G/c^3)^{-5/3} * f^{-5/3}
```

### 1PN amplitude correction

```
x = (pi M_total G f / c^3)^{2/3}

H+_1PN = [(19/6) + (3/2)eta - (1/3)eta^2
          + ((-19/6) + (11/6)eta) * cos(2iota)] * x

H×_1PN = [cos(iota) * (17/6 - (5/6)eta)] * x
         + higher terms
```

### 1.5PN amplitude (tail terms — only phase enters at this order
for non-spinning; amplitude correction enters at 2.5PN for tails,
so 1.5PN amplitude is zero for circular non-spinning)

```
H+_1.5PN = 0   [for non-spinning, circular, in amplitude]
H×_1.5PN = 0
```

### 2PN amplitude correction

```
H+_2PN = [(5/24)(22 - 92eta + 96eta^2)
          + cos(2iota) * ((-9/8)(2 - 4eta + 3eta^2))] * x^2

H×_2PN = [cos(iota) * ((5/8)(2 + 10eta - 22eta^2))
          + (sin^2(iota) corrections)] * x^2
```

**Key point:** The 2PN coefficients of H+ and H× depend on eta
differently, so the frequency-domain ratio H+(f)/H×(f) is genuinely
frequency-dependent at 2PN.

### Phase

2PN TaylorF2 phase (non-spinning, aligned):

```
Psi(f) = 2 pi f t_c - phi_c - pi/4
         + (3/(128 eta)) * u^{-5} * [
             1                        (0PN)
             + (20/9)(743/336 + 11/4 eta) * u^2    (1PN)
             - 16 pi * u^3                          (1.5PN)
             + 10 * (3058673/1016064 + 5429/1008 eta + 617/144 eta^2) * u^4
           ]

u = (pi M_total G f / c^3)^{1/3}
```

---

## 4. Inclination Dependence

At iota = 0 (face-on):
- H+ = (1+1)/2 = 1, H× = 1
- Most sensitive to both polarisations

At iota = pi/2 (edge-on):
- H+ = 0, H× = 0 (signal vanishes at exact edge-on)
- Actually H+_0 = 1/2, H×_0 = 0 at edge-on

At iota = pi/4:
- H+_0 = (1 + 1/2)/2 = 3/4, H×_0 = 1/sqrt(2)
- Asymmetric: h+ has larger amplitude than h×
- This is the most informative inclination for twist detection

**Rule:** Test twist sensitivity at iota = pi/4 (45 degrees) as
the canonical non-degenerate inclination.

---

## 5. What This Module Is NOT

```
NOT a replacement for:
  - LALSuite IMRPhenomD / SEOBNRv4 waveforms
  - Posterior-sampled templates
  - Full inspiral-merger-ringdown model
  - Calibrated amplitude with distance

IS:
  - Analytic control approximation for twist degeneracy testing
  - Correct in the inspiral regime (f << f_ISCO)
  - Sufficient to show that 2PN breaks the 0PN degeneracy
  - Not to be used for final SSZ claim
```

---

## 6. Gate Status

```
POLARIZATION_CONTROL:            ANALYTIC_2PN_APPROXIMATION
PN_ORDER:                        2PN_AMPLITUDE + 2PN_PHASE
INCLINATION_DEPENDENCE:          IMPLEMENTED
SPIN:                            NOT_INCLUDED (non-spinning)
MERGER_RINGDOWN:                 NOT_INCLUDED
POSTERIOR_PARAMETERS_USED:       NO
REAL_DATA_FITTING:               NO
READY_FOR_REAL_LIGO_SSZ_CLAIM:   NO
SSZ_SUPPORT_CLAIM_MADE:          NO
```
