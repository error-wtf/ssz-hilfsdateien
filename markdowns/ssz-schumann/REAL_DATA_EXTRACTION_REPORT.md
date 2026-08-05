# SSZ Schumann Experiment - Real Data Extraction Report

**Datum:** 2025-12-08  
**Status:** Proof-of-Concept erfolgreich  
**Autoren:** Carmen Wrede & Lino Casu

---

## Executive Summary

Erstmalige erfolgreiche Extraktion von **echten Schumann-Resonanz-Frequenzen** aus den Zenodo Sierra Nevada ELF-Rohdaten. 100 Stunden Daten aus Oktober 2013 wurden verarbeitet und die fundamentalen Schumann-Moden (f1-f4) extrahiert.

---

## 1. Datenquelle

### Zenodo Dataset
- **DOI:** 10.5281/zenodo.6348930
- **Paper:** Salinas et al. (2022) - "Schumann resonance data processing programs"
- **Standort:** Sierra Nevada, Spanien
- **Zeitraum:** März 2013 - Februar 2017 (4 Jahre)
- **Dateigröße:** 26.5 GB (komprimiert)

### Rohdaten-Format
| Parameter | Wert |
|-----------|------|
| Sampling Rate | 256 Hz (3906 µs) |
| Datentyp | int16 (ADC-Werte) |
| Dateilänge | 921600 Samples = 1 Stunde |
| Sensoren | 2 (NS und EW Magnetfeld) |
| Dateien gesamt | 33.086 |

---

## 2. Verarbeitungsmethode

### Pipeline
```
RAW ELF Data (int16)
    ↓
Welch PSD (nperseg=8192, noverlap=4096)
    ↓
Peak Detection in Schumann-Bändern
    ↓
Lorentzian Fitting (f0, gamma, amplitude)
    ↓
CSV Output (timestamp, f1, f2, f3, f4)
```

### Frequenzbänder für Peak-Detection
| Mode | Suchbereich | Erwarteter Wert |
|------|-------------|-----------------|
| f1 | 6.5 - 9.0 Hz | ~7.83 Hz |
| f2 | 13.0 - 16.0 Hz | ~14.1 Hz |
| f3 | 19.0 - 22.0 Hz | ~20.3 Hz |
| f4 | 25.0 - 28.0 Hz | ~26.4 Hz |

---

## 3. Ergebnisse

### Verarbeitete Daten
- **Monat:** Oktober 2013 (YYMM: 1310)
- **Dateien verfügbar:** 744
- **Dateien verarbeitet:** 100 (Proof-of-Concept)
- **Fehler:** 0

### Extrahierte Schumann-Frequenzen

| Mode | Mittelwert | Std.Abw. | Literatur | Differenz |
|------|------------|----------|-----------|-----------|
| **f1** | 8.04 Hz | ±0.13 Hz | 7.83 Hz | +0.21 Hz |
| **f2** | 14.70 Hz | ±0.30 Hz | 14.1 Hz | +0.60 Hz |
| **f3** | 21.00 Hz | ±0.21 Hz | 20.3 Hz | +0.70 Hz |
| **f4** | 27.52 Hz | ±0.22 Hz | 26.4 Hz | +1.12 Hz |

### Beobachtungen
1. **Systematischer Offset:** Alle Moden liegen ~3-4% über Literaturwerten
2. **Diurnale Variation:** Deutlich sichtbar in allen Moden
3. **Korrelation zwischen Moden:** f1-f4 zeigen ähnliche Variationsmuster
4. **Variationsbereich:** f1 ±0.5 Hz, f2 ±1.0 Hz, f3 ±0.5 Hz, f4 ±0.8 Hz

---

## 4. Spektralanalyse

### Rohspektrum (1 Stunde Daten)

![Spektrum](output/real_schumann_spectrum.png)

**Beobachtungen:**
- Schumann-Peaks bei ~8, 14, 21, 27 Hz sichtbar
- Starke Störung bei ~30 Hz (lokales Rauschen oder Instrument)
- 50 Hz Netzbrummen-Harmonische erkennbar
- 1/f-Rauschen im Niederfrequenzbereich

### Zeitreihen (100 Stunden)

![Zeitreihen](output/real_schumann_timeseries.png)

**Beobachtungen:**
- Klare diurnale Modulation (Tag/Nacht-Zyklus)
- f2 zeigt größte relative Variation
- Alle Moden korreliert (globaler Effekt)

---

## 5. Diskussion

### Offset zu Literaturwerten

Der systematische Offset von +3-4% könnte verursacht sein durch:

1. **Peak-Detection-Methode:** Lorentzian-Fit findet Maximum, nicht Zentroid
2. **Lokale Bedingungen:** Sierra Nevada hat spezifische ionosphärische Eigenschaften
3. **Zeitraum:** Oktober 2013 war nahe Sonnenmaximum (Zyklus 24)
4. **Instrumenteneffekte:** Frequenzgang des ELF-Sensors

### SSZ-Relevanz

Für die SSZ-Analyse ist der **relative Shift** wichtiger als der absolute Wert:

```
delta_seg(t) = -[f_obs(t) - f_mean] / f_mean
```

Die beobachtete Variation von ±1-2% ist konsistent mit:
- Ionosphärischer Modulation durch Sonneneinstrahlung
- Möglicher SSZ-Segmentierungseffekt (zu testen)

---

## 6. Generierte Dateien

### Daten
| Datei | Beschreibung | Größe |
|-------|--------------|-------|
| `data/schumann/real/processed/schumann_1310_processed.csv` | Extrahierte Frequenzen | ~15 KB |
| `data/schumann/real/raw/2013_2017.zip` | Rohdaten (Zenodo) | 26.5 GB |

### Plots
| Datei | Beschreibung |
|-------|--------------|
| `output/real_schumann_spectrum.png` | PSD-Spektrum mit Schumann-Moden |
| `output/real_schumann_timeseries.png` | Zeitreihen f1-f4 |

### Scripts
| Datei | Beschreibung |
|-------|--------------|
| `scripts/process_one_month.py` | Hauptverarbeitungs-Script |

---

## 7. Nächste Schritte

### Kurzfristig
- [ ] Alle 744 Dateien von Oktober 2013 verarbeiten
- [ ] F10.7 Solar Flux Daten für gleichen Zeitraum laden
- [ ] Kp-Index Daten für gleichen Zeitraum laden
- [ ] Korrelationsanalyse f1 vs. F10.7

### Mittelfristig
- [ ] Mehrere Monate verarbeiten (2013-2017)
- [ ] Saisonale Variation analysieren
- [ ] SSZ-Modell anwenden und testen

### Langfristig
- [ ] Vollständige 4-Jahres-Analyse
- [ ] Vergleich mit anderen Stationen (falls verfügbar)
- [ ] Publikationsvorbereitung

---

## 8. Technische Details

### Systemanforderungen
- Python 3.10+
- numpy, scipy, pandas, matplotlib
- ~30 GB Festplattenspeicher für Rohdaten
- ~2 GB RAM für Verarbeitung

### Verarbeitungszeit
- 100 Dateien: ~30 Sekunden
- 744 Dateien (1 Monat): ~4 Minuten (geschätzt)
- 33.086 Dateien (4 Jahre): ~3 Stunden (geschätzt)

### Reproduzierbarkeit
```bash
cd e:\clone\ssz-schuhman-experiment
python scripts/process_one_month.py
```

---

## 9. Referenzen

1. Salinas, A., et al. (2022). "Schumann resonance data processing programs and four-year measurements from Sierra Nevada ELF station." *Computers & Geosciences*, 165, 105148.

2. Nickolaenko, A. P., & Hayakawa, M. (2002). *Resonances in the Earth-Ionosphere Cavity*. Kluwer Academic Publishers.

3. Zenodo Dataset: https://zenodo.org/records/6348930

---

## 10. Fazit

**Proof-of-Concept erfolgreich!**

Die Extraktion echter Schumann-Resonanz-Frequenzen aus den Zenodo-Rohdaten funktioniert. Die extrahierten Werte sind physikalisch plausibel und zeigen die erwartete diurnale Variation. Die Daten sind bereit für die SSZ-Korrelationsanalyse.

---

*© 2025 Carmen Wrede & Lino Casu*  
*Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4*
