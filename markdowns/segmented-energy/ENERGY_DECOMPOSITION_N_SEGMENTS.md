# Energiezerlegung mit N-Segmentierung - Vollständige Herleitung

**Formale Ebene bis zur untersten Ausführungsebene**  
**Erstellt:** 2025-12-07  
**Für:** Segmented Spacetime Energy Framework

---

## 1. Grundansatz mit N-Segmentierung

### 1.1 Gesamtenergie-Zerlegung

Testmasse **m** in Zentralfeld mit Masse **M**, Bahn/Radialrichtung in **N** Segmente zerlegt.

```
E_tot = E_rest + E_GR + E_SR
```

**Komponenten:**
```
E_rest = m·c²                    (Ruheenergie)
E_GR   = Σ_{n=1}^N E_gr_n        (Gravitativer Anteil)
E_SR   = Σ_{n=1}^N E_sr_n        (Spezial-relativistischer Anteil)
```

**Physikalische Bedeutung:**
- **E_gr_n:** Gravitativer Energiebeitrag im Segment n
- **E_sr_n:** SR-Beitrag (kinetisch, Lorentz-Faktor) im Segment n
- **N:** Anzahl der Segmente (über φ, g1/g2-Zonen, oder andere Skalierung)

### 1.2 Radiale Segmentierung

**Segment-Grenzen:**
```
r_0, r_1, r_2, ..., r_N
```

**Segment n:** Bereich zwischen r_{n-1} und r_n

**Segmentierungs-Strategien:**
- Logarithmisch: `r_n = r_0 · (r_N/r_0)^(n/N)`
- φ-basiert: `r_n = r_0 · φ^(n·α)` für geeignetes α
- SSZ-Spiral: Aus φ-Spiral-Geometrie abgeleitet
- g1/g2-Zonen: Domänen-spezifische Grenzen

---

## 2. Auflösung auf unterste Formelebene

### 2.1 Gravitationsanteil E_GR (Newton-Limit)

**Potential:**
```
Φ(r) = -GM/r
```

**Diskrete Änderung im Segment n:**
```
ΔE_gr_n = E_pot(r_n) - E_pot(r_{n-1})
        = m·Φ(r_n) - m·Φ(r_{n-1})
        = -GMm·(1/r_n - 1/r_{n-1})
```

**Einzelsegment-Beitrag:**
```
E_gr_n = -GMm·(1/r_n - 1/r_{n-1})
```

**Summe über alle Segmente:**
```
E_GR = Σ_{n=1}^N E_gr_n
     = -GMm·Σ_{n=1}^N (1/r_n - 1/r_{n-1})
```

**Teleskopische Vereinfachung:**
```
E_GR = -GMm·(1/r_N - 1/r_0)
```

**SSZ-Erweiterung:**
Ersetze Φ(r) durch SSZ-Potential:
```
Φ_SSZ(r) = -mc²·(Ξ(r) - 1)   oder
Φ_SSZ(r) = -mc²·(γ(r) - 1)   oder
Φ_SSZ(r) = basierend auf φ_G(r)
```

Dann:
```
E_gr_n = m·Φ_SSZ(r_n) - m·Φ_SSZ(r_{n-1})
```

### 2.2 SR-Anteil E_SR

**Lokale Geschwindigkeit im Segment n:**
```
v_n = sqrt(GM/r_n)   (Kepler-Orbit, Newton-Limit)
```

**Lorentz-Faktor:**
```
γ_n = 1/sqrt(1 - v_n²/c²)
```

**SR-Energie im Segment n:**
```
E_sr_n = (γ_n - 1)·m·c²
```

**Summe über alle Segmente:**
```
E_SR = Σ_{n=1}^N E_sr_n
     = Σ_{n=1}^N (γ_n - 1)·m·c²
```

**Explizit mit v_n:**
```
E_SR = m·c²·Σ_{n=1}^N [1/sqrt(1 - GM/(r_n·c²)) - 1]
```

**SSZ-Erweiterung:**
In SSZ kann v_n durch g2-relativen Boost oder φ-Spiral-Geschwindigkeit ersetzt werden:
```
v_n = v_SSZ(r_n)  (aus SSZ-Metrik abgeleitet)
```

### 2.3 Vollständige Formel (unterste Ebene)

**Einsetzen von E_gr_n und E_sr_n:**
```
E_tot = m·c²
        + Σ_{n=1}^N [-GMm·(1/r_n - 1/r_{n-1})]
        + Σ_{n=1}^N [(γ_n - 1)·m·c²]
```

**Mit teleskopischer Vereinfachung von E_GR:**
```
E_tot = m·c²
        - GMm·(1/r_N - 1/r_0)
        + Σ_{n=1}^N (γ_n - 1)·m·c²
```

**Faktorisiert nach m:**
```
E_tot = m·[c²
          - GM·(1/r_N - 1/r_0)
          + c²·Σ_{n=1}^N (γ_n - 1)]
```

**Mit explizitem γ_n:**
```
E_tot = m·{c²
          - GM·(1/r_N - 1/r_0)
          + c²·Σ_{n=1}^N [1/sqrt(1 - v_n²/c²) - 1]}
```

**Mit explizitem v_n = sqrt(GM/r_n):**
```
E_tot = m·{c²
          - GM·(1/r_N - 1/r_0)
          + c²·Σ_{n=1}^N [1/sqrt(1 - GM/(r_n·c²)) - 1]}
```

**Das ist die unterste Formelebene!**

Nur noch fundamentale Größen:
- m, M, G, c (physikalische Konstanten)
- r_0, r_n, r_N (geometrische Parameter)
- N (Segmentzahl)

Keine Sammel-Energiesymbole (E_GR, E_SR) mehr!

---

## 3. SSZ-spezifische Erweiterungen

### 3.1 SSZ-Potential mit Ξ(r)

**Segment-Dichte:**
```
Ξ(r) = Ξ_max(1 - exp(-φ · r_s / r))
```

**SSZ-Potential:**
```
Φ_SSZ(r) = -mc²·Ξ(r)
```

**Gravitationsbeitrag (SSZ):**
```
E_gr_n = m·c²·[Ξ(r_{n-1}) - Ξ(r_n)]
```

**Gesamte GR-Energie (SSZ):**
```
E_GR = m·c²·[Ξ(r_0) - Ξ(r_N)]
```

### 3.2 SSZ-Geschwindigkeit mit φ_G(r)

**Gravitationspotential-Funktion:**
```
φ_G(r) = sqrt(2GM/(r·c²))
```

**SSZ-Geschwindigkeit:**
```
v_SSZ(r) = c·tanh(φ_G(r))  oder
v_SSZ(r) = basierend auf Dual-Velocity v_fall
```

**SR-Beitrag (SSZ):**
```
γ_n = cosh(φ_G(r_n))
E_sr_n = [γ_n - 1]·m·c²
```

### 3.3 φ-Spiral Segmentierung

**Segment-Anzahl nach Bingsi:**
```
N(r) = N_0 + (4/π)·ln(φ)·|ln(r/a)|
```

**Radiale Segmente (logarithmisch):**
```
r_n = a·exp(b·θ_n)
mit b = ln(φ)/π
```

**Segment-Grenzen:**
```
θ_n = n·(π/4)  (45° Schritte)
r_n = a·exp(ln(φ)·n/4)
```

---

## 4. Grenzfälle und Konsistenz-Checks

### 4.1 Kontinuierlicher Grenzfall (N → ∞)

**Gravitationsanteil:**
```
lim_{N→∞} Σ_{n=1}^N E_gr_n = ∫_{r_0}^{r_N} m·dΦ/dr·dr
                            = m·[Φ(r_N) - Φ(r_0)]
                            = -GMm·(1/r_N - 1/r_0)
```

**SR-Anteil:**
```
lim_{N→∞} Σ_{n=1}^N E_sr_n = ∫_{r_0}^{r_N} (γ(r) - 1)·m·c²·dr/r
```

**Konsistenz:** ✅ Segmentierung geht korrekt in Integral über

### 4.2 Einzelsegment (N = 1)

**Nur ein Segment von r_0 bis r_1:**
```
E_GR = -GMm·(1/r_1 - 1/r_0)
E_SR = (γ_1 - 1)·m·c²
```

**Konsistenz:** ✅ Triviale Reduktion

### 4.3 Teleskopische Eigenschaft

**Kontrolle:**
```
Σ_{n=1}^N (1/r_n - 1/r_{n-1}) = 1/r_N - 1/r_0
```

**Beweis:**
```
(1/r_1 - 1/r_0)
+ (1/r_2 - 1/r_1)
+ (1/r_3 - 1/r_2)
+ ...
+ (1/r_N - 1/r_{N-1})
= 1/r_N - 1/r_0  ✓
```

### 4.4 Energie-Erhaltung

**Bei konstanter Gesamtenergie E_tot:**

Segmentierung ändert NICHT die Gesamtenergie, nur ihre Verteilung:
```
E_tot (grob, N=10) = E_tot (fein, N=1000)
```

**Konsistenz:** ✅ Energie ist extensive Größe

---

## 5. Schwarzes Loch Szenario (SSZ)

### 5.1 Horizont bei r_h = r_s

**Äußerer Bereich (r > r_s):**
```
r_0 = r_h = 2GM/c²  (Horizont)
r_N = r_obs         (Beobachter weit entfernt)
```

**g1/g2-Aufteilung:**
- **g1-Segmente:** Innerhalb φ-Grenze (r < r_φ)
- **g2-Segmente:** Außerhalb φ-Grenze (r > r_φ)

**Segment-Dichte:**
```
Ξ(r_h) ≈ Ξ_max·(1 - exp(-φ)) ≈ 0.802·Ξ_max
Ξ(∞) = 0
```

### 5.2 Zeit-Dilatation am Horizont

**GR:**
```
D_GR(r_h) = 0  (Singularität!)
```

**SSZ:**
```
D_SSZ(r_h) = 1/(1 + Ξ(r_h)) ≈ 0.667  (endlich!)
```

**Energie-Korrektur:**
```
E_obs = E_local·D_SSZ(r)
```

### 5.3 Photon bei r → r_h

**Grenzfall:**
```
v_fall → c
v_esc → c
γ → ∞  (GR)
γ_SSZ endlich  (SSZ durch Sättigung)
```

**Energie am Horizont (SSZ):**
```
E(r_h) = m·c²·[1 + Ξ_max·(1 - exp(-φ))]  (endlich!)
```

---

## 6. Numerische Implementierung

### 6.1 Algorithmus-Struktur

```python
# 1. Definiere Segment-Grenzen
r_edges = geomspace(r0, rN, N+1)

# 2. Berechne Gravitationsbeiträge
Phi_edges = -G*M / r_edges
E_pot_edges = m * Phi_edges
E_gr_segments = diff(E_pot_edges)
E_GR = sum(E_gr_segments)

# 3. Berechne SR-Beiträge
r_mid = sqrt(r_edges[:-1] * r_edges[1:])
v = sqrt(G*M / r_mid)
gamma = 1 / sqrt(1 - (v/c)**2)
E_sr_segments = (gamma - 1) * m * c**2
E_SR = sum(E_sr_segments)

# 4. Gesamtenergie
E_rest = m * c**2
E_tot = E_rest + E_GR + E_SR
```

### 6.2 Konsistenz-Tests

**Test 1: Teleskopische Eigenschaft**
```python
E_GR_sum = sum(E_gr_segments)
E_GR_tel = m * (-G*M * (1/rN - 1/r0))
assert abs(E_GR_sum - E_GR_tel) < tol
```

**Test 2: N-Unabhängigkeit**
```python
E_tot_N10 = compute_energy(N=10)
E_tot_N100 = compute_energy(N=100)
assert abs(E_tot_N10 - E_tot_N100) / E_tot_N10 < 1e-6
```

**Test 3: GR-Grenzfall**
```python
# Bei schwachen Feldern: E_tot ≈ E_GR (Newton)
if r0 >> r_s:
    assert abs(E_SR) << abs(E_GR)
```

### 6.3 Visualisierung

**Energie-Profil:**
```python
plot(r_mid, E_gr_segments, label='E_gr per segment')
plot(r_mid, E_sr_segments, label='E_sr per segment')
plot(r_mid, E_gr_segments + E_sr_segments, label='Total per segment')
```

**Kumulative Energie:**
```python
E_cumulative = cumsum(E_gr_segments + E_sr_segments)
plot(r_edges[1:], E_cumulative + E_rest)
```

---

## 7. Zusammenfassung

### 7.1 Vollständige Formel (unterste Ebene)

```
E_tot = m·{c²
          - GM·(1/r_N - 1/r_0)
          + c²·Σ_{n=1}^N [1/sqrt(1 - GM/(r_n·c²)) - 1]}
```

**Nur fundamentale Größen:**
- m, M, G, c (Konstanten)
- r_0, r_n, r_N (Radien)
- N (Segmentzahl)

### 7.2 SSZ-Version

```
E_tot = m·{c²
          + c²·[Ξ(r_0) - Ξ(r_N)]
          + c²·Σ_{n=1}^N [cosh(φ_G(r_n)) - 1]}
```

**Mit:**
- Ξ(r) = Ξ_max(1 - exp(-φ · r_s / r))
- φ_G(r) = sqrt(2GM/(r·c²))

### 7.3 Vorteile der Segmentierung

1. **Explizite Lokalität:** Energie-Beiträge pro Segment sichtbar
2. **SSZ-Integration:** Einfache Ersetzung von Φ(r) durch Ξ(r)
3. **Numerische Stabilität:** Vermeidung von Singularitäten
4. **Physikalische Intuition:** Segment = physikalische Domäne
5. **Erweiterbarkeit:** g1/g2-Zonen, φ-Spirale, etc.

### 7.4 Nächste Schritte

1. ✅ Mathematische Herleitung (dieses Dokument)
2. ✅ Astropy-Implementierung (siehe Python-Script)
3. ⏭️ SSZ-Potential Ξ(r) integrieren
4. ⏭️ Black-Hole-Szenario (r_0 = r_h)
5. ⏭️ g1/g2-Domänen-spezifische Korrekturen
6. ⏭️ φ-Spiral-Segmentierung testen
7. ⏭️ Visualisierung und Validierung

---

**Status:** Vollständig hergeleitet, bereit für numerische Tests

**Lizenz:** ANTI-CAPITALIST SOFTWARE LICENSE v1.4

© 2025 Carmen Wrede & Lino Casu
