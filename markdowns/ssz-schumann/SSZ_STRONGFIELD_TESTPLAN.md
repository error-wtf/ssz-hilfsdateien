# SSZ Strong-Field Test Plan

**Datum:** 2025-12-09  
**Status:** Planungsphase  
**Autoren:** Carmen Wrede & Lino Casu

---

## Executive Summary

Die Schumann-Analyse hat gezeigt: Bei GM/(Rc²) ~ 7×10⁻¹⁰ (Erdoberfläche) ist SSZ nicht vom klassischen Hintergrund trennbar. Für einen aussagekräftigen SSZ-Test brauchen wir **stärkere Gravitationsfelder**.

### Gravitationspotential-Skala

| Objekt | GM/(Rc²) | SSZ-Sensitivität | Datentyp |
|--------|----------|------------------|----------|
| Erdoberfläche | 7×10⁻¹⁰ | ❌ Zu schwach | Schumann (getestet) |
| Sonne (Oberfläche) | 2×10⁻⁶ | ⚠️ Grenzwertig | Helioseismologie |
| Weißer Zwerg | ~10⁻⁴ | ✅ Möglich | Spektrallinien |
| **Neutronenstern** | **~0.2** | **✅ Ideal** | Pulsar-Timing, X-Ray |
| **BH (ISCO)** | **~0.5** | **✅ Ideal** | Fe-Kα, QPOs, GW |
| LBV-Nebel (G79) | variabel | ✅ Bereits getestet | ALMA, VLT |

---

## 1. Priorität A: Neutronenstern-Daten (NICER)

### 1.1 Warum NICER?

- **Instrument:** Neutron Star Interior Composition Explorer (ISS)
- **Ziel:** Präzise Masse-Radius-Bestimmung von Neutronensternen
- **GM/(Rc²):** ~0.1-0.3 (genau im SSZ-Regime!)
- **Messungen:** Pulse profiles, Zeitdilatation, Shapiro-Delay

### 1.2 Konkrete Datensätze

| Pulsar | Typ | M/M☉ | R (km) | GM/(Rc²) | Daten |
|--------|-----|------|--------|----------|-------|
| **PSR J0030+0451** | MSP | 1.44 | 13.0 | 0.16 | NICER + XMM |
| **PSR J0740+6620** | MSP | 2.08 | 12.4 | 0.25 | NICER + XMM |
| **PSR J1614-2230** | MSP | 1.97 | ~13 | 0.22 | Timing |

### 1.3 SSZ-Test-Ansatz

**Klassisches Modell:**
```
Gravitationsrotverschiebung: z_grav = (1 - 2GM/Rc²)^(-1/2) - 1
Zeitdilatation: τ_obs / τ_emit = (1 - 2GM/Rc²)^(1/2)
```

**SSZ-Modell:**
```
z_SSZ = z_grav × D_SSZ
D_SSZ = 1 + δ_seg(r)
```

**Observable:** Abweichung der gemessenen Rotverschiebung von GR-Vorhersage

### 1.4 Datenquelle

```
HEASARC: https://heasarc.gsfc.nasa.gov/
NICER Archive: https://heasarc.gsfc.nasa.gov/docs/nicer/nicer_archive.html
Spezifisch: PSR J0030+0451 ObsIDs
```

---

## 2. Priorität A: Gravitationswellen (LIGO/Virgo)

### 2.1 Warum GW?

- **Bereits genutzt:** GW170817 hat |c_gw - c|/c < 10⁻¹⁵ gezeigt
- **Starkes Feld:** Merger-Phase bei GM/(Rc²) ~ 0.5
- **Saubere Physik:** Keine komplexe Ionosphäre/Atmosphäre

### 2.2 Konkrete Events

| Event | Typ | M_total/M☉ | z | SNR | SSZ-Relevanz |
|-------|-----|------------|---|-----|--------------|
| **GW150914** | BBH | 65 | 0.09 | 24 | Ringdown-Frequenz |
| **GW170817** | BNS | 2.7 | 0.01 | 33 | c_gw vs c_em |
| **GW190521** | BBH | 150 | 0.82 | 14 | Höchste Masse |

### 2.3 SSZ-Test-Ansatz

**Klassisches Modell (GR):**
```
Ringdown: f_QNM = c³/(2πGM) × F(a/M)
Inspiral: f_GW = (1/π) × (GM_chirp/c³)^(-5/8) × (5/256 × 1/t)^(3/8)
```

**SSZ-Modell:**
```
f_QNM_SSZ = f_QNM_GR × D_SSZ(r_horizon)
```

**Observable:** Konsistenz zwischen Inspiral- und Ringdown-Parametern

### 2.4 Datenquelle

```
GWOSC: https://gwosc.org/
Strain data: https://gwosc.org/eventapi/html/GWTC/
Parameter estimates: https://zenodo.org/communities/ligo-virgo-kagra/
```

---

## 3. Priorität B: Fe-Kα Linien (XMM-Newton/NuSTAR)

### 3.1 Warum Fe-Kα?

- **Emission:** 6.4 keV (neutral) bis 6.97 keV (H-like)
- **Ort:** Innere Akkretionsscheibe, r ~ 3-10 r_g
- **GM/(Rc²):** ~0.1-0.3 am ISCO
- **Effekte:** Gravitationsrotverschiebung + Doppler + Beaming

### 3.2 Konkrete Quellen

| Quelle | Typ | M_BH/M☉ | Spin a/M | Daten |
|--------|-----|---------|----------|-------|
| **Cyg X-1** | HMXB | 21 | >0.95 | XMM, NuSTAR |
| **GRS 1915+105** | LMXB | 12 | >0.98 | XMM, Chandra |
| **MCG-6-30-15** | Seyfert 1 | 3×10⁶ | ~0.99 | XMM (lang!) |

### 3.3 SSZ-Test-Ansatz

**Klassisches Modell (relxill):**
```
Linienprofil = ∫ ε(r) × g⁴ × δ(E - g×E_rest) × dA
g = Rotverschiebungsfaktor (Kerr-Metrik)
```

**SSZ-Modell:**
```
g_SSZ = g_Kerr × (1 + δ_seg(r))
```

**Observable:** Residuen im Linienprofil nach relxill-Fit

### 3.4 Datenquelle

```
XMM-Newton: https://www.cosmos.esa.int/web/xmm-newton/xsa
NuSTAR: https://heasarc.gsfc.nasa.gov/docs/nustar/nustar_archive.html
Chandra: https://cxc.harvard.edu/cda/
```

---

## 4. Priorität B: ALMA Nebel-Daten (bereits vorhanden!)

### 4.1 Verbindung zu G79.29+0.46

Wir haben bereits SSZ-Analysen für LBV-Nebel durchgeführt:
- **Repository:** `g79-cygnus-test`
- **Ergebnis:** SSZ-Segmentierung reproduziert Ringstruktur

### 4.2 Weitere ALMA-Targets

| Objekt | Typ | Distanz | ALMA-Band | Status |
|--------|-----|---------|-----------|--------|
| G79.29+0.46 | LBV-Nebel | 1.7 kpc | 6, 7 | ✅ Analysiert |
| AG Car | LBV | 6 kpc | 6 | Verfügbar |
| η Car | LBV | 2.3 kpc | 3, 6, 7 | Verfügbar |
| Crab Nebula | SNR/Pulsar | 2 kpc | 3, 6 | Verfügbar |

### 4.3 Datenquelle

```
ALMA Archive: https://almascience.eso.org/aq/
Project codes: 2019.1.xxxxx etc.
```

---

## 5. Implementierungsplan

### Phase 1: NICER Pulsar-Analyse (2 Wochen)

```python
# Pseudocode für NICER-Pipeline
def ssz_pulsar_test(obs_id: str):
    # 1. Daten laden
    events = load_nicer_events(obs_id)
    
    # 2. Pulse profile extrahieren
    profile = fold_events(events, ephemeris)
    
    # 3. GR-Modell fitten (PINT/Tempo2)
    gr_params = fit_gr_model(profile)
    
    # 4. SSZ-Korrektur berechnen
    delta_ssz = compute_ssz_correction(gr_params['M'], gr_params['R'])
    
    # 5. Residuen analysieren
    residuals = profile - gr_model(gr_params)
    chi2_gr = compute_chi2(residuals)
    
    # 6. SSZ-Modell fitten
    ssz_params = fit_ssz_model(profile, delta_ssz)
    chi2_ssz = compute_chi2(profile - ssz_model(ssz_params))
    
    return {
        'delta_chi2': chi2_gr - chi2_ssz,
        'ssz_amplitude': ssz_params['delta_seg'],
        'significance': compute_significance(delta_chi2, ndof=1)
    }
```

### Phase 2: GW Ringdown-Analyse (1 Woche)

```python
# Pseudocode für GW-Pipeline
def ssz_ringdown_test(event: str):
    # 1. Strain-Daten laden
    strain = load_gwosc_strain(event)
    
    # 2. Ringdown isolieren
    t_merger = get_merger_time(strain)
    ringdown = strain[t_merger:t_merger + 0.1]
    
    # 3. QNM-Frequenz messen
    f_qnm_obs, tau_obs = fit_damped_sinusoid(ringdown)
    
    # 4. GR-Vorhersage aus Inspiral
    M_final, a_final = get_final_params(event)
    f_qnm_gr = qnm_frequency(M_final, a_final)
    
    # 5. SSZ-Test
    delta_f = (f_qnm_obs - f_qnm_gr) / f_qnm_gr
    
    return {
        'f_qnm_obs': f_qnm_obs,
        'f_qnm_gr': f_qnm_gr,
        'delta_f_percent': delta_f * 100,
        'ssz_consistent': abs(delta_f) < 0.01  # 1% Schwelle
    }
```

### Phase 3: Fe-Kα Spektralanalyse (3 Wochen)

```python
# Pseudocode für X-Ray-Pipeline
def ssz_feka_test(obs_id: str, source: str):
    # 1. Spektrum extrahieren
    spectrum = extract_xmm_spectrum(obs_id)
    
    # 2. Kontinuum fitten (powerlaw + diskbb)
    continuum = fit_continuum(spectrum, 2.0, 10.0)  # keV
    
    # 3. Fe-Kα Region isolieren
    fe_region = spectrum[5.5:7.5]  # keV
    
    # 4. relxill-Fit (Standard GR)
    relxill_params = fit_relxill(fe_region, continuum)
    
    # 5. SSZ-modifiziertes Modell
    # g_SSZ = g_Kerr × (1 + delta_seg)
    ssz_params = fit_ssz_relxill(fe_region, continuum)
    
    # 6. Modellvergleich
    delta_chi2 = relxill_params['chi2'] - ssz_params['chi2']
    
    return {
        'relxill_chi2': relxill_params['chi2'],
        'ssz_chi2': ssz_params['chi2'],
        'delta_seg_best': ssz_params['delta_seg'],
        'improvement_sigma': np.sqrt(delta_chi2)
    }
```

---

## 6. Erwartete Ergebnisse

### Szenario A: SSZ nicht detektiert

| Test | Erwartung | Konsequenz |
|------|-----------|------------|
| NICER | δ_seg < 1% | SSZ < O(10⁻²) bei NS |
| GW | Δf/f < 1% | SSZ konsistent mit GR |
| Fe-Kα | Keine Verbesserung | relxill ausreichend |

**Interpretation:** SSZ ist entweder sehr klein oder hat andere funktionale Form als angenommen.

### Szenario B: SSZ-Hinweis

| Test | Erwartung | Konsequenz |
|------|-----------|------------|
| NICER | δ_seg ~ 1-5% | SSZ-Effekt bei NS! |
| GW | Δf/f ~ 1% | Ringdown-Anomalie |
| Fe-Kα | χ² verbessert | SSZ-Korrektur nötig |

**Interpretation:** SSZ hat messbare Effekte in starken Feldern → Paper!

---

## 7. Konkrete nächste Schritte

### Sofort (diese Woche):

1. **GWOSC-Daten für GW150914 herunterladen**
   ```bash
   pip install gwosc
   python -c "from gwosc.datasets import event_gps; print(event_gps('GW150914'))"
   ```

2. **NICER-Daten für PSR J0030+0451 anfragen**
   - HEASARC Browse: https://heasarc.gsfc.nasa.gov/cgi-bin/W3Browse/w3browse.pl
   - Mission: NICER
   - Target: PSR J0030+0451

3. **XMM-Spektrum für Cyg X-1 herunterladen**
   - XSA: https://www.cosmos.esa.int/web/xmm-newton/xsa
   - Target: Cyg X-1
   - Instrument: EPIC-pn

### Mittelfristig (2-4 Wochen):

4. **SSZ-Pulsar-Modul implementieren**
   - Basierend auf PINT (Pulsar Timing)
   - SSZ-Korrektur als zusätzlicher Parameter

5. **SSZ-GW-Modul implementieren**
   - Basierend auf PyCBC oder Bilby
   - Ringdown-Analyse mit SSZ-Modifikation

6. **SSZ-XRay-Modul implementieren**
   - Basierend auf XSPEC + relxill
   - SSZ als multiplikativer Faktor auf g

---

## 8. Ressourcen

### Software

| Tool | Zweck | URL |
|------|-------|-----|
| PINT | Pulsar Timing | https://github.com/nanograv/PINT |
| PyCBC | GW-Analyse | https://pycbc.org/ |
| Bilby | Bayesian GW | https://lscsoft.docs.ligo.org/bilby/ |
| XSPEC | X-Ray Spektren | https://heasarc.gsfc.nasa.gov/xanadu/xspec/ |
| relxill | Reflexionsmodelle | http://www.sternwarte.uni-erlangen.de/~dauser/research/relxill/ |

### Literatur

| Thema | Paper | arXiv |
|-------|-------|-------|
| NICER M-R | Miller+2019 | 1912.05705 |
| GW170817 c_gw | Abbott+2017 | 1710.05834 |
| Fe-Kα relxill | Dauser+2014 | 1312.5510 |
| SSZ Theorie | Casu & Wrede | (in prep) |

---

## 9. Fazit

Die Schumann-Analyse war ein wichtiger **Null-Test**: Sie zeigt, dass SSZ bei GM/(Rc²) ~ 10⁻¹⁰ nicht detektierbar ist. Das ist konsistent mit der Theorie!

Für einen **positiven Test** brauchen wir:
- **Neutronensterne** (GM/(Rc²) ~ 0.2)
- **Schwarze Löcher** (GM/(Rc²) ~ 0.5)
- **Gravitationswellen** (dynamisches starkes Feld)

Die Daten existieren und sind öffentlich zugänglich. Die Pipeline-Struktur ist analog zur Schumann-Analyse:

```
1. Daten laden (NICER/GWOSC/XMM)
2. Klassisches Modell fitten (GR)
3. SSZ-Korrektur berechnen
4. Residuen analysieren
5. Chi²-Test: GR vs SSZ
6. Obergrenze oder Detektion berichten
```

---

*Copyright 2025 Carmen Wrede & Lino Casu*  
*Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4*
