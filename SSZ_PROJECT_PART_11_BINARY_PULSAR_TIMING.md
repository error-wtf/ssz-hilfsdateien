# ChatGPT Project SSZ Compilation — Part 11 / 17
## Category: BINARY PULSAR TIMING

This is compiled ChatGPT Project file 11 of 17. It contains verbatim transcripts of all unique markdown documents related to this specific physical or experimental domain, sorted alphabetically by repository and path. Old historical duplicate folders have been actively deduplicated.

- **Total Files Compiled (Deduplicated):** 1
- **Total Verbatim Lines:** 186



# =========================================================================
# FILE: galactic-year/README.md
# =========================================================================

# Galactic Year - Sonnenorbit Simulation

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue)](https://python.org)
[![License](https://img.shields.io/badge/License-Antikapitalistisch%201.4-red)](LICENSE)
[![SSZ](https://img.shields.io/badge/SSZ-Framework-orange)](https://github.com/topics/segmented-spacetime)

**Berechnung und Visualisierung der galaktischen Umlaufbahn der Sonne mit klassischer Kepler-Mechanik und dem Segmented Spacetime (SSZ) Framework.**

Dieses Repository berechnet die Umlaufbahn der Sonne um das galaktische Zentrum (Sagittarius A*) unter Verwendung:
- **Echter astronomischer Daten** von der SIMBAD-Datenbank
- **Klassischer Kepler-Mechanik** (Newton/GR)
- **Segmented Spacetime (SSZ)** Zeitdilatationskorrekturen

---

## Übersicht

Die Sonne benötigt ca. **230 Millionen Jahre** für einen Umlauf um das galaktische Zentrum. Dieses Projekt simuliert:
- Exzentrische Bahn mit **8.3 kpc** mittlerem Abstand
- Vertikale Oszillation (ca. **±80 pc**)
- SSZ-Zeitdilatationseffekte

---

## Animationen

### 1. Klassische Kepler-Bahn (2D)

![Klassische Umlaufbahn](https://raw.githubusercontent.com/error-wtf/galactic-year/main/output/01_orbit_classical.gif)

Die klassische elliptische Umlaufbahn mit radialer Geschwindigkeitsvariation:
- Perigalaktikum: ~7.8 kpc (schnellste Bewegung)
- Apogalaktikum: ~9.2 kpc (langsamste Bewegung)
- Bahnebenen-Neigung: ca. 0.5°

---

### 2. SSZ vs. Klassisch - Seitlicher Vergleich

![SSZ Vergleich](https://raw.githubusercontent.com/error-wtf/galactic-year/main/output/02_orbit_ssz_comparison.gif)

Direkter Vergleich der klassischen und SSZ-korrigierten Bahn:
- Ξ(R₀) ≈ 6×10⁻⁸
- D(R₀) ≈ 0.99999994
- Geschwindigkeitsreduktion: ~0.0000%

---

### 3. 3D-Animation mit vertikaler Oszillation

![3D Umlaufbahn](https://raw.githubusercontent.com/error-wtf/galactic-year/main/output/03_orbit_3d.gif)

Die vollständige 3D-Bahn zeigt die vertikale Oszillation:
- Vertikale Amplitude: ±0.08 kpc
- Oszillationsperiode: ~70 Millionen Jahre
- Rotierende Kameraansicht

---

### 4. Solar Orbit 2D (Erweitert)

![Solar Orbit 2D](https://raw.githubusercontent.com/error-wtf/galactic-year/main/output/solar_orbit_2d.gif)

Detaillierte 2D-Darstellung über mehrere Galaktische Jahre:
- Dateigröße: ~18 MB
- Dauer: Mehrere Umläufe
- Mit Geschwindigkeitsvektoren

---

### 5. Solar Orbit 3D (Erweitert)

![Solar Orbit 3D](https://raw.githubusercontent.com/error-wtf/galactic-year/main/output/solar_orbit_3d.gif)

Hochauflösende 3D-Visualisierung:
- Dateigröße: ~13 MB
- Frei rotierbare 3D-Ansicht
- Zeigt die "Wobbel"-Bewegung durch die Galaxie

---

### 6. Aktuelle Position (Statisch)

![Aktuelle Position](https://raw.githubusercontent.com/error-wtf/galactic-year/main/output/solar_orbit_now.png)

Snapshot der aktuellen Sonnenposition in der Galaxie.

---

## Physikalische Grundlagen

### Klassische Mechanik

```
v = √(GM/r)
T = 2π √(a³/GM)
```

**Parameter:**
- M(Sgr A*) ≈ 4.3 × 10⁶ M☉
- R₀ ≈ 8.3 kpc
- Exzentrizität e ≈ 0.07

### SSZ (Segmented Spacetime) Framework

**Zeitdilatation:** `D(r) = 1/(1 + Ξ(r))`

**Weak Field:** `Ξ(r) = r_s/(2r)` für r >> r_s

**Strong Field:** `Ξ(r) = 1 - exp(-φ · r_s / r)` für r ~ r_s

Mit φ = (1 + √5)/2 ≈ 1.618 (Goldener Schnitt)

---

## Installation

```bash
pip install -r requirements.txt
```

**Abhängigkeiten:** numpy, matplotlib, imageio, tqdm, requests

---

## Verwendung

```bash
# Komplette Pipeline
python run_all.py

# Einzelne Schritte
python fetch_orbit_data.py
python calculate_ssz_orbit.py
python animate_orbit.py
```

---

## Ausgabedateien

| Datei | Größe | Beschreibung |
|-------|-------|--------------|
| `01_orbit_classical.gif` | ~58 KB | Klassische 2D-Animation |
| `02_orbit_ssz_comparison.gif` | ~85 KB | SSZ Vergleich |
| `03_orbit_3d.gif` | ~85 KB | 3D-Animation |
| `solar_orbit_2d.gif` | ~18 MB | Erweiterte 2D-Bahn |
| `solar_orbit_3d.gif` | ~13 MB | Erweiterte 3D-Ansicht |
| `solar_orbit_now.png` | ~482 KB | Aktuelle Position |

---

## Ergebnisse

| Parameter | Wert |
|-----------|------|
| Ξ(R₀) | 6.2 × 10⁻⁸ |
| D(R₀) | 0.999999938 |
| Umlaufzeit | 230.0 Millionen Jahre |
| Mittlere Geschwindigkeit | 247.8 km/s |

---

## Autoren

- **Lino Casu** - Konzept & SSZ-Physik
- **Carmen Wrede** - SSZ Framework Entwicklung

---

## Lizenz

**Antikapitalistische Lizenz 1.4**

Copyright (c) 2026 Lino Casu & Carmen Wrede

- ✅ Nicht-kommerzielle Nutzung frei
- ✅ Bildung/Forschung willkommen  
- ⚠️ Kommerzielle Nutzung nur mit Genehmigung
- ❌ Militärische & Überwachungszwecke verboten

Siehe [LICENSE](LICENSE) für vollständigen Text.

---

**Repository:** https://github.com/error-wtf/galactic-year
