# SSZ Schumann Real Data Analysis Report

**Datum:** 2025-12-08  
**Version:** 1.0  
**Status:** Analyse abgeschlossen mit echten Daten  
**Autoren:** Carmen Wrede & Lino Casu

---

## Executive Summary

Diese Analyse testet das **SSZ-Minimalmodell** gegen echte Schumann-Resonanz-Daten. Alle Zahlen stammen aus tatsaechlichen Programmlaeufen - keine synthetischen oder halluzinierten Werte.

### Datenquellen

| Datentyp | Quelle | Status |
|----------|--------|--------|
| **Schumann-Resonanzen** | Zenodo Sierra Nevada ELF Station (doi:10.5281/zenodo.7761644) | ECHT |
| **F10.7 Solarflux** | Rekonstruiert aus NOAA Monatsmittelwerten | REKONSTRUIERT |
| **Kp Index** | Rekonstruiert aus GFZ Monatsmittelwerten | REKONSTRUIERT |

### Hauptergebnis

| Metrik | Wert (eta=0.74 fix) | Wert (eta gefittet) |
|--------|---------------------|---------------------|
| **Datenpunkte** | 744 Stunden | 744 Stunden |
| **Zeitraum** | 01.10.2013 - 31.10.2013 | 01.10.2013 - 31.10.2013 |
| **eta** | 0.7400 (fix) | 0.8101 +/- 0.0012 |
| **delta_SSZ_global** | -9.47% +/- 0.23% | -0.00% +/- 0.21% |
| **chi^2/ndof** | 55.36 | 55.36 |
| **p-value** | < 10^-4 | < 10^-4 |
| **Mode-Spread** | 3.17% | 2.90% |
| **Ergebnis** | **SSZ MINIMALMODELL ABGELEHNT** | **SSZ MINIMALMODELL ABGELEHNT** |

---

## 1. Daten und Methode

### 1.1 Schumann-Rohdaten

**Quelle:** Sierra Nevada ELF Station, Spanien  
**Format:** int16 binary, 256 Hz Abtastrate  
**Verarbeitung:** FFT + Lorentzian-Fit fuer Modenextraktion

```
Datei: data/schumann/real/processed/schumann_1310_processed.csv
Records: 744
Zeitraum: 2013-10-01 00:03:47 bis 2013-10-31 23:00:46
```

### 1.2 Beobachtete Frequenzen (Mittelwerte)

| Mode | f_beobachtet (Hz) | Standardabweichung (Hz) | n |
|------|-------------------|-------------------------|---|
| f1 | 8.055 | 0.136 | 744 |
| f2 | 14.754 | 0.312 | 744 |
| f3 | 21.036 | 0.213 | 744 |
| f4 | 27.554 | 0.219 | 744 |

### 1.3 Klassisches Modell

Die klassische Schumann-Frequenz fuer Mode n ist:

```
f_n = eta * c / (2*pi*R) * sqrt(n*(n+1))
```

mit:
- c = 299792458 m/s (Lichtgeschwindigkeit)
- R = 6.371e6 m (Erdradius)
- eta = Ionosphaerenkorrekturfaktor

**Literaturwert:** eta ~ 0.74 (Sentman 1995, Nickolaenko & Hayakawa 2002)

### 1.4 SSZ-Minimalmodell (getestete Hypothese)

**Hypothese:** Alle Frequenzabweichungen koennen durch einen einzigen, mode-unabhaengigen Faktor D_SSZ erklaert werden:

```
f_n_obs = f_n_classical / D_SSZ
D_SSZ = 1 + delta_SSZ
```

**Vorhersage:** delta_SSZ ist fuer alle Moden gleich.

---

## 2. Ergebnisse

### 2.1 Mit fixem eta = 0.74

**Klassische Referenzfrequenzen:**

| Mode | f_klassisch (Hz) |
|------|------------------|
| f1 | 7.838 |
| f2 | 13.575 |
| f3 | 19.198 |
| f4 | 24.784 |

**Per-Mode delta_seg_classical:**

| Mode | delta (%) | Fehler (%) |
|------|-----------|------------|
| f1 | -2.78 | 0.58 |
| f2 | -8.69 | 0.88 |
| f3 | -9.57 | 0.56 |
| f4 | -11.18 | 0.29 |

**SSZ-Hypothesentest:**

```
delta_SSZ_global = -9.467% +/- 0.228%
chi^2 = 166.07
ndof = 3
chi^2/ndof = 55.36
p-value < 10^-4
```

### 2.2 Mit gefittetem eta = 0.8101

**Klassische Referenzfrequenzen:**

| Mode | f_klassisch (Hz) |
|------|------------------|
| f1 | 8.580 |
| f2 | 14.860 |
| f3 | 21.015 |
| f4 | 27.131 |

**Per-Mode delta_seg_classical:**

| Mode | delta (%) | Fehler (%) |
|------|-----------|------------|
| f1 | +6.11 | 0.53 |
| f2 | +0.71 | 0.81 |
| f3 | -0.10 | 0.51 |
| f4 | -1.56 | 0.27 |

**SSZ-Hypothesentest:**

```
delta_SSZ_global = -0.000% +/- 0.209%
chi^2 = 166.07
ndof = 3
chi^2/ndof = 55.36
p-value < 10^-4
```

### 2.3 Mode-Korrelationen

```
Mean inter-mode correlation: 0.625
```

SSZ wuerde eine Korrelation nahe 1.0 vorhersagen (alle Moden verschieben sich gemeinsam).
Der beobachtete Wert von 0.625 zeigt signifikante mode-spezifische Effekte.

### 2.4 Raumwetter-Korrelationen

| Korrelation | r | p-value | Signifikant? |
|-------------|---|---------|--------------|
| delta_SSZ vs F10.7 | -0.103 | 0.580 | Nein |
| delta_SSZ vs Kp | +0.026 | 0.891 | Nein |

**Hinweis:** F10.7 und Kp sind rekonstruierte Proxies, keine echten Tagesdaten.

---

## 3. Interpretation

### 3.1 Was wurde falsifiziert?

**FALSIFIZIERT:** Das SSZ-Minimalmodell

> "Ein Szenario, in dem die Schumann-Frequenzen primaer durch einen globalen, mode-unabhaengigen SSZ-Faktor verschoben werden, ist mit den Daten unvereinbar."

**Evidenz:**
- chi^2/ndof = 55.36 >> 1 (erwartet: ~1 bei Konsistenz)
- p-value < 10^-4 (Hypothese mit >99.99% Konfidenz abgelehnt)
- Mode-Spread = 3.17% (SSZ erwartet: < 1%)

### 3.2 Was wurde NICHT falsifiziert?

**NICHT FALSIFIZIERT:** SSZ als kleine Korrektur

> "Ein zusaetzlicher SSZ-Beitrag von < O(1%) koennte weiterhin existieren, liegt aber unterhalb der dominanten Mode-abhaengigen Effekte und ist in diesem Setup nicht auflösbar."

**Praktische Obergrenze:**

```
|delta_SSZ| < 0.5% (bei eta=0.74)
|delta_SSZ| < 0.4% (bei eta gefittet)
```

### 3.3 Warum sind die Moden unterschiedlich?

Die beobachtete Mode-Abhaengigkeit (f1: -2.8%, f4: -11.2%) ist typisch fuer **klassische ionosphaerische Dispersion**:

1. **Wellenleiter-Dispersion:** Hoehere Moden "sehen" die Ionosphaere staerker
2. **Frequenzabhaengige Leitfaehigkeit:** Hoehere Frequenzen koppeln anders an D/E/F-Schichten
3. **Ionosphaerenhoehe:** Hoehere Moden sind empfindlicher auf Hoehenaenderungen

Das SSZ-Minimalmodell ("ein globaler Stretch-Faktor") kann diese Mode-Abhaengigkeit per Definition nicht erklaeren.

---

## 4. Limitationen

### 4.1 Daten

| Limitation | Auswirkung |
|------------|------------|
| Ein Monat (Oktober 2013) | Keine saisonalen Effekte sichtbar |
| Eine Station (Sierra Nevada) | Keine geografische Konsistenzpruefung |
| Rekonstruierte Proxies | Korrelationsanalyse eingeschraenkt |

### 4.2 Methodik

| Limitation | Auswirkung |
|------------|------------|
| Festes eta vs. gefittetes eta | Beide Varianten zeigen gleiches chi^2 |
| Keine explizite Dispersionsmodellierung | Klassische Effekte nicht separiert |
| Schumann als SSZ-Test ungeeignet | Ionosphaerenphysik ueberlagert SSZ |

---

## 5. Reproduzierbarkeit

### 5.1 Dateien

```
scripts/run_ssz_schumann_realdata.py  # Hauptanalyse
ssz_analysis/core.py                   # Kernfunktionen
data/schumann/real/processed/          # Verarbeitete Daten
output/ssz_schumann_realdata_results.json  # Ergebnisse
```

### 5.2 Ausfuehrung

```bash
# Mit fixem eta
python scripts/run_ssz_schumann_realdata.py --station sierra_nevada --year 2013 --month 10

# Mit gefittetem eta
python scripts/run_ssz_schumann_realdata.py --station sierra_nevada --year 2013 --month 10 --fit-eta
```

### 5.3 Abhaengigkeiten

```
numpy
pandas
scipy
```

---

## 6. Fazit

### 6.1 Wissenschaftliche Schlussfolgerung

| Aussage | Status |
|---------|--------|
| SSZ-Minimalmodell (ein globaler Faktor fuer alle Moden) | **ABGELEHNT** |
| Klassische ionosphaerische Dispersion | **DOMINIERT** |
| SSZ als kleine Korrektur (< 0.5%) | **OFFEN** (nicht auflösbar) |

### 6.2 Einordnung

> "Wir haben's ehrlich getestet. Die Erde schreit: 'Ionosphaere first, SSZ wenn ueberhaupt als leises Fluestern im Hintergrund.'"

Das ist genau das, was echte Physik macht:
1. Hypothese formulieren (SSZ als globaler Faktor)
2. Klare Vorhersage: alle Moden sollten im gleichen Verhaeltnis verschoben sein
3. Test mit echten Daten -> Hypothese verworfen
4. Konsequenz: SSZ muss subtiler und/oder an anderen Observablen getestet werden

### 6.3 Naechste Schritte

Fuer einen definitiven SSZ-Test sollten Observablen gewaehlt werden, wo die klassische Physik **simpler** ist:

| Observable | Klassischer Hintergrund | SSZ-Sensitivitaet |
|------------|------------------------|-------------------|
| Gravitationswellen (GW170817) | Minimal | ~10^-15 (bereits gemessen!) |
| Atomuhren-Netzwerke | Gut verstanden | ~10^-18 |
| Kavitaetsresonatoren | Kontrollierbar | ~10^-15 |
| GPS-Timing | Komplex aber modellierbar | ~10^-9 |
| Schumann-Resonanzen | **Sehr komplex** | ~10^-2 (diese Analyse) |

**Wichtig:** GW170817 hat bereits gezeigt: |c_gw - c|/c < 10^-15. Das ist ein viel staerkeres Limit als Schumann-Resonanzen je liefern koennten!

---

## 7. Technische Details

### 7.1 Formeln

**delta_seg_classical:**
```
delta_seg = -(f_obs - f_classical) / f_classical
```

**Gewichteter Mittelwert:**
```
delta_SSZ_global = sum(w_n * delta_n) / sum(w_n)
w_n = 1 / sigma_n^2
```

**Chi-squared Test:**
```
chi^2 = sum_n [(delta_n - delta_SSZ_global) / sigma_n]^2
ndof = n_modes - 1 = 3
```

### 7.2 Validierung

Die Rohdaten wurden gegen Literaturwerte validiert:

| Mode | Erwartet (Hz) | Beobachtet (Hz) | Status |
|------|---------------|-----------------|--------|
| f1 | 7.5 - 8.5 | 8.055 | OK |
| f2 | 13.5 - 15.0 | 14.754 | OK |
| f3 | 19.5 - 21.5 | 21.036 | OK |
| f4 | 25.5 - 28.0 | 27.554 | OK |

---

*Copyright 2025 Carmen Wrede & Lino Casu*  
*Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4*

---

## Appendix: JSON-Ergebnisse

Die vollstaendigen Ergebnisse sind in `output/ssz_schumann_realdata_results.json` gespeichert.
