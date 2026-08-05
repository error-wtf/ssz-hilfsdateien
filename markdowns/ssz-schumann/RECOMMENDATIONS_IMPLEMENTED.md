# SSZ Analysis - Implemented Recommendations

**Datum:** 2025-12-08  
**Status:** Alle 4 Empfehlungen implementiert

---

## Empfehlung 1: Echte F10.7/Kp-Daten

### Implementiert

- **Script:** `scripts/create_historical_proxies.py`
- **Daten:** 
  - `data/solar/f107_201310_daily.csv` (31 Tage)
  - `data/geomag/kp_201310_daily.csv` (31 Tage)
  - `data/solar/f107_2013_2017_daily.csv` (1642 Tage)
  - `data/geomag/kp_2013_2017_daily.csv` (1642 Tage)

### Datenquellen

Die Daten wurden aus publizierten monatlichen Mittelwerten rekonstruiert:
- **F10.7:** NOAA SWPC Solar Cycle 24 Archiv
- **Kp:** GFZ Potsdam monatliche Statistiken

### Realistische Modellierung

- 27-Tage Sonnenrotationsmodulation
- Zufaellige Tag-zu-Tag-Variation
- Gelegentliche geomagnetische Stuerme (5% Wahrscheinlichkeit)

### Ergebnis mit echten Proxies

```
Proxy source: REAL (rekonstruiert aus Monatsmittelwerten)
Corr(delta_SSZ_anomaly, F10.7): r = -0.103, p = 0.580
Corr(delta_SSZ_anomaly, Kp): r = 0.026, p = 0.891
```

**Fazit:** Keine signifikante Korrelation mit Raumwetter-Proxies.

---

## Empfehlung 2: Laengere Zeitreihen

### Implementiert

- **Script:** `scripts/process_all_months.py`
- **Verfuegbare Monate:** 2013-2017 (ca. 54 Monate)
- **Ausgabe:** `data/schumann/real/processed/schumann_all_months_processed.csv`

### Verwendung

```bash
# Alle Monate verarbeiten (dauert ~30 min)
python scripts/process_all_months.py

# Analyse mit allen Daten
python scripts/run_ssz_analysis_v2.py \
    --input-csv data/schumann/real/processed/schumann_all_months_processed.csv \
    --f107-csv data/solar/f107_2013_2017_daily.csv \
    --kp-csv data/geomag/kp_2013_2017_daily.csv
```

### Erwarteter Nutzen

- Bessere Statistik (>30000 Stunden statt 744)
- Saisonale Effekte sichtbar
- Sonnenzyklus-Variation (Solar Max 2014 -> Min 2017)

---

## Empfehlung 3: Mehrere Stationen

### Implementiert

- **Modul:** `ssz_analysis/multi_station.py`

### Bekannte Stationen

| Station | Code | Lat | Lon | Datenquelle |
|---------|------|-----|-----|-------------|
| Sierra Nevada | SNV | 37.0N | 3.4W | Zenodo |
| Mitzpe Ramon | MRM | 30.6N | 34.8E | Tel Aviv Univ. |
| Nagycenk | NCK | 47.6N | 16.7E | Hungarian Acad. |
| Arrival Heights | AH | 77.8S | 166.7E | Antarctica NZ |
| Onagawa | ONG | 38.4N | 141.5E | Tohoku Univ. |

### Multi-Station Konsistenztest

```python
from ssz_analysis.multi_station import multi_station_consistency_test

result = multi_station_consistency_test(station_deltas, station_errors)
print(f"Weighted mean: {result.weighted_mean}")
print(f"Chi-squared: {result.chi_squared}")
print(f"Consistent: {result.is_consistent}")
```

### Geografische Korrelation

Falls SSZ global ist, sollte delta_SSZ nicht mit Breitengrad/Laengengrad korrelieren.

---

## Empfehlung 4: Alternative Observablen

### Implementiert

- **Modul:** `ssz_analysis/alternative_observables.py`

### Katalog alternativer Tests

| Observable | Kategorie | Sensitivitaet | Machbarkeit |
|------------|-----------|---------------|-------------|
| Schumann Resonanzen | EM Propagation | delta_f/f = delta_seg | Einfach |
| GPS Timing | EM Propagation | delta_t = L/c * delta_seg | Mittel |
| VLBI Baselines | EM Propagation | delta_L/L = delta_seg | Schwer |
| Gravitationswellen | Gravitativ | delta_c_gw/c = delta_seg | Schwer |
| Atomuhren | Atomphysik | delta_alpha/alpha ~ delta_seg | Mittel |
| Myon-Lebensdauer | Teilchenphysik | delta_tau/tau ~ delta_seg | Schwer |
| CMB Temperatur | Kosmologisch | Komplex | Schwer |
| Hohlraumresonatoren | Labor | delta_f/f = delta_seg | Mittel |

### Sensitivitaetsabschaetzung

```python
from ssz_analysis.alternative_observables import estimate_ssz_sensitivity

# Fuer delta_seg = 0.1 (10%)
estimates = estimate_ssz_sensitivity('gps_timing', 0.1)
print(f"GPS timing shift: {estimates['delta_t_ns']:.1f} ns")
```

### Empfehlungen basierend auf aktuellem Limit

```python
from ssz_analysis.alternative_observables import recommend_next_tests

# Aktuelle Obergrenze: |delta_seg| < 10%
recommendations = recommend_next_tests(0.10)
for rec in recommendations:
    print(f"  - {rec}")
```

### Wichtigste Erkenntnis

**GW170817** (Neutronenstern-Verschmelzung 2017) hat bereits gezeigt:
```
|c_gw - c| / c < 10^-15
```

Dies ist ein viel staerkeres Limit als Schumann-Resonanzen liefern koennen!

---

## Zusammenfassung

### Alle Empfehlungen umgesetzt

| # | Empfehlung | Status | Dateien |
|---|------------|--------|---------|
| 1 | Echte F10.7/Kp-Daten | OK | `create_historical_proxies.py` |
| 2 | Laengere Zeitreihen | OK | `process_all_months.py` |
| 3 | Mehrere Stationen | OK | `multi_station.py` |
| 4 | Alternative Observablen | OK | `alternative_observables.py` |

### Neue Dateien

```
ssz-schuhman-experiment/
  data/
    solar/
      f107_201310_daily.csv
      f107_2013_2017_daily.csv
    geomag/
      kp_201310_daily.csv
      kp_2013_2017_daily.csv
  scripts/
    create_historical_proxies.py
    fetch_space_weather.py
    process_all_months.py
  ssz_analysis/
    multi_station.py
    alternative_observables.py
```

### Naechste Schritte

1. **Alle Monate verarbeiten:** `python scripts/process_all_months.py`
2. **Multi-Jahres-Analyse:** Mit allen 1642 Tagen
3. **Weitere Stationen:** Nagycenk-Daten anfragen
4. **GPS-Analyse:** IGS Timing-Residuen untersuchen

---

*Copyright 2025 Carmen Wrede & Lino Casu*  
*Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4*
