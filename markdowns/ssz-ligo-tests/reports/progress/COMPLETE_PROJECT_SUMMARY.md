# Complete Project Summary — SSZ-LIGO-Tests
**Datum:** 2026-05-20
**Autor:** Bingsi (Hermes Agent)
**Status:** ZWISCHENSTAND — Keine neuen Fixes bis Freigabe

---

## 1. Project Goal

### 1.1 Was ist das Ziel von ssz-ligo-tests?

Das Repository soll testen, ob das Segmented-Spacetime-Modell (SSZ) eine
messbare Abweichung von der Allgemeinen Relativitätstheorie (GR) in echten
LIGO-Daten erzeugt — **ohne** dabei LIGO-eigene Parameter-Schätzungen
(Massen, Spins, QNM-Frequenzen) zu verwenden.

Ziel ist NICHT:
- SSZ zu beweisen
- SSZ zu widerlegen
- LIGO-Daten als falsch darzustellen

Ziel IST:
- Eine methodisch saubere Pipeline zu bauen, die SSZ-Forward-Model
  direkt auf kalibrierten Strain anwendet
- Anti-zirkulär zu bleiben (keine GR-Posterior-Produkte als SSZ-Input)
- Reproduzierbarkeitslücken zu dokumentieren
- Claim-Disziplin zu wahren

### 1.2 Warum LIGO anders ist als Teleskopdaten/NICER

LIGO misst keine Position, keine Helligkeit, keine Spektrallinie. Es misst
Differentiellen Arm-Längen-Change (DARM) — Sub-Atomare Verschiebungen von
Spiegeln, die Kilometer voneinander entfernt sind. Das Rohsignal ist ein
Kontroll-Fehler-Signal, kein direktes astrophysikalisches Observablen-Äquivalent.

Teleskop: Photonen → Spektrum → physikalische Größe (z.B. Temperatur)
LIGO: DARM → Kalibrationsmodell → h(t) → Matched Filter → Posterior

Jeder Schritt ist modellabhängig. Strain h(t) ist bereits ein
kalibriertes, gefiltertes, DQ-klassifiziertes Produkt.

### 1.3 Warum ein SSZ-LIGO-Test strain-level sein muss

Posterior-Produkte (Massen, Spins, QNM-Frequenzen) sind Ergebnisse
einer GR/Kerr-konditionierten Inferenz. Wenn man diese als SSZ-Input
verwendet, testet man nicht SSZ gegen LIGO — man testet, ob
SSZ+GR-Inferenz-Output konsistent mit GR-Inferenz-Output ist.

Nur kalibrierter Strain h(t) ist (näherungsweise) modellneutral.
Deshalb: SSZ muss auf Strain angewendet werden, nicht auf Posterioren.

### 1.4 Warum PE/QNM/Posterior-Produkte nicht erlaubt sind

| Produkt | Warum nicht metric-neutral |
|---------|---------------------------|
| m1, m2, M_chirp | Aus GR/CBC-Templates geschätzt |
| Spins χ1, χ2 | Aus Kerr-Metrik-Templates geschätzt |
| QNM-Frequenzen | Aus Kerr-QNM-Modellen geschätzt |
| Bayessche Posterioren | Bedingt auf GR-Waveform-Modelle |
| Remnant-Masse, -Spin | Aus NR/GR-Konsistenz-Relationen |

Diese Produkte sind **Inferenz-Output, nicht Mess-Input**.

### 1.5 Warum kein SSZ-Claim und keine Falsifikation

- SSZ hat kein finales, vollständiges LIGO-Forward-Modell (RSG-Phasenintegral fehlt)
- V0/V1-Formeln sind Proxies, nicht finale Derivierungen
- ε220 ist BLOCKED_BRANCH_CONFLICT
- L1-DQ ist ungeklärt
- Nur N=1 Off-source-Fenster

→ Kein Claim möglich. Das Repo dokumentiert das transparent.

---

## 2. Current Repository State

### 2.1 Hauptordner

```
E:\clone\ssz-ligo-tests\
├── src/ssz_ligo_tests/     — Python-Package (17 Module)
├── tests/                   — Test-Suite (unit, validation, integration)
├── scripts/                 — 68 Ausführungsskripte
├── reports/                 — 78 Report-Dateien (+ 3 neue in progress/)
├── docs/                    — 20+ Dokumentationsdateien
├── data_manifest/           — CSVs, Inventare
├── logs/                    — Ausführungslogs
```

### 2.2 Reports (Auswahl)

| Kategorie | Beispiele |
|-----------|----------|
| Status-Gates | DQ_AWARE_FINAL_LIGO_STATUS.md, FINAL_INTERPRETATION_LOCK.md |
| Pipeline | FINAL_EXECUTION_REPORT.md, REAL_STRAIN_LOAD_REPORT.md |
| Anti-Circularity | ANTI_CIRCULARITY_FINAL_GATE.md, GLOBAL_ANTI_CIRCULARITY_RULE.md |
| L1-Diagnostik | L1_ANOMALY_DIAGNOSTIC_REPORT.md, L1_GAUSSIANITY_TEST.md |
| H1/L1-Kohärenz | H1_L1_COHERENCE_PIPELINE_REPORT.md, H1_L1_LONG_BASELINE_REPLICATION_REPORT.md |
| Artifact-Gates | GAUSSIANITY_ARTIFACT_GATE_REPORT.md, ARTIFACT_SCORE_REPORT.md |
| SSZ-Forward | SSZ_FORWARD_APPLICATION_REPORT.md, DERIVED_V0_STRAIN_PIPELINE_REPORT.md |
| Methodologie | LIGO_RELEASE_MASTER_STATUS_REPORT.md, OPEN_DATA_METHODOLOGY_POSITION.md |

### 2.3 Tests — WICHTIGE KORREKTUR

**README.md behauptet: "497 PASS, 1 xfail"**

Der tatsächliche pytest-Log (PYTEST_FULL_RUN_REPORT.md, 2026-05-18) zeigt:

```
176 Tests gesammelt
123 PASS
 52 FAIL
  1 XFAIL
Exit Code: 1 (FAIL)
```

Die 52 FAILS fallen in Kategorien:
- 16× AttributeError: SSZForwardModel-Methoden fehlen (Code-API-Änderungen)
- 12× NameError: D_ssz, D_gr Import-Probleme (unit/validation tests)
- 9× AssertionError: Wert-Änderungen (Ξ_strong, Regime-Erkennung)
- 15× AssertionError: Status-String-Änderungen (CONFLICTING → PARTIAL_EXPLORATORY)

**Die README-Angabe "497 PASS" ist veraltet/falsch und muss korrigiert werden.**

### 2.4 Datenlage

| Typ | Dateien | Status |
|-----|---------|--------|
| Strain HDF5 (H1, L1, V1) | 6 × je 4kHz+16kHz | Pfade bekannt, Hashes fehlen |
| Posterior-Metafiles | 2 Dateien (190+292 MB) | NICHT für SSZ verwendbar |
| CSVs (data_manifest) | ~6 Dateien | Ungeprüfte Provenance |
| GW250207 Strain | 0 Dateien | Nicht heruntergeladen (laut artifact_score) |

### 2.5 V0/V1/Proxy/Synthetic/Real Klassifikation

| Typ | Was | Status |
|-----|-----|--------|
| V1 LOCKED | delta_psi_SSZ (0PN), rdot_SSZ, P_GW_SSZ | Aus SSZ-Buch Ch.31 deriviert |
| V0 PROXY | delta_a = D²−1, h_SSZ Konstruktion | Explorative Platzhalter |
| Synthetic | Twist-Branch, GA-Interferometer | Reine Simulationen |
| Real HDF5 | Strain-Pipeline, L1-Diagnostik | Echte GWOSC-Daten |
| Real (blockiert) | H1/L1-Kohärenz, Twist-Real | Blockiert durch L1-DQ |

---

## 3. Source-of-Truth State

### 3.1 SSZ Source of Truth

```
PRIMÄR:
  E:\clone\ssz-complete-documentation\
    → formula_compendium.md, ssz_overview.md, prime_directive.md
  E:\clone\book-full\06_PAPERS\
    → NICHT EINGESEHEN (30+ Paper)

SEKUNDÄR (nur bei Konsistenz mit Primär):
  ssz-ligo-tests/docs/ (SSZ-Formel-Derivationen)
  ssz-ligo-tests/src/ssz_ligo_tests/ (Code-Locks)
```

### 3.2 LIGO Data Source

```
E:\clone\ligo-gw240925-gw250207-release\
  Zenodo: 10.5281/zenodo.18600070
  → Strain: 6 HDF5 (H1/L1/V1 × 4kHz/16kHz)
  → Posterioren: 2 Metafiles (combinedPHM)
  → Symlinks: ~140 broken auf Windows
```

### 3.3 LIGO Test Repo

```
E:\clone\ssz-ligo-tests\
  → Dieses Repository
  → Privat gestellt (Sicherheitsmaßnahme)
```

### 3.4 ChatGPT/Windsurf-Material

```
E:\
  ligo chatgpt diskussion 1.pdf  — NICHT GELESEN (22 MB PDF)
  ligo chatgpt diskussion 2.pdf  — NICHT GELESEN
  ligo chatgpt diskussion 3.pdf  — NICHT GELESEN

Status: Nur als Fehler-/Entscheidungslog relevant.
        KEINE wissenschaftliche Primärquelle.
```

---

## 4. What Is Actually Known So Far

### VERIFIED (durch Datei/Log belegt)

```
✅ Trigger-GPS = 1411261107.984 (DQ_AWARE_FINAL_LIGO_STATUS.md Z.4)
✅ HDF5-Fenster = [1411260416, 1411264512] (Dateiname)
✅ Trigger liegt im Fenster: Offset 691.984s (Berechnung)
✅ 1417240123 ist FALSCH — nur in AUDIT_STOP.txt + FINAL_EXECUTION_REPORT.md
✅ H1 Strain geladen: 16384 samples, mean=-2.0e-20, std=2.73e-18 (REAL_STRAIN_LOAD_REPORT.md)
✅ DQ-Bits VERIFIED_FROM_HDF5: CBC_CAT2/CAT3 clean an beiden Detektoren
✅ L1 zeigt reproduzierbaren Bandpower-Exzess (2.28×)
✅ L1 CW_CAT1=0 und NO_CW_HW_INJ=0 sind file-wide, nicht trigger-spezifisch
✅ Kein SSZ-Claim, keine Falsifikation (mehrfach dokumentiert)
✅ Anti-Circularity-Regeln eingehalten
✅ 123 Tests PASS, 52 FAIL, 1 XFAIL (pytest-log)
```

### LIMITED (teilweise belegt, Einschränkungen)

```
⚠️ N=1 Off-source-Fenster (keine statistische Signifikanz)
⚠️ V0-Proxy deltaA = D²−1 (explorativ, keine finale Formel)
⚠️ 0PN GR-Control (keine 3.5PN-Templates)
⚠️ L1 Gaussianity: FAIL (chronisch, nicht trigger-spezifisch)
⚠️ Keine Omicron/iDQ offline DQ-Produkte
```

### UNVERIFIED (nicht durch eigene Prüfung belegt)

```
❓ HDF5-Hashes (SHA256) — nicht berechnet
❓ HDF5-Keys/Dataset-Struktur — nicht aus HDF5 gelesen
❓ CSV-Provenance — nicht geprüft
❓ Pipeline-Neuausführung mit verifizierten Daten — nicht durchgeführt
❓ Alle Reports außer den 5 manuell geprüften
❓ GW250207 Strain — nicht vorhanden/nicht geprüft
```

### INVALID (nachgewiesen falsch)

```
❌ AUDIT_STOP.txt: "trigger at 1417240123 (80 days outside)"
❌ FINAL_EXECUTION_REPORT.md Z.41-44: "trigger at GPS ~1417240123 ... Delta: ~69.2 days"
❌ README.md: "497 PASS" — tatsächlich 123 PASS + 52 FAIL
```

### UNKNOWN (keine ausreichende Information)

```
❓ Herkunft von 1417240123 (Windsurf-Halluzination? GPS/Unix-Konfusion?)
❓ ChatGPT-Diskussionen (PDFs nicht lesbar)
❓ book-full/06_PAPERS-Inhalte
❓ LIGO-Kalibrationskette (DeepResearch blockiert)
```

---

## 5. Major Risks

### 5.1 Technische Risiken

| Risiko | Schwere | Status |
|--------|---------|--------|
| Falscher Trigger-GPS (1417240123) in 2 Dateien | HOCH | Identifiziert, markiert, nicht korrigiert |
| Reports ohne HDF5-Provenance | HOCH | ~70 Reports ungeprüft |
| CSVs ohne Rohdatenkette | HOCH | Nicht nachverfolgbar |
| N=1 Off-source-Fenster | MITTEL | Dokumentiert, limitiert Statistik |
| Windsurf-generierte Reports | MITTEL | Könnten ohne echte Execution entstanden sein |
| Synthetic Tests ≠ Real Tests | MITTEL | README unterscheidet, aber Vermischung möglich |
| README "497 PASS" ist falsch | MITTEL | Tatsächlich 123 PASS + 52 FAIL |
| Alte Windsurf-Artefakte in data_manifest/ | NIEDRIG | Noch nicht identifiziert |

### 5.2 Datenrisiken

| Risiko | Schwere | Status |
|--------|---------|--------|
| LIGO DQ/Omicron/iDQ fehlen | HOCH | Blockiert H1/L1-Kohärenz-Claims |
| Keine Kalibrations-Unsicherheit | MITTEL | Blockiert Präzisions-Claims |
| Keine Aux-Channel-Daten | MITTEL | Keine unabhängige DQ-Verifikation |
| GW250207 Strain fehlt | NIEDRIG | Zweites Event für Kreuzvalidierung |

### 5.3 Methodische Risiken

| Risiko | Schwere | Status |
|--------|---------|--------|
| SSZ-V0/V1-Proxies als finale Formeln missverstanden | HOCH | README dokumentiert korrekt, aber Reports könnten abweichen |
| Synthetic-Tests als Real-Tests präsentiert | MITTEL | Klassifikation in README, Reports zu prüfen |
| Anti-Circularity-Verletzung durch ungeprüfte Scripts | MITTEL | Gate-Tests pass, aber nicht alle Scripts geprüft |

### 5.4 Reputationsrisiken

| Risiko | Schwere | Status |
|--------|---------|--------|
| "497 PASS" im README bei tatsächlich 52 FAIL | HOCH | Public-facing — muss korrigiert werden |
| README Reproducibility-Kritik zu scharf formuliert | MITTEL | Sections 1-5 der README sind methodisch sauber, aber politisch exponiert |
| Falscher Trigger als "Datenfehler" statt "Auditfehler" | MITTEL | Korrigiert in progress/-Dateien |
| Veröffentlichung vor Provenance-Audit | HOCH | Repo ist privat — Sicherheitsmaßnahme korrekt |

---

## 6. Current Safe Public Position

### Was das Repo sagt (korrekt, eingehalten)

```
- Strain = Measurement Input
- Posterior Products = Model-Conditioned Inference Output
- Kein SSZ-Claim (SSZ_SUPPORT_CLAIM_MADE: NO)
- Keine SSZ-Falsifikation (SSZ_FALSIFICATION_CLAIM_MADE: NO)
- Keine Anschuldigungen bezüglich Fehlverhaltens oder Datenmanipulation
- Fokus: Provenance, Reproducibility, Anti-Circular Method
```

### Was das Repo sagen sollte (Empfehlung)

```
"Public GWOSC products are useful for standard GR/CBC workflows,
but are not a full public reconstruction package for independent
anti-circular non-GR forward-model tests."

"Full non-GR reproducibility requires calibration traces,
DQ products (Omicron/iDQ), AUX channels, line lists,
and detector-characterization context."
```

### Was das Repo NICHT sagen darf

```
❌ Behauptungen bezüglich absichtlichen Fehlverhaltens oder Datenmanipulation
❌ "GW240925 is not real"
❌ "SSZ is confirmed/falsified by LIGO"
❌ "Nobelpreis unberechtigt"
❌ "497 PASS" (falsche Zahl)
```

---

**Fazit: Erster vertrauenswürdiger Rettungsstand. Drei kritische INVALID-Funde identifiziert. Keine Panik nötig. Nächster Schritt: Korrektur der INVALID-Elemente + HDF5-Provenance.**
