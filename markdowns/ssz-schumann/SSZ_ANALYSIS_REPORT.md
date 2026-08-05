# SSZ Schumann Resonance Analysis Report

**Datum:** 2025-12-08  
**Status:** Analyse abgeschlossen  
**Autoren:** Carmen Wrede & Lino Casu

---

## Executive Summary

Vollständige Analyse von **744 Stunden** echter Schumann-Resonanz-Daten aus Oktober 2013 (Sierra Nevada ELF Station). Die Daten wurden mit dem SSZ-Modell (Segmented Spacetime) analysiert und auf Korrelationen mit Sonnenaktivität (F10.7) und geomagnetischer Aktivität (Kp) getestet.

### Hauptergebnisse

| Metrik | Wert |
|--------|------|
| **Datenpunkte** | 744 Stunden |
| **Zeitraum** | 01.10.2013 - 31.10.2013 |
| **f1 beobachtet** | 8.055 ± 0.046 Hz |
| **f1 klassisch** | 7.838 Hz |
| **delta_seg (Mittel)** | -8.05% |
| **SSZ-Konsistenz** | Nein (modenabhängig) |

---

## 1. Datenübersicht

### Verarbeitete Daten
- **Quelle:** Zenodo Sierra Nevada ELF Station
- **Dateien:** 744 (1 Stunde pro Datei)
- **Zeitraum:** Oktober 2013 (kompletter Monat)
- **Sampling:** 256 Hz, int16 ADC

### Extrahierte Frequenzen

| Mode | Beobachtet | Klassisch (η=0.74) | Abweichung |
|------|------------|-------------------|------------|
| f1 | 8.055 Hz | 7.838 Hz | +2.78% |
| f2 | 14.754 Hz | 13.575 Hz | +8.69% |
| f3 | 21.036 Hz | 19.198 Hz | +9.57% |
| f4 | 27.554 Hz | 24.784 Hz | +11.18% |

---

## 2. SSZ-Analyse

### Segment Density Deviation (delta_seg)

Die SSZ-Theorie postuliert:
```
f_observed = f_classical / D_SSZ
D_SSZ = 1 + delta_seg
delta_seg = -(f_obs - f_classical) / f_classical
```

### Ergebnisse

| Mode | delta_seg (Mittel) | delta_seg (Std) |
|------|-------------------|-----------------|
| f1 | -2.78% | ±0.57% |
| f2 | -8.69% | ±2.30% |
| f3 | -9.57% | ±1.11% |
| f4 | -11.18% | ±0.88% |

**Interpretation:**
- Negative delta_seg bedeutet: beobachtete Frequenz **höher** als klassisch
- Dies entspricht einer **schnelleren** effektiven Lichtgeschwindigkeit
- Oder: die klassische Formel mit η=0.74 unterschätzt die Frequenzen

### SSZ-Konsistenztest

**SSZ-Vorhersage:** Alle Moden sollten den **gleichen relativen Shift** zeigen.

**Ergebnis:**
- Spread zwischen Moden: 0.0366 (3.66%)
- Schwellwert für SSZ-Konsistenz: < 0.02 (2%)
- **Fazit: Mode-abhängiger Shift → klassischer Effekt dominiert**

---

## 3. Korrelationsanalyse

### Korrelationen mit Sonnenaktivität

| Korrelation | r-Wert | p-Wert | Signifikant? |
|-------------|--------|--------|--------------|
| f1 vs F10.7 | -0.241 | 0.191 | Nein |
| f2 vs F10.7 | -0.028 | 0.880 | Nein |
| delta_seg vs F10.7 | 0.068 | 0.714 | Nein |
| delta_seg vs Kp | 0.102 | 0.587 | Nein |

**Interpretation:**
- Keine signifikante Korrelation zwischen Schumann-Frequenzen und F10.7/Kp
- Dies könnte an den synthetischen F10.7/Kp-Daten liegen (echte tägliche Daten benötigt)
- Oder: der Effekt ist zu klein für einen Monat Daten

### SSZ-Modell-Fit

```
delta_seg(t) = beta0 + beta1 * F10.7_norm(t)
```

| Parameter | Wert | Fehler |
|-----------|------|--------|
| beta0 | -0.0805 | ±0.0009 |
| beta1 | 0.0003 | ±0.0009 |
| RMSE | 0.0049 | - |

**Interpretation:**
- beta1 ≈ 0 → keine signifikante solare Modulation in diesem Datensatz
- beta0 ≈ -8% → konstanter Offset zur klassischen Theorie

---

## 4. Diurnale Variation

### Beobachtete Tagesgänge

| Mode | Minimum (UTC) | Maximum (UTC) | Amplitude |
|------|---------------|---------------|-----------|
| f1 | ~12:00 | ~06:00 | 0.34 Hz |
| f2 | ~15:00 | ~12:00 | 0.65 Hz |
| f3 | ~08:00 | ~13:00 | 0.45 Hz |
| f4 | ~04:00 | ~14:00 | 0.55 Hz |

**Interpretation:**
- Klare diurnale Modulation in allen Moden
- Maximum typischerweise am Nachmittag (UTC)
- Konsistent mit globaler Blitzaktivität (Afrika/Amerika)

---

## 5. Plots

### Zeitreihen
![Zeitreihen](output/ssz_analysis_timeseries.png)

### Korrelationen
![Korrelationen](output/ssz_analysis_correlations.png)

### Diurnale Variation
![Diurnal](output/ssz_analysis_diurnal.png)

---

## 6. Diskussion

### Warum ist delta_seg modenabhängig?

Die beobachtete Modenabhängigkeit (f1: -2.8%, f4: -11.2%) deutet auf **klassische ionosphärische Effekte** hin:

1. **Ionosphärenhöhe:** Höhere Moden sind empfindlicher auf Höhenänderungen
2. **Leitfähigkeitsprofil:** Frequenzabhängige Dämpfung
3. **Wellenleiter-Dispersion:** Nicht-idealer Hohlleiter

### SSZ-Effekt nicht nachweisbar?

Das bedeutet **nicht**, dass SSZ falsch ist:

1. **Zu kurzer Zeitraum:** 1 Monat ist möglicherweise nicht genug
2. **Synthetische Hilfsdaten:** Echte F10.7/Kp-Daten könnten Korrelationen zeigen
3. **Klassische Effekte dominieren:** SSZ-Effekt könnte unter ~0.1% liegen
4. **Falscher Ansatz:** SSZ wirkt möglicherweise nicht auf Schumann-Frequenzen

### Nächste Schritte

1. **Echte F10.7-Daten** von NOAA/LASP für 2013-2017 beschaffen
2. **Längerer Zeitraum** analysieren (4 Jahre statt 1 Monat)
3. **Solare Events** identifizieren (Flares, CMEs) und gezielt analysieren
4. **Andere Stationen** vergleichen (falls verfügbar)

---

## 7. Generierte Dateien

### Daten
| Datei | Beschreibung |
|-------|--------------|
| `data/schumann/real/processed/schumann_1310_processed.csv` | 744 Stunden Frequenzdaten |
| `output/ssz_analysis_daily.csv` | Tägliche Mittelwerte |
| `output/ssz_analysis_hourly.csv` | Stündliche Mittelwerte |
| `output/ssz_analysis_summary.json` | Zusammenfassung als JSON |

### Plots
| Datei | Beschreibung |
|-------|--------------|
| `output/ssz_analysis_timeseries.png` | Zeitreihen mit F10.7/Kp |
| `output/ssz_analysis_correlations.png` | Korrelationsplots |
| `output/ssz_analysis_diurnal.png` | Tagesgang aller Moden |

### Scripts
| Datei | Beschreibung |
|-------|--------------|
| `scripts/process_one_month.py` | Rohdaten-Verarbeitung |
| `scripts/run_ssz_analysis.py` | SSZ-Analyse |

---

## 8. Fazit

### Erreicht
- ✅ 744 Stunden echte Schumann-Daten extrahiert
- ✅ Frequenzen f1-f4 mit Lorentzian-Fitting bestimmt
- ✅ SSZ-Modell angewendet und getestet
- ✅ Diurnale Variation quantifiziert
- ✅ Korrelationsanalyse durchgeführt

### Ergebnis
- **SSZ-Effekt nicht nachweisbar** in diesem Datensatz
- **Klassische ionosphärische Effekte** dominieren
- **Modenabhängiger Shift** widerspricht SSZ-Vorhersage

### Empfehlung
Für einen definitiven SSZ-Test werden benötigt:
1. Längerer Zeitraum (Jahre statt Monate)
2. Echte tägliche Sonnen-/Geomagnetik-Daten
3. Mehrere unabhängige Stationen
4. Fokus auf extreme Sonnenereignisse

---

*© 2025 Carmen Wrede & Lino Casu*  
*Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4*
