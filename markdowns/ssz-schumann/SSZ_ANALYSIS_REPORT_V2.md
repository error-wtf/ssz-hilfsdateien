# SSZ Schumann Resonance Analysis Report v2

**Datum:** 2025-12-08  
**Version:** 2.1  
**Status:** Analyse abgeschlossen  
**Autoren:** Carmen Wrede & Lino Casu

---

## Executive Summary

Vollstaendige Analyse von **744 Stunden** echter Schumann-Resonanz-Daten aus Oktober 2013 (Sierra Nevada ELF Station). Die Analyse testet das **SSZ-Minimalmodell** - die Hypothese, dass Schumann-Frequenzabweichungen durch einen einzigen, mode-unabhaengigen Laufzeitfaktor D_SSZ erklaert werden koennen.

### Hauptergebnis

| Metrik | Wert |
|--------|------|
| **Datenpunkte** | 744 Stunden |
| **Zeitraum** | 01.10.2013 - 31.10.2013 |
| **Global delta_SSZ** | -9.47% +/- 0.23% |
| **Chi-squared/ndof** | 55.36 |
| **P-value** | < 0.0001 |
| **Ergebnis** | **SSZ-MINIMALMODELL ABGELEHNT** |

### Praezise Schlussfolgerung

Ein einfaches SSZ-Minimalmodell mit einem globalen, mode-unabhaengigen Laufzeitfaktor ist mit den Daten **unvereinbar** (chi²/ndof = 55).

Die beobachteten Mode-abhaengigen Offsets (f1: -2.8%, f4: -11.2%) sind konsistent mit **klassischer ionosphaerischer Dispersion**.

Ein zusaetzlicher, kleiner SSZ-Beitrag unterhalb der dominanten Mode-abhaengigen Dispersion (< 1%) bleibt mit dieser Analyse jedoch **prinzipiell vereinbar** - er ist lediglich nicht auflösbar.

---

## 1. Klassische Ergebnisse

### 1.1 Beobachtete vs. Klassische Frequenzen

Mit eta = 0.74 (Literaturwert fuer ionosphaerische Korrektur, siehe Sentman 1995, Nickolaenko & Hayakawa 2002):

**Hinweis zu eta:** Der Wert 0.74 ist ein etablierter Naeherungswert fuer die effektive Leitfaehigkeit der Ionosphaere. Ein Fit von eta an die Daten (--fit-eta) ergibt eta_fit ~ 0.80, was die Abweichungen reduziert aber nicht eliminiert. Die Mode-Abhaengigkeit bleibt bestehen.

| Mode | f_beobachtet | f_klassisch | Abweichung |
|------|--------------|-------------|------------|
| f1 | 8.055 Hz | 7.838 Hz | +2.78% |
| f2 | 14.754 Hz | 13.575 Hz | +8.69% |
| f3 | 21.036 Hz | 19.198 Hz | +9.57% |
| f4 | 27.554 Hz | 24.784 Hz | +11.18% |

### 1.2 Per-Mode Offsets (delta_seg_classical)

```
delta_seg_classical = -(f_obs - f_classical) / f_classical
```

| Mode | delta_seg_classical | Unsicherheit |
|------|---------------------|--------------|
| f1 | -2.78% | +/- 0.58% |
| f2 | -8.69% | +/- 0.88% |
| f3 | -9.57% | +/- 0.56% |
| f4 | -11.18% | +/- 0.29% |

**Interpretation:**
- Negative Werte bedeuten: f_obs > f_klassisch
- Die Abweichung ist **stark modenabhaengig** (f1: -2.8%, f4: -11.2%)
- Dies ist typisch fuer **klassische ionosphaerische Dispersion**

### 1.3 Diurnale Variation

| Mode | Tagesgang-Amplitude |
|------|---------------------|
| f1 | 0.34 Hz |
| f2 | 0.65 Hz |
| f3 | 0.46 Hz |
| f4 | 0.55 Hz |

Die diurnale Variation ist konsistent mit globaler Blitzaktivitaet und ionosphaerischer Tag/Nacht-Modulation.

---

## 2. SSZ-Hypothesentest

### 2.1 SSZ-Minimalmodell (getestete Hypothese)

Wir testen hier explizit ein **Extremfall-Szenario**:

**Hypothese:** Alle Abweichungen der Schumann-Frequenzen vom idealen Kugelhohlleiter-Modell koennen als ein einziger, mode-unabhaengiger Laufzeitfaktor D_SSZ beschrieben werden.

```
f_n_obs = f_n_classical / D_SSZ
D_SSZ = 1 + delta_SSZ
```

**Kritische Vorhersage:** delta_SSZ sollte fuer **alle Moden gleich** sein.

**Was wir NICHT testen:** Ein Modell der Form:
```
delta_n_total = delta_n_klassisch + delta_SSZ
```
wobei delta_n_klassisch die bekannte ionosphaerische Dispersion beschreibt. Ein solches erweitertes Modell wuerde einen kleinen, zusaetzlichen SSZ-Term erlauben.

### 2.2 Globales delta_SSZ

Gewichteter Mittelwert ueber alle Moden:

```
delta_SSZ_global = -9.467% +/- 0.228%
```

### 2.3 Chi-Squared Test

Wenn SSZ korrekt ist, sollten alle Per-Mode-Deltas mit delta_SSZ_global uebereinstimmen:

```
chi^2 = sum_n [(delta_n - delta_SSZ) / sigma_n]^2
```

| Statistik | Wert |
|-----------|------|
| chi^2 | 166.07 |
| ndof | 3 |
| chi^2/ndof | **55.36** |
| P-value | **< 0.0001** |

**Interpretation:**
- chi^2/ndof >> 1 bedeutet: Die Moden sind **nicht konsistent** mit einem gemeinsamen delta_SSZ
- P-value < 0.0001: SSZ-Hypothese wird mit >99.99% Konfidenz **abgelehnt**

### 2.4 Auflösungsgrenze fuer einen zusaetzlichen SSZ-Term

Die Mode-abhaengigen klassischen Offsets liegen im Bereich **3-11%**.
Die Messunsicherheiten pro Mode liegen bei **< 1%**.

Ein zusaetzlicher, wirklich mode-unabhaengiger SSZ-Term waere daher - grob gesprochen - nur im Bereich **< 1%** robust nachweisbar. In den vorliegenden Daten ist kein solcher konsistenter Term sichtbar.

**Praktische Obergrenze:** Falls SSZ existiert und mode-unabhaengig ist, dann |delta_SSZ| < ~1% (verborgen unter der klassischen Dispersion).

### 2.5 SSZ-Konsistenzmetriken (heuristische Arbeitsdefinitionen)

| Metrik | Wert | Schwellwert* | Erfuellt? |
|--------|------|--------------|-----------|
| Mode-Spread | 3.17% | < 2% | Nein |
| Inter-Mode-Korrelation | 0.625 | > 0.7 | Nein |
| SSZ-Score | 0.379 | > 0.5 | Nein |

*Diese Schwellwerte sind **heuristische Arbeitsdefinitionen** fuer dieses Experiment, nicht physikalisch abgeleitete Grenzwerte.

**Fazit:** Alle Metriken verfehlen die definierten Konsistenzschwellwerte.

---

## 3. Korrelationsanalyse

### 3.1 Korrelationen mit Raumwetter-Proxies

| Korrelation | r-Wert | P-Wert | Signifikant? |
|-------------|--------|--------|--------------|
| delta_SSZ_anomaly vs F10.7 | 0.072 | 0.700 | Nein |
| delta_SSZ_anomaly vs Kp | -0.007 | 0.972 | Nein |

**Hinweis:** Diese Korrelationen wurden mit **synthetischen** F10.7/Kp-Daten berechnet und sind daher **nicht fuer physikalische Interpretation geeignet**.

### 3.2 Inter-Mode-Korrelationen

Die Korrelation der delta_seg_anomaly zwischen verschiedenen Moden:

```
Mean inter-mode correlation = 0.625
```

Dies zeigt, dass die Moden teilweise korreliert variieren (globale Effekte), aber nicht perfekt (modenspezifische Effekte).

---

## 4. Diskussion

### 4.1 Warum ist delta_seg modenabhaengig?

Die beobachtete Modenabhaengigkeit (f1: -2.8%, f4: -11.2%) ist ein klares Zeichen fuer **klassische ionosphaerische Dispersion**:

1. **Wellenleiter-Dispersion:** Hoehere Moden "sehen" die Details der Ionosphaere/Erde staerker
2. **Frequenzabhaengige Leitfaehigkeit:** Hoehere Frequenzen koppeln anders an die D/E/F-Schichten
3. **Ionosphaerenhöhe:** Hoehere Moden sind empfindlicher auf Hoehenaenderungen

Das SSZ-Minimalmodell ("ein globaler Stretch-Faktor") produziert per Definition:
- Alle Verhaeltnisse der Moden bleiben gleich, nur die Skala verschiebt sich

Aber die Daten zeigen:
- Die Verhaeltnisse selbst sind verzogen (f2/f1, f3/f1 etc. weichen vom Kugelwert ab)

**Fazit:** Schumann-Resonanzen sind kein sauberer Test fuer ein einfaches, kugelsymmetrisches SSZ-Minimalmodell. Sie sind dominiert von klassischer, komplizierter Plasmaphysik.

### 4.2 Was genau wurde falsifiziert (und was nicht)?

#### FALSIFIZIERT: SSZ als dominanter, mode-unabhaengiger Effekt

> "Ein Szenario, in dem die Schumann-Frequenzen primaer durch einen globalen, mode-unabhaengigen SSZ-Faktor verschoben werden, ist mit den Daten unvereinbar. Klassische ionosphaerische Dispersion dominiert."

#### NICHT FALSIFIZIERT: SSZ als kleine Korrektur

> "Ein zusaetzlicher SSZ-Beitrag von < O(1%) koennte weiterhin existieren, liegt aber unterhalb der dominanten Mode-abhaengigen Effekte und ist in diesem Setup nicht auflösbar."

### 4.3 Limitationen dieser Analyse

1. **Rekonstruierte Proxy-Daten:** F10.7 und Kp wurden aus Monatsmittelwerten rekonstruiert (nicht tagesgenau gemessen)
2. **Ein Monat:** Laengere Zeitreihen koennten subtile Effekte aufdecken
3. **Eine Station:** Mehrere Stationen wuerden systematische Fehler reduzieren
4. **Feste eta:** Ein Fit von eta reduziert die Abweichungen, eliminiert aber nicht die Mode-Abhaengigkeit
5. **Schumann als SSZ-Test ungeeignet:** Die komplexe Ionosphaerenphysik ueberlagert jeden moeglichen SSZ-Effekt

### 4.4 Methodische Anmerkung

Diese Analyse setzt implizit:
```
delta_n_klassisch = 0
```
und prueft, ob alles durch delta_SSZ erklaert werden kann. Dass das nicht klappt, ist logisch - der klassische Anteil ist gross und modeabhaengig.

Ein erweitertes Modell mit expliziter klassischer Dispersion:
```
delta_n_total = delta_n_klassisch(n) + delta_SSZ
```
wuerde einen kleinen, zusaetzlichen SSZ-Term erlauben, ist aber mit den vorliegenden Daten nicht sinnvoll testbar.

---

## 5. Generierte Dateien

### Daten
| Datei | Beschreibung |
|-------|--------------|
| `output/ssz_analysis_daily.csv` | Taegliche Mittelwerte mit delta_seg |
| `output/ssz_analysis_hourly.csv` | Stuendliche Mittelwerte |
| `output/ssz_analysis_summary.json` | Vollstaendige Zusammenfassung |

### Plots
| Datei | Beschreibung |
|-------|--------------|
| `output/ssz_analysis_timeseries.png` | Zeitreihen mit klassischer Referenz |
| `output/ssz_analysis_correlations.png` | SSZ-Test und Korrelationen |
| `output/ssz_analysis_diurnal.png` | Tagesgang aller Moden |

---

## 6. Implementation Details

### 6.1 Code-Struktur

```
ssz-schuhman-experiment/
  ssz_analysis/
    __init__.py          # Modul-Exports
    core.py              # Kernfunktionen
  scripts/
    process_one_month.py # Rohdaten-Extraktion
    run_ssz_analysis_v2.py # Hauptanalyse (CLI)
```

### 6.2 Kernfunktionen

| Funktion | Beschreibung |
|----------|--------------|
| `load_schumann_data()` | Laedt CSV mit Schumann-Frequenzen |
| `get_classical_reference()` | Berechnet klassische Frequenzen |
| `fit_classical_eta()` | Fittet optimales eta |
| `compute_delta_seg_classical()` | Offset vs. klassisch |
| `compute_delta_seg_anomaly()` | Anomalie vs. Modenmittel |
| `estimate_delta_ssz_global()` | Gewichteter Mittelwert |
| `run_ssz_hypothesis_test()` | Vollstaendiger Chi^2-Test |

### 6.3 CLI-Verwendung

```bash
# Standard-Analyse (erwartet echte Proxy-Daten)
python scripts/run_ssz_analysis_v2.py

# Mit synthetischen Proxies (Demo)
python scripts/run_ssz_analysis_v2.py --use-synthetic-proxies

# Mit angepasstem eta
python scripts/run_ssz_analysis_v2.py --eta 0.76

# Mit eta-Fit
python scripts/run_ssz_analysis_v2.py --fit-eta
```

### 6.4 Reproduzierbarkeit

```bash
# 1. Rohdaten extrahieren (falls noch nicht geschehen)
python scripts/process_one_month.py

# 2. Analyse ausfuehren
python scripts/run_ssz_analysis_v2.py --use-synthetic-proxies

# Erwartete Ausgabe:
# - 744 Records
# - f1_mean ~ 8.055 Hz
# - delta_f1_classical ~ -2.78%
# - chi^2/ndof ~ 55
```

---

## 7. Fazit

### Was diese Analyse zeigt

1. **Mathematisch sauber:** Fehlerfortpflanzung, Chi-squared-Test und Hypothesentest sind konsequent durchgefuehrt
2. **Ehrliche Wissenschaft:** Das eigene Modell wird nicht schoengerechnet
3. **Klares Ergebnis:** Das SSZ-Minimalmodell ist mit den Daten unvereinbar

### Praezises Ergebnis

| Aussage | Status |
|---------|--------|
| SSZ-Minimalmodell (ein globaler Faktor fuer alle Moden) | **ABGELEHNT** |
| Klassische ionosphaerische Dispersion | **DOMINIERT** |
| SSZ als kleine Korrektur (< 1%) | **OFFEN** (nicht auflösbar) |

### Wissenschaftliche Einordnung

> "Wir haben's ehrlich getestet. Die Erde schreit: 'Ionosphaere first, SSZ wenn ueberhaupt als leises Fluestern im Hintergrund.'"

Das ist genau das, was echte Physik macht:
1. Hypothese formulieren (SSZ als globaler Faktor)
2. Klare Vorhersage: alle Moden sollten im gleichen Verhaeltnis verschoben sein
3. Test mit Daten -> Hypothese verworfen
4. Konsequenz: SSZ muss subtiler und/oder an anderen Observablen getestet werden

### Naechste sinnvolle Schritte

Fuer einen definitiven SSZ-Test sollten Observablen gewaehlt werden, wo die klassische Physik **simpler** ist:

| Observable | Klassischer Hintergrund | SSZ-Sensitivitaet |
|------------|------------------------|-------------------|
| Atomuhren-Netzwerke | Gut verstanden | ~10^-18 |
| Gravitationswellen (GW170817) | Minimal | ~10^-15 (bereits gemessen!) |
| Kavitaetsresonatoren | Kontrollierbar | ~10^-15 |
| GPS-Timing | Komplex aber modellierbar | ~10^-9 |
| Schumann-Resonanzen | **Sehr komplex** | ~10^-2 (diese Analyse) |

**Wichtig:** GW170817 hat bereits gezeigt: |c_gw - c|/c < 10^-15. Das ist ein viel staerkeres Limit als Schumann-Resonanzen je liefern koennten!

---

*Copyright 2025 Carmen Wrede & Lino Casu*  
*Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4*
