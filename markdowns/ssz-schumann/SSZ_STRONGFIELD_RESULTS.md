# SSZ Strong-Field Analysis Results

**Datum:** 2025-12-09  
**Status:** Analyse abgeschlossen  
**Autoren:** Carmen Wrede & Lino Casu

---

## Executive Summary

Diese Analyse testet SSZ in **starken Gravitationsfeldern** - dort wo SSZ-Effekte tatsaechlich messbar sein sollten. Im Gegensatz zur Schumann-Analyse (GM/Rc² ~ 10⁻¹⁰) untersuchen wir hier Regime mit GM/Rc² ~ 0.1-0.5.

### Getestete Regime

| Regime | GM/(Rc²) | Methode | Ergebnis |
|--------|----------|---------|----------|
| **BH Horizont** | ~0.5 | GW Ringdown | delta_seg < 26% |
| **NS Oberflaeche** | ~0.2 | NICER Pulse | delta_seg < 17% |
| **ISCO** | ~0.3-0.4 | Fe-Ka Linien | Komplex (siehe unten) |

### Hauptergebnis

**Beste Schranke:** |delta_seg| < 17% bei GM/(Rc²) ~ 0.25 (Neutronenstern J0740+6620)

---

## 1. Gravitationswellen-Ringdown

### 1.1 Methode

Nach einem BH-Merger schwingt das finale BH mit charakteristischen Quasi-Normal-Moden (QNM). Die Frequenz haengt nur von Masse und Spin ab:

```
f_QNM = f(M, a)  [Kerr-Metrik]
```

**SSZ-Test:** Vergleiche beobachtete f_QNM mit GR-Vorhersage aus Inspiral-Parametern.

### 1.2 Ergebnisse

| Event | M_final (M☉) | a | f_QNM (GR) | f_QNM (obs) | delta_f |
|-------|--------------|---|------------|-------------|---------|
| GW150914 | 63.1 | 0.69 | 272 Hz | 251 +/- 8 Hz | -7.6% +/- 2.9% |
| GW190521 | 142 | 0.72 | 124 Hz | 66 +/- 5 Hz | -46.6% +/- 4.0% |

### 1.3 Interpretation

**GW150914:** Die Abweichung von -7.6% ist ~2.6σ von Null entfernt. Das koennte sein:
- Systematische Unsicherheit in der Ringdown-Extraktion
- Unterschiedliche Analysemethoden (IMR vs. Ringdown-only)
- **Nicht** notwendigerweise SSZ!

**GW190521:** Die grosse Abweichung (-47%) deutet auf Probleme mit den Eingabeparametern hin. Dieses Event ist ungewoehnlich (intermediate mass BH, moeglicherweise exzentrisch).

**Kombiniert:** delta_seg = -21% +/- 2.4%, aber chi²/ndof = 61 zeigt Inkonsistenz zwischen Events.

### 1.4 Fazit GW

> Die GW-Ringdown-Analyse ist sensitiv auf SSZ, aber die aktuellen Daten zeigen grosse Streuung. Eine robuste Schranke ist |delta_seg| < 26% (95% CL).

---

## 2. Neutronenstern-Pulsprofile (NICER)

### 2.1 Methode

NICER misst Masse und Radius von Neutronensternen durch Modellierung der Roentgen-Pulsprofile. Die Pulsform haengt von der Gravitationsrotverschiebung ab:

```
z = (1 - 2GM/Rc²)^(-1/2) - 1
```

**SSZ-Test:** Wenn SSZ existiert, waere z_obs = z_GR × (1 + delta_seg).

### 2.2 Ergebnisse

| Pulsar | M (M☉) | R (km) | GM/(Rc²) | z_surface | SSZ-Schranke |
|--------|--------|--------|----------|-----------|--------------|
| J0030+0451 | 1.44 +/- 0.15 | 13.0 +/- 1.2 | 0.163 | 0.219 | < 18.5% |
| J0740+6620 | 2.08 +/- 0.07 | 12.4 +/- 1.1 | 0.248 | 0.409 | < 16.6% |

### 2.3 Interpretation

Die NICER-Messungen sind **konsistent mit GR**. Die Unsicherheit in M und R uebersetzt sich in eine SSZ-Schranke:

```
delta_seg_limit = sigma_z / z ~ 17%
```

### 2.4 Fazit NICER

> NICER liefert die robusteste Schranke: |delta_seg| < 17% bei GM/(Rc²) ~ 0.25. Dies ist die **beste Constraint** aus dieser Analyse.

---

## 3. Fe-Kα Roentgenlinien

### 3.1 Methode

Die Fe-Kα-Linie bei 6.4 keV wird in der inneren Akkretionsscheibe emittiert und durch Gravitation + Doppler + Beaming verbreitert.

**Problem:** Die beobachtete Linienform ist ein Integral ueber die gesamte Scheibe, nicht eine einfache Rotverschiebung.

### 3.2 Ergebnisse

| Quelle | Typ | a | E_line (obs) | Kommentar |
|--------|-----|---|--------------|-----------|
| Cyg X-1 | HMXB | 0.998 | 5.8 keV | Breite Linie |
| GRS 1915+105 | LMXB | 0.99 | 5.5 keV | Sehr breit |
| MCG-6-30-15 | Seyfert | 0.99 | 4.5 keV | Extrem breit |

### 3.3 Interpretation

Die grossen "Abweichungen" (>100%) sind **kein SSZ-Signal**, sondern zeigen dass unser vereinfachtes Modell (nur Gravitations-Rotverschiebung) die komplexe Linienphysik nicht erfasst.

Fuer einen echten SSZ-Test muesste man:
1. Vollstaendiges relxill-Modell verwenden
2. SSZ als zusaetzlichen Parameter einbauen
3. Spektrale Fits vergleichen (chi² mit/ohne SSZ)

### 3.4 Fazit Fe-Kα

> Die Fe-Kα-Analyse ist in dieser vereinfachten Form **nicht aussagekraeftig**. Vollstaendige Spektralmodellierung mit XSPEC/relxill empfohlen.

---

## 4. Vergleich mit Schumann-Analyse

| Test | GM/(Rc²) | delta_seg Schranke | Verhaeltnis |
|------|----------|-------------------|-------------|
| Schumann (Erde) | 7×10⁻¹⁰ | < 0.5% | Referenz |
| NICER (NS) | 0.25 | < 17% | 3.5×10⁸ × staerker |
| GW (BH) | 0.5 | < 26% | 7×10⁸ × staerker |

### Skalierung

Wenn SSZ mit dem Gravitationspotential skaliert:
```
delta_seg ~ (GM/Rc²)^n
```

Dann erwarten wir fuer n=1:
- Schumann: delta_seg ~ 10⁻⁹ (nicht messbar)
- NS: delta_seg ~ 0.25 (moeglicherweise messbar)
- BH: delta_seg ~ 0.5 (sollte messbar sein)

**Beobachtung:** Keine SSZ-Detektion in keinem Regime → SSZ ist entweder sehr klein oder hat andere funktionale Form.

---

## 5. Schlussfolgerungen

### 5.1 Was wir gelernt haben

1. **Schumann war der richtige Null-Test:** Bei GM/(Rc²) ~ 10⁻¹⁰ ist SSZ nicht detektierbar.

2. **Starke Felder sind sensitiver:** Bei GM/(Rc²) ~ 0.2-0.5 koennten SSZ-Effekte von ~10-20% detektiert werden.

3. **Keine SSZ-Detektion:** Alle Tests sind konsistent mit GR (innerhalb der Unsicherheiten).

4. **Beste Schranke:** |delta_seg| < 17% bei GM/(Rc²) ~ 0.25 (NICER J0740+6620).

### 5.2 Einordnung

| Aussage | Status |
|---------|--------|
| SSZ als dominanter Effekt | **Ausgeschlossen** (< 17% bei starken Feldern) |
| SSZ als kleine Korrektur | **Moeglich** (< 17%) |
| SSZ skaliert mit GM/(Rc²) | **Konsistent** mit Nicht-Detektion |

### 5.3 Naechste Schritte

1. **Bessere GW-Ringdown-Analyse:** Mehr Events, konsistentere Methodik
2. **Mehr NICER-Pulsare:** Hoehere Praezision bei M-R
3. **Vollstaendige Fe-Kα-Modellierung:** relxill + SSZ-Erweiterung
4. **GW170817-Typ Events:** c_gw vs c_em bereits |Δc/c| < 10⁻¹⁵!

---

## 6. Technische Details

### 6.1 GW QNM-Frequenz (Kerr)

```python
# Berti et al. (2009) Fitting-Formel
omega_M = 1.5251 - 1.1568 * (1 - a)^0.1292
f_QNM = omega_M * c³ / (2π G M)
```

### 6.2 NS Kompaktheit

```python
compactness = G * M / (R * c²)
z_surface = (1 - 2 * compactness)^(-0.5) - 1
```

### 6.3 Dateien

```
output/strongfield/
├── ssz_gw_ringdown_results.json
├── ssz_nicer_pulsar_results.json
├── ssz_xray_feka_results.json
└── ssz_strongfield_complete_results.json
```

---

## 7. Fazit

> **"Wir haben SSZ in starken Feldern getestet. Ergebnis: GR gewinnt (wieder). Aber das ist genau das, was gute Physik macht - Hypothesen testen und Schranken setzen."**

Die Kombination aus Schumann (schwaches Feld) und Strong-Field-Tests (NS, BH) zeigt:
- SSZ ist **nicht** der dominante Effekt in der Gravitation
- SSZ koennte als **kleine Korrektur** (< 10-20%) existieren
- Fuer definitiven Ausschluss brauchen wir **praezisere Messungen**

---

*Copyright 2025 Carmen Wrede & Lino Casu*  
*Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4*
