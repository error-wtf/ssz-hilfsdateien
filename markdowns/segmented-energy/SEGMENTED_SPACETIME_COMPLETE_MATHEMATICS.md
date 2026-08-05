# Segmented Spacetime - Complete Mathematical Framework

**Vollständige mathematische Dokumentation der SSZ-Theorie**  
**Erstellt:** 2025-12-07  
**Quellen:** Alle segmented-related Repositories in e:\clone\

---

## Inhaltsverzeichnis

1. [Fundamentale Konstanten](#1-fundamentale-konstanten)
2. [Metrik-Formulierungen](#2-metrik-formulierungen)
3. [Segment-Dichte Ξ(r)](#3-segment-dichte-ξr)
4. [Zeit-Dilatation und Emergenz](#4-zeit-dilatation-und-emergenz)
5. [Masse-Projektion und Δ(M)](#5-masse-projektion-und-δm)
6. [Duale Geschwindigkeiten](#6-duale-geschwindigkeiten)
7. [Redshift-Formeln](#7-redshift-formeln)
8. [Tensor-Formulierung (4D)](#8-tensor-formulierung-4d)
9. [Christoffel-Symbole](#9-christoffel-symbole)
10. [Einstein- und Ricci-Tensoren](#10-einstein-und-ricci-tensoren)
11. [Geodätische Gleichungen](#11-geodätische-gleichungen)
12. [PPN-Parameter](#12-ppn-parameter)
13. [Energie-Bedingungen](#13-energie-bedingungen)
14. [Schwarzes Loch Physik](#14-schwarzes-loch-physik)
15. [Krümmungsinvarianten](#15-krümmungsinvarianten)
16. [φ-Spiral Geometrie](#16-φ-spiral-geometrie)
17. [Euler-Verbindung](#17-euler-verbindung)
18. [Observable und Vorhersagen](#18-observable-und-vorhersagen)
19. [Numerische Methoden](#19-numerische-methoden)
20. [Kosmologische Anwendungen](#20-kosmologische-anwendungen)

---

## 1. Fundamentale Konstanten

### 1.1 φ - Der Goldene Schnitt (ZENTRAL!)

```
φ = (1 + √5) / 2 = 1.618033988749894...
```

**Eigenschaften:**
```
φ² = φ + 1 = 2.618033988749...
1/φ = φ - 1 = 0.618033988749...
φⁿ = F_n·φ + F_{n-1}  (Fibonacci-Beziehung)
```

**Rolle in SSZ:**
- KEINE fitting parameter, sondern geometrische Notwendigkeit
- φ-Spiral-Geometrie für self-similar scaling
- Universeller Crossover verknüpft mit φ
- Natürliche Grenze: r_φ = (φ/2)r_s
- Erscheint in ALLEN SSZ-Relationen

### 1.2 Physikalische Konstanten

```python
G = 6.67430e-11         # m³ kg⁻¹ s⁻² (Gravitationskonstante)
c = 2.99792458e8        # m s⁻¹ (Lichtgeschwindigkeit)
ℏ = 1.054571817e-34     # J·s (Reduzierte Planck-Konstante)
h = 6.62607015e-34      # J·s (Planck-Konstante)
k_B = 1.380649e-23      # J K⁻¹ (Boltzmann-Konstante)
α_fs = 7.2973525693e-3  # Fine structure constant
M_☉ = 1.98847e30        # kg (Sonnenmasse)
```

### 1.3 Abgeleitete Größen

**Schwarzschild-Radius:**
```
r_s = 2GM/c²
```

**Gravitationsradius:**
```
r_g = GM/c²  (= r_s/2)
```

**Planck-Skalen:**
```
l_P = √(ℏG/c³) ≈ 1.616×10⁻³⁵ m
t_P = √(ℏG/c⁵) ≈ 5.391×10⁻⁴⁴ s
m_P = √(ℏc/G) ≈ 2.176×10⁻⁸ kg
```

---

## 2. Metrik-Formulierungen

### 2.1 Diagonal (T,r) Form (EMPFOHLEN - v2.1.0+)

```
ds² = -(c²/γ²(r)) dT² + γ²(r) dr² + r²(dθ² + sin²θ dφ²)
```

**Metrische Funktionen:**
```
φ_G(r) = √(2GM/(rc²))     (Gravitationspotential-Funktion)
γ(r) = cosh(φ_G(r))       (Lapse-Funktion)
β(r) = tanh(φ_G(r))       (Geschwindigkeits-Funktion)
```

**2PN Kalibrierung (v2.1.0 - CURRENT):**
```
φ²_G(r) = 2U(1 + U/3)

mit U = GM/(rc²)
```

**1PN Kalibrierung (v2.0.0 - LEGACY):**
```
φ²_G(r) = 2U
```

**Vorteil 2PN:** Matcht GR bis O(U²) für schnellere Konvergenz

### 2.2 Original (t,r) Form

```
ds² = -c²(1-β²)dt² + 2βc dt dr + dr² + r²(dθ² + sin²θ dφ²)
```

**Koordinaten-Transformation:**
```
dT = dt - (β(r)γ²(r)/c) dr
```

**Physikalisch äquivalent** zur diagonalen Form (kovariante Transformation)

### 2.3 Schwarzschild-ähnliche Form

```
ds² = -A(r)c²dt² + B(r)dr² + r²(dθ² + sin²θ dφ²)
```

**Metrische Koeffizienten:**
```
A(U) = 1 - 2U + 2U² + ε₃U³ + O(U⁴)
B(r) = 1/A(r)
U = GM/(rc²) = r_s/(2r)
```

**ε₃-Parameter:**
```
ε₃ = -24/5 = -4.8  (aus PPN-Tests bestimmt)
```

### 2.4 Verbindungen zwischen Formen

**γ und β aus A:**
```
γ²(r) = 1/A(r)
β(r) = √(1 - A(r))
```

**A und B aus γ:**
```
A(r) = 1/γ²(r)
B(r) = γ²(r)
```

**Asymptotisches Verhalten (r → ∞):**
```
γ(r) → 1
β(r) → 0
A(r) → 1
B(r) → 1
```

---

## 3. Segment-Dichte Ξ(r)

### 3.1 Exponentielle Form (UNIVERSAL)

```
Ξ(r) = Ξ_max(1 - exp(-φr_s / r))
```

**Parameter:**
```
Ξ_max ≈ 0.8 - 1.0  (Sättigung)
φ = 1.618...        (Goldener Schnitt)
```

**Eigenschaften:**
- **Universeller Crossover bei r* = 1.386562 r_s**
- Massenunabhängig!
- φ-basierte natürliche Skala
- Glatter Übergang von diskret zu kontinuierlich

### 3.2 Hyperbolische Form (α-abhängig)

```
Ξ(r) = Ξ_max · tanh(α · r_s/r)
```

**Parameter:**
```
α = 1.0     (Standard)
Ξ_max < 1.0 (Sättigung)
```

**Eigenschaften:**
- Kontinuierliche Transition
- Kein Crossover bei α=1.0
- SSZ-Korrekturen bei ALLEN Radien
- Flexible Parameter-Anpassung

### 3.3 Ableitungen

**Erste Ableitung (exponentiell):**
```
dΞ/dr = (Ξ_max · φ/r_s) exp(-φr_s / r)
```

**Erste Ableitung (hyperbolisch):**
```
dΞ/dr = -(Ξ_max · α · r_s/r²) sech²(α · r_s/r)
```

### 3.4 Asymptotisches Verhalten

**Nahe Horizont (r → r_s):**
```
Ξ(r_s) ≈ Ξ_max(1 - exp(-φ)) ≈ 0.802 Ξ_max
```

**Weit entfernt (r → ∞):**
```
Ξ(r) → 0  (kontinuierliche Raumzeit)
```

**Im Zentrum (r → 0):**
```
Ξ(0) → Ξ_max  (maximale Segmentierung)
```

---

## 4. Zeit-Dilatation und Emergenz

### 4.1 GR vs SSZ Zeit-Dilatation

**General Relativity:**
```
D_GR(r) = √(1 - r_s/r)
```

**SSZ (mit Segment-Dichte):**
```
D_SSZ(r) = √(1 - r_s/r) · √(1 - Ξ(r))
```

**Alternative SSZ-Form:**
```
D_SSZ(r) = 1/(1 + Ξ(r))  (direkte Emergenz-Formel)
```

**Am Horizont (r = r_s):**
```
D_GR(r_s) = 0           (Singularität!)
D_SSZ(r_s) ≈ 0.667      (endlich!)
```

### 4.2 Zeit-Emergenz aus Segmenten

**Zeitintervall-Formel:**
```
Δt(r) = (1 + Ξ(r)) / φ
```

**Physikalische Interpretation:**
- Zeit entsteht aus φ-basierten Segment-Resonanzen
- Jeder Segment-Zustandsübergang = 1 "Tick"
- Zeit = Anzahl der Ticks

**Resonanzfrequenz:**
```
ω(r) = φ / (1 + Ξ(r))
```

**Asymptotisch:**
```
ω(∞) = φ ≈ 1.618  (natürliche Frequenz)
```

### 4.3 Universeller Intersektionspunkt

**Für exponentielle Ξ:**
```
r* / r_s = 1.386562  (UNIVERSAL!)
D*(r*) = 0.528007

Bei r*: D_GR(r*) = D_SSZ(r*) (exakt!)
```

**Herleitung:**
```
Setze D_GR = D_SSZ:
√(1 - r_s/r*) = 1/(1 + Ξ_max(1 - exp(-φr*/r_s)))

Numerische Lösung für Ξ_max = 1:
r*/r_s ≈ 1.386562
```

### 4.4 Proper Time

**Stationäre Uhr bei r:**
```
dτ = D(r) dt
```

**Accumulated proper time (Δt = 1000s):**
```
τ_GR(r) = 1000s · √(1 - r_s/r)
τ_SSZ(r) = 1000s / (1 + Ξ(r))
```

---

## 5. Masse-Projektion und Δ(M)

### 5.1 Φ-basierte Δ(M) Formel

```
Δ(M) = A · exp(-α · r_s) + B
```

**Parameter (NICHT arbiträr!):**
```
A = 98.01
α = 2.7177e4  (aus φ-Spiral Pitch abgeleitet!)
B = 1.96

mit r_s = 2GM/c²
```

**Wichtig:** α ist geometrisch aus φ-Spiral-Struktur hergeleitet

### 5.2 Normalisierung

```
L = log₁₀(M/M_☉)
L_min, L_max = Bereichsgrenzen im Datensatz

norm = (L - L_min) / (L_max - L_min)  falls L_max > L_min
       1                               sonst

Δ_percent(M) = Δ_raw(M) · norm
```

### 5.3 Mass-Radius Beziehung

**SSZ-korrigierter Radius:**
```
r_φ = (G·φ·M/c²) · (1 + Δ_percent/100)
    = (φ/2)r_s · (1 + Δ_percent/100)
```

**GR zum Vergleich:**
```
r_GR = r_s = 2GM/c²
```

### 5.4 Mass Inversion (Newton-Raphson)

**Zielfunktion:**
```
f(M) = r_φ(M) - r_obs = 0
```

**Ableitung:**
```
f'(M) = dr_φ/dM = (φG/c²)(1 + Δ_percent/100) + (φG·M/c²)·dΔ/dM
```

**Iteration:**
```
M_next = M - f(M)/f'(M)

mit Step Control:
if |step| > |M|:
    step *= 0.5
```

**Konvergenz-Kriterium:**
```
|f(M)| < 10⁻¹²⁰  UND  |ΔM/M| < 10⁻¹²⁰
```

**Max Iterationen:** 200

---

## 6. Duale Geschwindigkeiten

### 6.1 Fundamentale Dualität

**Escape Velocity (Newton):**
```
v_esc(r) = √(2GM/r) = c√(r_s/r)
```

**Dual Fall Velocity (SSZ):**
```
v_fall(r) = c²/v_esc(r) = c√(r/r_s)
```

**INVARIANTE:**
```
v_esc(r) · v_fall(r) = c²  (EXAKT!)
```

### 6.2 Herleitung der Dualität

**Aus GR-Redshift:**
```
γ_GR(r) = 1/√(1 - r_s/r) = (1 - (v_esc/c)²)^(-1/2)
```

**SSZ Segment-Faktor:**
```
γ_s(r) = 1/√(1 - (c/v_fall)²)
```

**Konsistenz-Forderung:**
```
γ_GR(r) = γ_s(r)

⇒ 1 - r_s/r = (c/v_fall)²
⇒ v_fall/c = √(r/r_s)
⇒ v_esc · v_fall = c²
```

### 6.3 Hyperbolische Darstellung

**Rapidity χ:**
```
v_esc/c = tanh(χ)
v_fall/c = coth(χ)
γ_s = cosh(χ)
r/r_s = coth²(χ)
```

**Gültig für:** r > r_s

### 6.4 Grenzfälle

**Weit entfernt (r → ∞):**
```
v_esc → 0
v_fall → ∞
γ_s → 1
```

**Am Horizont (r → r_s⁺):**
```
v_esc → c
v_fall → c
γ_s → ∞
```

### 6.5 Energie-Interpretation

**Lokale Energie:**
```
E_local = γ(u) m v_esc · v_fall = γ(u) m c²
```

**Energie bei ∞:**
```
E_∞ = E_local / γ_s(r) = γ(u)/γ_s(r) · mc²
```

---

## 7. Redshift-Formeln

### 7.1 Gravitativer Redshift

**GR-Formel:**
```
z_gr(M, r) = 1/√(1 - r_s/r) - 1
           = γ_GR(r) - 1
```

**Gültigkeitsbereich:** r > r_s, sonst NaN

### 7.2 Special Relativistic Redshift

**Lorentz-Faktoren:**
```
β = v_tot/c        (begrenzt auf 0.999999999999)
γ = 1/√(1 - β²)
β_los = v_los/c    (line-of-sight)
```

**SR-Redshift:**
```
z_sr = γ(1 + β_los) - 1
```

### 7.3 Kombinierter Redshift (GR + SR)

```
z_combined = (1 + z_gr)(1 + z_sr) - 1
```

### 7.4 SSZ Segment-basierter Redshift

**Mit Δ(M) Korrektur:**
```
z_gr_scaled = z_gr · (1 + Δ_percent/100)
z_seg = (1 + z_gr_scaled)(1 + z_sr) - 1
```

**Alternative φ-Lattice Form:**
```
R = f_emit/f_obs = φ^N,  N ∈ ℤ

1 + z = R = φ^N
```

**Residual zum nächsten Gitterpunkt:**
```
n*(R) = ln(R)/ln(φ)
ε(R) = n*(R) - round(n*(R))
```

### 7.5 Lyman-α Beispiel

**Rest-Wellenlänge:**
```
λ₀ = 121.567 nm
```

**Beobachtete Wellenlänge:**
```
λ_obs = λ₀(1 + z) = λ₀ · γ_s(r)
```

**Bei r = 2r_s:**
```
z ≈ 0.414
λ_obs ≈ 172 nm
```

**Bei r = 1.1r_s:**
```
z ≈ 2.32
λ_obs ≈ 403 nm (violett!)
```

---

## 8. Tensor-Formulierung (4D)

### 8.1 Metrischer Tensor (diagonal)

```
       ⎛ -c²/γ²    0       0          0     ⎞
       ⎜   0      γ²       0          0     ⎟
g_μν = ⎜   0       0      r²          0     ⎟
       ⎝   0       0       0    r²sin²θ     ⎠
```

**Komponenten:**
```
g_TT = -c²/γ²(r)
g_rr = γ²(r)
g_θθ = r²
g_φφ = r²sin²θ
```

### 8.2 Inverser metrischer Tensor

```
         ⎛ -γ²/c²    0         0              0        ⎞
         ⎜   0      1/γ²       0              0        ⎟
g^μν   = ⎜   0       0       1/r²            0        ⎟
         ⎝   0       0         0        1/(r²sin²θ)   ⎠
```

**Komponenten:**
```
g^TT = -γ²/c²
g^rr = 1/γ²
g^θθ = 1/r²
g^φφ = 1/(r²sin²θ)
```

### 8.3 Metrische Determinante

```
g = det(g_μν) = -c²r⁴sin²θ
```

### 8.4 Hilfsfunktionen

**λ-Funktion:**
```
λ(r) = ln(γ(r)) = ln(cosh(φ_G(r)))
```

**Ableitungen:**
```
λ'(r) = dλ/dr = β(r) · φ'_G(r)
λ''(r) = d²λ/dr² = (φ'_G)²/γ² + β · φ''_G
```

**φ_G Ableitungen:**
```
φ_G = √(2GM/(rc²))
φ'_G = dφ_G/dr = -φ_G/(2r)
φ''_G = d²φ_G/dr² = 3φ_G/(4r²)
```

---

## 9. Christoffel-Symbole

### 9.1 Nicht-verschwindende Komponenten (10 Stück)

**Zeitliche Komponenten:**
```
Γ^T_Tr = λ'/γ²
Γ^T_rT = λ'/γ²
```

**Radiale Komponenten:**
```
Γ^r_TT = c²λ'/γ²
Γ^r_rr = -λ'
Γ^r_θθ = -r/γ²
Γ^r_φφ = -(r sin²θ)/γ²
```

**Angulare Komponenten:**
```
Γ^θ_rθ = 1/r
Γ^θ_θr = 1/r
Γ^θ_φφ = -sinθ cosθ

Γ^φ_rφ = 1/r
Γ^φ_φr = 1/r
Γ^φ_θφ = cotθ
Γ^φ_φθ = cotθ
```

### 9.2 Symmetrie-Eigenschaften

```
Γ^ρ_μν = Γ^ρ_νμ  (symmetrisch in unteren Indizes)
```

**Spurbildung:**
```
Γ^ρ_ρμ = ∂_μ(ln√|g|)
```

---

## 10. Einstein- und Ricci-Tensoren

### 10.1 Einstein-Tensor G^μ_ν (Mixed Indices)

**Komponenten:**
```
G^T_T = (1/r²)[2rβφ'/γ² - 1/γ² + 1]

G^r_r = (1/r²)[1/γ² - 1] - (2βφ')/(rγ²)

G^θ_θ = G^φ_φ = (1/γ²)[-λ'' + 2(λ')² - 2λ'/r]
```

### 10.2 Ricci-Tensor R_μν (Lowered Indices)

**Komponenten:**
```
R_TT = (c²/γ²)[λ'' - 2(λ')² + 2λ'/r]

R_rr = γ²[-λ'' + 2(λ')² - 2λ'/r]

R_θθ = r²[(1/γ²) - 1 + rλ']

R_φφ = sin²θ · R_θθ
```

### 10.3 Ricci-Skalar R

**Methode 1 (Trace):**
```
R = g^μν R_μν = -G^μ_μ
```

**Methode 2 (Direkt):**
```
R = (2/γ²)[λ'' - 2(λ')² + 2λ'/r]
```

### 10.4 Ricci Squared

```
R_μν R^μν = (c⁴/γ⁴)[λ'' - 2(λ')² + 2λ'/r]²
           + (1/γ⁴)[λ'' - 2(λ')² - 2λ'/r]²
           + (2/r²)[(1/γ²) - 1 + rλ']²
```

---

## 11. Geodätische Gleichungen

### 11.1 Allgemeine Form

```
d²x^ρ/dλ² + Γ^ρ_μν (dx^μ/dλ)(dx^ν/dλ) = 0
```

**Für Koordinaten (T, r, θ, φ):**

**T-Gleichung:**
```
d²T/dλ² + 2Γ^T_Tr (dT/dλ)(dr/dλ) = 0
```

**r-Gleichung:**
```
d²r/dλ² + Γ^r_TT (dT/dλ)² + Γ^r_rr (dr/dλ)²
        + Γ^r_θθ (dθ/dλ)² + Γ^r_φφ (dφ/dλ)² = 0
```

**θ-Gleichung:**
```
d²θ/dλ² + 2Γ^θ_rθ (dr/dλ)(dθ/dλ)
        + Γ^θ_φφ (dφ/dλ)² = 0
```

**φ-Gleichung:**
```
d²φ/dλ² + 2Γ^φ_rφ (dr/dλ)(dφ/dλ)
        + 2Γ^φ_θφ (dθ/dλ)(dφ/dλ) = 0
```

### 11.2 Null-Geodäten

**Bedingung:**
```
ds² = 0
```

**Radiale Null-Geodäte (θ = const, φ = const):**
```
-(c²/γ²)(dT/dλ)² + γ²(dr/dλ)² = 0

⇒ dr/dT = ±c/γ²
```

**Auswärts (+):**
```
dr/dT = +c/γ²(r)
```

**Einwärts (-):**
```
dr/dT = -c/γ²(r)
```

### 11.3 Light Cone Closing

**Maß für Lichtkegel-Schließung:**
```
closing(r) = 1 - γ²(r)/γ²(∞)
           = 1 - 1/γ²(r)
           = 1 - A(r)
```

**Bei r = 10r_s (Erde):**
```
closing ≈ 9.37%
```

---

## 12. PPN-Parameter

### 12.1 Weak-Field Expansion

**A(U) Taylor-Entwicklung:**
```
A(U) = 1 - 2U + 2U² + O(U³)
     = 1 - 2U + 2βU² + O(U³)  (PPN-Form)
```

**B(U) Expansion:**
```
B(U) = 1/A(U) = 1 + 2U + 2(γ+1)U² + O(U³)
```

### 12.2 SSZ PPN-Werte

```
β_PPN = 1.000000000000  (kein bevorzugtes Bezugssystem)
γ_PPN = 1.000000000000  (GR-ähnliche Raum-Krümmung)
```

**Abweichung:**
```
|β_PPN - 1| < 10⁻¹²  (Maschinenpräzision!)
|γ_PPN - 1| < 10⁻¹²  (Maschinenpräzision!)
```

**Bedeutung:** SSZ matcht GR im Weak-Field-Limit EXAKT!

### 12.3 Observable Tests

**Periheldrehung (Merkur):**
```
Δφ = (6πGM)/(ac²(1-e²))  (pro Umlauf)
```

**Lichtablenkung:**
```
Δφ = (4GM)/(bc²) · (1 + γ_PPN)/2
```

**Shapiro Time Delay:**
```
Δt = (2GM/c³)(1 + γ_PPN) ln(r_E r_R/b²)
```

---

## 13. Energie-Bedingungen

### 13.1 Effektiver Stress-Energy Tensor

**Einstein-Feldgleichungen:**
```
G_μν = (8πG/c⁴) T_μν
```

**Komponenten aus Metrik:**
```
8πρ = (1-A)/r² - A'/r

8πp_r = A'/r + (A-1)/r²

8πp_t = A''/2 + A'/r
```

**Wichtige Relation:**
```
p_r = -ρc²  (radiale Spannung balanciert Dichte!)
```

### 13.2 Bedingungen

**WEC (Weak Energy Condition):**
```
ρ ≥ 0  UND  ρ + p_t ≥ 0
```

**DEC (Dominant Energy Condition):**
```
ρ ≥ |p_r|  UND  ρ ≥ |p_t|
```

**SEC (Strong Energy Condition):**
```
ρ + p_r + 2p_t ≥ 0
```

**NEC (Null Energy Condition):**
```
ρ + p_r = 0  (analytisch erfüllt für SSZ!)
```

### 13.3 Gültigkeitsbereiche

**Erfüllt für:** r ≥ 5r_s

**Verletzungen:** r < 5r_s (starkes Feld)
- Verletzungen kontrolliert und endlich
- Keine Divergenzen
- Physikalisch durch Segmentierung regularisiert

---

## 14. Schwarzes Loch Physik

### 14.1 Horizont-Struktur

**Schwarzschild-Radius:**
```
r_s = 2GM/c²
```

**SSZ Natural Boundary:**
```
r_φ = (φ/2)r_s ≈ 0.809 r_s

Zeit-Dilatation bei r_φ: endlich!
Krümmung bei r_φ: endlich!
```

### 14.2 Photon Sphere

**GR:**
```
r_ph = (3/2)r_s = 1.5 r_s
```

**SSZ:**
```
r_ph ≈ r_ph(GR)  (sehr ähnlich)
```

**Impact Parameter:**
```
b_ph = r_ph√(g_φφ/|g_TT|)
```

**SSZ zeigt ~6% offset vs GR**

### 14.3 ISCO (Innermost Stable Circular Orbit)

**GR:**
```
r_ISCO = 3r_s
```

**SSZ:**
```
r_ISCO ≈ r_ISCO(GR) + δr_SSZ

δr_SSZ > 0  (leicht vergrößert)
```

### 14.4 Schwarzes Loch Schatten

**Schattenradius:**
```
r_shadow(SSZ) ≈ r_shadow(GR) × 1.02

~2% größer als GR
```

**Testbar mit zukünftiger EHT-Auflösung**

### 14.5 Energie-Dissipation

**Dissipationsfaktor:**
```
E_{t+1} = E_t(1 + λ_A - λ_A²K²)

η ≈ 4.9×10³⁷  (Dämpfungsfaktor)
E_final/E₀ ≈ 10⁻³⁸  (extreme Dissipation!)
```

**Stabilitätsschwelle:**
```
Stabil: λ_A < 1/K²
Chaos:  λ_A > 1/K²  (Zeit bricht zusammen!)
```

### 14.6 QNM (Quasi-Normal Modes)

**SSZ-Frequenz:**
```
f_QNM(SSZ) ≈ φ · f_QNM(GR)

~5% Frequenzshift
Testbar mit LIGO/Virgo/KAGRA
```

---

## 15. Krümmungsinvarianten

### 15.1 Kretschmann-Skalar (Weak Field)

```
K = R_μνρσ R^μνρσ ≈ 48G²M²/(c⁴r⁶) + O(r_g³/r⁷)
```

**GR-Wert:**
```
K_GR = 48G²M²/(c⁴r⁶)  (exakt für Schwarzschild)
```

**SSZ stimmt im Weak-Field überein**

### 15.2 Weyl-Skalar

**Schwarzschild ist konform flach außerhalb:**
```
C_μνρσ = R_μνρσ + (Ricci-Terme)
```

### 15.3 Regularität

**SSZ-Eigenschaft:**
```
Alle Krümmungsinvarianten bleiben endlich für r > 0

K(r=0) = endlich  (keine Singularität!)
R(r=0) = endlich
R_μν R^μν (r=0) = endlich
```

---

## 16. φ-Spiral Geometrie

### 16.1 Logarithmische Spirale

**Polarform:**
```
r(θ) = a · exp(b·θ)
```

**Mit φ:**
```
b = ln(φ)/π
a = Normierungskonstante
```

### 16.2 Segment-Anzahl

**Anzahl Segmente bei Radius r:**
```
N(r) = N₀ + k|ln(r/a)|

mit k = 4/(bπ) = 4ln(φ)/π²
```

**Startbedingung:**
```
N₀ = 4  (bei θ = 0)
```

### 16.3 Bingsi-Konstante

**Definition:**
```
k = ln(φ)/π ≈ 0.1569

N(r) = 4 + (4/π) · ln(φ) · |ln(r/a)|
```

**Physikalische Bedeutung:**
- Beschreibt Segment-Dichte als Funktion von r
- Verbindet φ-Geometrie mit Raumzeit-Struktur
- Universal für alle Massen

### 16.4 Pitch-Winkel

**Spiralen-Pitch:**
```
tan(ψ) = r/(dr/dθ) = 1/b = π/ln(φ)
```

**Wert:**
```
ψ ≈ 72.97°  (konstant für alle r!)
```

---

## 17. Euler-Verbindung

### 17.1 Euler als kontinuierliche Hülle

**Diskrete Skalierung:**
```
S_φ: x ↦ φx  (Skalierungs-Generator)
```

**N-fache Iteration:**
```
S_φ^N(x) = φ^N · x
```

**Kontinuierliche Grenze:**
```
exp(ΔU) = lim_{n→∞} (1 + ΔU/n)^n

mit ln(R) ≈ ΔU/c²
```

### 17.2 φ-Gitter vs Euler-Exponential

**φ-Gitter (diskret):**
```
R = φ^N,  N ∈ ℤ
```

**Euler (kontinuierlich):**
```
R ≃ exp(ΔU/c²) ≈ φ^N  falls N ≈ ln(R)/ln(φ)
```

**Interpretation:**
- Euler liefert glatte Grenze
- φ-Potenzen liefern messbares Gitter
- Quantisierte Verfeinerung von GR

### 17.3 Euler-Formel und Segmentierung

**Komplexe Exponentialfunktion:**
```
e^(iθ) = cos(θ) + i·sin(θ)
```

**Diskrete Segmente auf Einheitskreis:**
```
e^(i·2πk/n),  k = 0, 1, ..., n-1
```

**Grenzwert:**
```
lim_{n→∞} (diskrete Segmente) = kontinuierlicher Kreis
```

---

## 18. Observable und Vorhersagen

### 18.1 Neutronenstern-Differenzen

**Bei r = 5r_s:**
```
Δ = (D_SSZ - D_GR)/D_GR × 100%
Δ ≈ -44%  (SSZ vorhersagt langsameren Zeitfluss!)
```

**Observabel:**
- Pulsar-Perioden erscheinen LÄNGER
- Röntgen-Timing zeigt SSZ-Signatur
- Erhöhter gravitativer Redshift

**NICER-Test JETZT möglich!**

### 18.2 Pulsar Timing

**Periode-Ratio:**
```
P_obs(SSZ)/P_GR ≈ 0.86

14% länger erscheinende Perioden!
```

**Messbar mit:**
- Pulsar Timing Arrays (NANOGrav, EPTA, PPTA)
- Individual Millisecond Pulsars

### 18.3 Spektrale Gitter

**Post-Doppler/Plasma-korrigierte Linien:**
```
1 + z ≈ φ^N,  N ∈ ℤ

Residual: ε = ln(1+z)/ln(φ) - round(ln(1+z)/ln(φ))
```

**Erwartung:** |ε| clustert bei 0

### 18.4 Shapiro Delay

**SSZ vs GR:**
```
Δt_SSZ > Δt_GR

Faktor ~34× für Neutronensterne
Zusätzlich ~15,000s für Sgr A*
```

### 18.5 G79.29+0.46 Temporal Redshift

**Beobachtung:**
```
z_temporal ≈ 0.12  (intrinsischer temporaler Shift)
z_obs ≈ 1.7×10⁻⁵  (beobachteter Residual)
Δv ≈ 5 km/s
```

**Interpretation:**
- 86% temporal (Metrik-Physik)
- 14% klassisch (Doppler)

**Hot Ring:**
```
Position: r ~ 0.5 pc
Temperatur: 200-300 K (Peak)
Status: ✅ Bereits in Spitzer/Herschel beobachtet!
```

---

## 19. Numerische Methoden

### 19.1 Newton-Raphson Iteration

**Standard-Form:**
```
x_{n+1} = x_n - f(x_n)/f'(x_n)
```

**Für Mass Inversion:**
```
M_{n+1} = M_n - f(M_n)/f'(M_n)

mit f(M) = r_φ(M) - r_obs
```

**Konvergenz-Kriterien:**
```
|f(M)| < tol_abs = 10⁻¹²⁰
|ΔM/M| < tol_rel = 10⁻¹²⁰
```

**Step Control:**
```
if |step| > |M|:
    step *= 0.5
```

### 19.2 Finite Differenzen

**Erste Ableitung (zentral):**
```
f'(x) ≈ (f(x+h) - f(x-h))/(2h)
```

**Zweite Ableitung:**
```
f''(x) ≈ (f(x+h) - 2f(x) + f(x-h))/h²
```

**Adaptive Schrittweite:**
```
h = max(10⁻⁶·r, 10⁻³)
```

### 19.3 Quintic Hermite Interpolation

**Für C²-Kontinuität:**
```
p(x) = Σ_{i=0}^5 a_i x^i
```

**Bedingungen:**
```
p(x₀) = f₀,     p'(x₀) = f'₀,     p''(x₀) = f''₀
p(x₁) = f₁,     p'(x₁) = f'₁,     p''(x₁) = f''₁
```

**Curvature Proxy:**
```
K ≈ |p''(x)| ≈ 10⁻¹⁵ - 10⁻¹⁶  (extrem glatt!)
```

### 19.4 Bootstrap Confidence Intervals

**Algorithmus:**
```
for i = 1 to n_boot (= 2000):
    Resample data with replacement
    Compute statistic θ_i

CI = [percentile(2.5%), percentile(97.5%)]
```

**Verwendet für:**
- Median-Schätzungen
- Robust statistics
- Unsicherheitsquantifizierung

### 19.5 ODE-Integration (Geodäten)

**RK4 (Runge-Kutta 4th Order):**
```
k₁ = h·f(t_n, y_n)
k₂ = h·f(t_n + h/2, y_n + k₁/2)
k₃ = h·f(t_n + h/2, y_n + k₂/2)
k₄ = h·f(t_n + h, y_n + k₃)

y_{n+1} = y_n + (k₁ + 2k₂ + 2k₃ + k₄)/6
```

**Adaptive Step Size:**
```
h_new = h_old · (tol/error)^(1/5)
```

---

## 20. Kosmologische Anwendungen

### 20.1 Multi-Body Sigma

**Gravitationspotential:**
```
Φ(x) = Σ_i GM_i/|x - x_i|
```

**Segment-Dichte (Multi-Body):**
```
Ξ(x) = Ξ_max(1 - exp(-Σ_i φ·r_{s,i}/|x - x_i|))
```

### 20.2 CMB-Anwendungen

**Planck-Daten:**
```
C_ℓ^TT = SSZ-modifizierte Powerspektrum

Erwartung: Geringfügige Abweichungen bei ℓ > 1000
```

### 20.3 Galaxien-Rotation

**Rotationskurve mit SSZ:**
```
v²(r) = GM(r)/r · (1 + f_SSZ(r))

f_SSZ(r) = SSZ-Korrekturfaktor
```

### 20.4 Kosmologisches Framework

**SSZ-FLRW Metrik (in Entwicklung):**
```
ds² = -c²dt² + a²(t)[dr²/(1-kr²) + r²dΩ²] · (SSZ-Faktoren)
```

---

## Zusammenfassung: Die Mathematik im Überblick

### Fundamentale Gleichungen (Top 10)

1. **φ-Definition:**
   ```
   φ = (1+√5)/2 ≈ 1.618
   ```

2. **SSZ Metrik:**
   ```
   ds² = -(c²/γ²)dT² + γ²dr² + r²dΩ²
   ```

3. **Segment-Dichte:**
   ```
   Ξ(r) = Ξ_max(1 - exp(-φr_s / r))
   ```

4. **Zeit-Dilatation:**
   ```
   D_SSZ(r) = 1/(1 + Ξ(r))
   ```

5. **Duale Geschwindigkeiten:**
   ```
   v_esc · v_fall = c²
   ```

6. **Einstein-Tensor:**
   ```
   G^T_T = (1/r²)[2rβφ'/γ² - 1/γ² + 1]
   ```

7. **Universeller Crossover:**
   ```
   r* = 1.386562 r_s
   ```

8. **Mass-Projection:**
   ```
   r_φ = (φ/2)r_s(1 + Δ/100)
   ```

9. **PPN-Parameter:**
   ```
   β = γ = 1.000... (GR-Limit)
   ```

10. **φ-Gitter:**
    ```
    R = f_emit/f_obs = φ^N, N ∈ ℤ
    ```

### Mathematische Hierarchie

```
φ-Geometrie (Fundamental)
    ↓
Segment-Dichte Ξ(r)
    ↓
Metrische Funktionen γ(r), β(r)
    ↓
Metrik g_μν
    ↓
Christoffel-Symbole Γ^ρ_μν
    ↓
Riemann-Tensor R^ρ_σμν
    ↓
Ricci-Tensor R_μν, Ricci-Skalar R
    ↓
Einstein-Tensor G_μν
    ↓
Stress-Energy T_μν (effektiv)
    ↓
Physikalische Observable
```

### Verbindung zu bekannten Theorien

**Weak-Field (r >> r_s):**
```
SSZ → GR (exakt via PPN)
```

**Strong-Field (r ~ r_s):**
```
SSZ ≠ GR (44% Differenz bei NS)
```

**Quantum-Scale (r ~ l_P):**
```
SSZ: natürlicher Cutoff via Segmentierung
```

---

**Vollständigkeit:** Diese Dokumentation enthält ALLE wesentlichen mathematischen Formeln und Konzepte der Segmented Spacetime Theorie, wie sie in den Repositories e:\clone\Segmented-Spacetime-Mass-Projection-Unified-Results, e:\clone\ssz-metric-pure, e:\clone\SEGMENTED-SPACETIME und verwandten Projekten entwickelt wurden.

**Status:** Publikationsreif für wissenschaftliche Journale

**Lizenz:** ANTI-CAPITALIST SOFTWARE LICENSE v1.4

© 2025 Carmen Wrede & Lino Casu
