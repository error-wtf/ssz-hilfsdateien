# RAW LIGO HDF5 PROVENANCE AUDIT
**Datum:** 2026-05-20 04:57 CEST
**Autor:** Bingsi (Hermes Agent)
**Skript:** scripts/run_hdf5_provenance_audit.py
**Status:** ✅ COMPLETE — STEP 02 abgeschlossen

---

## Ergebnis

```
✅ ALLE 6 STRAIN-HDF5-DATEIEN VERIFIZIERT
✅ TRIGGER 1411261107.984 LIEGT IN ALLEN 6 DATEIEN
✅ SHA256, HDF5-KEYS, ATTRIBUTES, STRAIN-STATS ERHOBEN
✅ min/max/mean/std, ERSTE/LETZTE SAMPLES EXTRAHIERT
```

---

## Dateien

| # | Detektor | Rate | Dateigröße | SHA256 (erste 16 Zeichen) |
|---|----------|------|-----------|---------------------------|
| 1 | H1 (Hanford) | 4kHz | 54.0 MB | 4da44bd2e5e17716 |
| 2 | H1 (Hanford) | 16kHz | 213.8 MB | 281104d46d00c3b7 |
| 3 | L1 (Livingston) | 4kHz | 128.7 MB | 188d5b71e0d1a77b |
| 4 | L1 (Livingston) | 16kHz | 509.6 MB | 227c901099df700c |
| 5 | V1 (Virgo) | 4kHz | 70.5 MB | f5777c40857bc42d |
| 6 | V1 (Virgo) | 16kHz | 289.3 MB | 838ec65b8502c5ed |

---

## GPS / Trigger

```
GPS-Start:  1411260416.0 (aus HDF5-Attribut GPSstart)
Dauer:      4096s (aus HDF5-Attribut Duration)
GPS-Ende:   1411264512.0

Trigger:    1411261107.984
Offset:     691.984s (vom Start)

TRIGGER IM FENSTER: JA ✅ (alle 6 Dateien)
```

---

## HDF5-Struktur

```
Root-Keys (alle Detektoren): ['meta', 'quality', 'strain']
Strain-Dataset-Pfad: strain/Strain
Strain-dtype: float64
```

**Wichtig:** H1 4kHz/16kHz enthalten NaN-Segmente (~58% der Datei).
Das Trigger-Fenster (±2s, 16384 Samples bei 4kHz) ist **komplett NaN-frei**
und liefert valide Strain-Werte.

---

## Strain-Statistiken (TRIGGER-FENSTER, ±2s, 4kHz)

| Detektor | min | max | mean | std |
|----------|-----|-----|------|-----|
| H1 | −7.25e-18 | +7.09e-18 | −2.01e-20 | 2.73e-18 |
| L1 | −2.29e-17 | +2.26e-17 | +4.57e-23 | 3.55e-18 |
| V1 | −8.48e-18 | +8.51e-18 | +3.15e-24 | 1.17e-18 |

**H1-Trigger-Fenster (direkt verifiziert):**
- 16384 Samples, min=−7.2509e-18, max=7.0932e-18, mean=−2.0062e-20, std=2.7274e-18
- NaN: 0, Inf: 0
- → Konsistent mit REAL_STRAIN_LOAD_REPORT.md

---

## Wichtige Beobachtungen

### H1 NaN-Segmente

H1 hat ~58% NaN-Anteil im gesamten 4096s-File. Dies ist GWOSC-typisch:
Segmente ohne Science-Mode-Daten werden als NaN markiert. Das **Trigger-Fenster**
ist komplett sauber.

### L1 und V1

L1 und V1 haben keine NaN-Segmente (0% NaN). Strain-Werte durchgehend
valide über die gesamten 4096s.

### Strain-Größenordnungen

Alle drei Detektoren zeigen plausible Strain-Amplituden (~10⁻¹⁸),
konsistent mit typischen GWOSC-O4-Daten.

---

## Ausgabedateien

```
JSON: reports/progress/raw_ligo_hdf5_provenance.json
CSV:  data_manifest/raw_ligo_hdf5_manifest.csv
LOG:  reports/progress/raw_ligo_hdf5_provenance_audit.md  (diese Datei)
```

---

## Nächster Schritt

Mit verifizierten HDF5-Hashes und bestätigtem Trigger-Fenster kann jetzt:
1. Pipeline mit HDF5-Hash-Logging neu ausgeführt werden
2. REPORT_PROVENANCE_AUDIT durchgeführt werden
3. CSVs mit HDF5-Hashes verknüpft werden
