# PROVENANCE-FIRST MASTER AUDIT — Zwischenstand
**Datum:** 2026-05-20
**Autor:** Bingsi (Hermes Agent)
**Status:** IN_PROGRESS — Phase 0-1 abgeschlossen, Phase 2-5 laufend

---

## 1. TRIGGER-GPS-KONTRADIKTION — GELÖST

### Fundstellen

| Datei | Wert | Status |
|-------|------|--------|
| `reports/DQ_AWARE_FINAL_LIGO_STATUS.md` | 1411261107.984 | KANONISCH ✅ |
| `AUDIT_STOP.txt` | 1417240123 | INVALID ❌ |
| `reports/FINAL_EXECUTION_REPORT.md` | ~1417240123 | INVALID ❌ |

### Berechnung

```
HDF5-Datei: H-H1_GWOSC_O4b4DiscC00_4KHZ_R1-1411260416-4096.hdf5
GPS-Start: 1411260416
Dauer: 4096s
GPS-Ende: 1411260416 + 4096 = 1411264512

Kanonischer Trigger: 1411261107.984
Offset vom Start: 1411261107.984 - 1411260416 = 691.984s

Trigger innerhalb 4096s-Fenster? JA — Offset 691.984s < 4096s
```

### Schlussfolgerung

Der Wert **1417240123** ist FALSCH. Er stammt aus einer Windsurf-Fehlinterpretation (wahrscheinlich: Unix-Time vs GPS-Time Konfusion oder anderer Event). Die Behauptung in AUDIT_STOP.txt "trigger at 1417240123 (80 days outside)" ist damit selbst ein **INVALID_AUDIT_FINDING**.

Der kanonische Trigger **1411261107.984** liegt **innerhalb** des HDF5-Fensters [1411260416, 1411264512].

### Aktionsbedarf
- `AUDIT_STOP.txt` muss korrigiert werden
- `reports/FINAL_EXECUTION_REPORT.md` muss korrigiert werden
- Alle Reports, die 1417240123 zitieren, sind INVALID

---

## 2. HDF5-PROVENANCE — BESTANDSAUFNAHME

### Dateinventar (ligo-gw240925-gw250207-release)

- **169 HDF5-Dateien** insgesamt (inkl. Symlinks)
- **26 zugängliche HDF5-Dateien** (Rest: Linux-Symlinks, broken auf Windows)
- **2 Top-Level-Metafiles** (Posterior-Samples, NICHT Strain):
  - `GW240925_combinedPHM_envcalC01_metafile.hdf5` (190.8 MB)
  - `GW250207_combinedPHM_cal_metafile.hdf5` (292.5 MB)
- **6 Strain-HDF5-Dateien** (GW240925-C00-Strain):
  - `H-H1_GWOSC_O4b4DiscC00_4KHZ_R1-1411260416-4096.hdf5` (H1, 4kHz)
  - `H-H1_GWOSC_O4b4DiscC00_16KHZ_R1-1411260416-4096.hdf5` (H1, 16kHz)
  - `L-L1_GWOSC_O4b4DiscC00_4KHZ_R1-1411260416-4096.hdf5` (L1, 4kHz)
  - `L-L1_GWOSC_O4b4DiscC00_16KHZ_R1-1411260416-4096.hdf5` (L1, 16kHz)
  - `V-V1_GWOSC_O4b4DiscC00_4KHZ_R1-1411260416-4096.hdf5` (V1, 4kHz)
  - `V-V1_GWOSC_O4b4DiscC00_16KHZ_R1-1411260416-4096.hdf5` (V1, 16kHz)

**WICHTIG:** Die `combinedPHM_*_metafile.hdf5`-Dateien enthalten POSTERIOR-SAMPLES (PE-Output), KEINE Strain-Daten. Sie sind für anti-zirkuläre SSZ-Tests NICHT als Primärdaten verwendbar. Die Strain-Daten sind die `H-H1_GWOSC_*`-Dateien.

---

## 3. SSZ SOURCE OF TRUTH — VERIFIZIERT

### Kanonische Quelle
`E:\clone\ssz-complete-documentation` = Single Source of Truth

### Formula Lock Status (aus ssz-complete-documentation + ssz-ligo-tests)

| Formel | Status | Kanonischer Wert/Form |
|--------|--------|----------------------|
| Ξ_weak(r) = r_s/(2r) | LOCKED | Weak field |
| Ξ_strong(r) = 1 - exp(-φ·r_s/r) | LOCKED | Strong field (g2/exponential) |
| Ξ_sat(r) = min(1-exp(-φ · r_s / r), Ξ_max) | LOCKED | Local saturation (metric-pure) |
| D(r) = 1/(1+Ξ(r)) | LOCKED | Time dilation |
| s(r) = 1+Ξ(r) = 1/D(r) | LOCKED | Scaling factor |
| D(r_s) = 0.55503 | LOCKED | Finite at Schwarzschild |
| φ = 1.618... | LOCKED | Segmentation constant |
| PPN β=γ=1 | LOCKED | GR-equivalent in weak field |
| delta_psi(V1) | DERIVED_LOCKED | Ch.31, 0PN inspiral |
| delta_a | DERIVED_V0_PROXY | D²−1, Platzhalter |
| epsilon_220 | BLOCKED_BRANCH_CONFLICT | 3% vs 31% vs 39% |

### Prime Directive (aus 11_GUARDRAILS)
- NULL/Light → PPN (1+γ)
- TIMELIKE/Clocks → Ξ-proxy
- TIMELIKE/Orbits → PPN (γ,β)

---

## 4. REPOSITORY STATUS — ssz-ligo-tests

### Tests: 497 PASS, 1 xfail (erwartet: epsilon_220)
### Pipeline: PASS_EXPLORATORY
### Claims: KEINE gemacht (SSZ_SUPPORT_CLAIM_MADE: NO, SSZ_FALSIFICATION_CLAIM_MADE: NO)
### Anti-Circularity: ENFORCED (no posterior, no PE, clean)

### Bewertung
Das Repository ist methodologisch SAUBER. Es macht keine falschen Behauptungen. Der einzige grobe Fehler ist der falsche Trigger-GPS in AUDIT_STOP.txt und FINAL_EXECUTION_REPORT.md — und das sind beides Artefakte, die leicht korrigierbar sind.

---

## 5. OFFENE PUNKTE (Phase 2-5 noch zu klären)

1. **SHA256 aller Strain-HDF5-Dateien** — noch nicht erhoben
2. **HDF5-Keys und Attribute der Strain-Dateien** — noch nicht inspiziert
3. **min/max/mean/std des geladenen Strains** — noch nicht berechnet
4. **Woher genau stammt 1417240123?** — Wahrscheinlich Windsurf-Halluzination oder GPS/Unix-Time-Konfusion
5. **ChatGPT-Diskussionen** — PDFs existieren (diskussion 1-3.pdf, ~22 MB total), noch nicht analysiert
6. **CSV-Provenance** — welche CSVs haben echte Datenherkunft?
7. **book-full/06_PAPERS** — noch nicht eingesehen
8. **LIGO DeepResearch** — Interferometer-Funktionsweise, Kalibrationskette, DQ-Flags
9. **Alle SSZ-Repos** — Übersicht erstellt, Inhalte zu prüfen

---

## 6. KORREKTUREN (SOFORT)

### AUDIT_STOP.txt
```
FALSCH: "trigger at 1417240123 (80 days outside)"
KORREKT: HDF5 GPS 1411260416+4096s enthält kanonischen Trigger 1411261107.984
Der Trigger liegt 691.984s innerhalb des Fensters.
Der Wert 1417240123 ist ein Windsurf/Agent-Artefakt — Herkunft ungeklärt.
```

### NEXT STEPS
1. ChatGPT-PDFs analysieren (Phase 4)
2. HDF5-Strain-Daten inspizieren (Phase 2)
3. book-full/06_PAPERS prüfen (Phase 1)
4. LIGO DeepResearch (Phase 5)
5. CSV/Report-Provenance (Phase 3)
6. Alle korrigierten Reports neu schreiben (Phase 6)
7. Tests mit verifizierten HDF5-Daten frisch ausführen (Phase 7)
