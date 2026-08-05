# Complete Project Report — SSZ-LIGO-Tests
**Datum:** 2026-05-20
**Autor:** Bingsi (Hermes Agent)
**Status:** ZWISCHENSTAND — Keine neuen Fixes bis Freigabe
**Leser:** Lino Casu, Carmen Wrede

---

## Executive Summary

Das ssz-ligo-tests-Repository wurde von Grund auf geprüft — nicht auf Physik,
sondern auf strukturelle Integrität, Daten-Provenance und Reputationsrisiken.

Die gute Nachricht: Das Repo ist methodologisch sauberer als befürchtet.
Es macht keine falschen Claims, verwendet keine Posterior-Daten und hält
strikte Anti-Circularity-Regeln ein. Der Code ist durchdacht, die Formel-Locks
sind dokumentiert, und die Pipeline lädt echte GWOSC-Daten korrekt.

Die schlechte Nachricht: Drei Dinge sind nachweislich falsch. Der Trigger-GPS-Wert
in AUDIT_STOP.txt und FINAL_EXECUTION_REPORT.md (1417240123) ist ein
Windsurf-Artefakt. Die README-Angabe "497 PASS" entspricht nicht dem
tatsächlichen pytest-Log (123 pass, 52 fail). Und die daraus abgeleitete
Panik ("Trigger 80 Tage außerhalb") war unbegründet — der korrekte Trigger
1411261107.984 liegt 691.984 Sekunden innerhalb des HDF5-Fensters.

Alle drei Fehler sind korrigierbar. Kein Datenfehler. Kein LIGO-Problem.
Ein Audit-Fehler wurde als Datenfehler missverstanden.

---

## What We Tried To Do

Das Projekt hat ein klares, wissenschaftlich legitimes Ziel:

**SSZ (Segmented Spacetime) gegen echte LIGO-Daten testen — ohne durch
GR-Posterior-Produkte zirkulär zu werden.**

Das ist schwerer als es klingt. LIGO veröffentlicht nicht einfach "die Daten".
Was öffentlich verfügbar ist, sind:

- Kalibrierter Strain h(t) — das ist Mess-Input (mit Kalibrationsmodell)
- Posterior-Samples (Massen, Spins, QNM-Frequenzen) — das ist GR-Inferenz-Output

Wenn man Posterioren als SSZ-Input verwendet, testet man nicht SSZ gegen
LIGO. Man testet, ob SSZ+GR konsistent mit GR ist. Das ist ein Zirkelschluss.

Deshalb der Ansatz: Nur Strain verwenden. PSD aus Off-source-Daten schätzen.
GR-Control-Template analytisch (TaylorF2 0PN) — kein Numerical-Relativity-Template.
SSZ-Korrektur direkt auf die Waveform im Frequenzraum anwenden.

Das ist der richtige Ansatz. Methodisch sauber und transparent.

---

## What Went Wrong Before

In der Entwicklungsphase — teilweise mit Windsurf als Coding-Assistent —
sind Fehler passiert. Sie sind dokumentierbar, aber nicht katastrophal.

### 1. Falscher Trigger-GPS-Wert

Der Wert 1417240123 taucht in zwei Dateien auf. Er ist um ~5.98 Millionen
Sekunden (~69 Tage) vom korrekten GW240925-Trigger 1411261107.984 entfernt.

Wahrscheinliche Ursache: Windsurf hat einen GPS-Wert aus einer anderen Quelle
(z.B. Unix-Timestamp, anderes Event, oder schlicht halluziniert) verwendet
und als GW240925-Trigger deklariert. Der korrekte Trigger ist in
GraceDB, im HDF5-Dateinamen und in DQ_AWARE_FINAL_LIGO_STATUS.md dokumentiert.

### 2. Falsche "80 Tage außerhalb"-Behauptung

Aus dem falschen Trigger-Wert wurde geschlossen, dass die vorhandenen
HDF5-Dateien den Trigger nicht abdecken — "80 days outside". Diese
Behauptung löste die Panik aus und führte zu AUDIT_STOP.txt.

In Wirklichkeit liegt der Trigger im Fenster. Der Fehler lag im Audit,
nicht in den Daten.

### 3. README "497 PASS" ist falsch

Das README zitiert stolz "497 PASS, 1 xfail". Der tatsächliche pytest-Log
(PYTEST_FULL_RUN_REPORT.md vom 2026-05-18) zeigt:

```
176 Tests gesammelt
123 PASS
 52 FAIL
  1 XFAIL
Exit Code: 1
```

Die 52 FAILS sind größtenteils API-Änderungen (SSZForwardModel-Methoden
wurden umbenannt oder entfernt) und Import-Fehler (D_ssz, D_gr). Sie sind
technischer Natur, nicht physikalisch. Aber die Zahl im README ist falsch
und muss korrigiert werden.

### 4. Execution Evidence fehlt oder ist unvollständig

Für viele Reports und CSVs fehlt die vollständige Beweiskette:

```
HDF5-Datei → SHA256 → Skript-Command → stdout/stderr → CSV → Report
```

CSVs können von Windsurf generiert worden sein, ohne dass das Skript
tatsächlich lief. Reports können Zahlen enthalten, die nie aus echten
Daten berechnet wurden. Ohne Provenance-Audit ist unklar, welche
Ergebnisse auf echter Execution beruhen und welche auf Artefakten.

Wichtig: Das ist keine Betrugsbehauptung gegen Windsurf. Es ist die
Feststellung, dass Execution Evidence für viele Artefakte fehlt und
nachgeholt werden muss.

---

## What Is Still Valuable

Trotz der Fehler bleibt viel Wertvolles erhalten:

### Struktur und Disziplin

- **Anti-Circularity-Prinzip** — sauber durchdacht und dokumentiert
- **SSZ Source-of-Truth-Trennung** — ssz-complete-documentation als
  kanonische Quelle, LIGO-Daten separat
- **Formula-Lock-System** — LOCKED, DERIVED_V0_PROXY, BLOCKED_BRANCH_CONFLICT
- **Claim-Disziplin** — mehrfach dokumentiert: kein Claim, keine Falsifikation

### Pipeline-Komponenten

- **HDF5-Lader** — liest echte GWOSC-Daten, DQ-Bits aus HDF5-Metadaten
- **PSD-Schätzung** — Welch aus Off-source, korrekt implementiert
- **SSZ-Core** — Ξ, D, s, Regime-Erkennung, getestet und dokumentiert
- **V1-Phasenkorrektur** — delta_psi aus Ch.31 deriviert (0PN)
- **Artifact-Gates** — L1-Diagnostik, Gaussianity, Stationarität

### Diagnostische Befunde (wenn durch echte Execution bestätigt)

- **H1 Strain** geladen und plausibel (std = 2.73e-18)
- **L1 Bandpower-Exzess** reproduzierbar (2.28×)
- **L1 Harmonic-Struktur** mit 60/120 Hz Mains-Lines
- **L1 Gaussianity** chronisch nicht-gaußisch in allen Fenstern
- **DQ-Bits** VERIFIED_FROM_HDF5

### Methodologische Position

Die README-Kritik an der LIGO-Reproduzierbarkeit (Abschnitte 1-5) ist
sachlich, belegt und methodisch sauber. Die fünf Kritikpunkte
(Kalibrationskette, Calibration-Defizit, Code-Provenance, PB-Gap,
GW150914-Replikation) sind dokumentiert und mit Quellen belegt.

---

## What Must Be Rebuilt

### 1. Raw HDF5 Provenance Chain (KRITISCH)

Für jede Strain-Datei:
- SHA256 berechnen
- HDF5-Keys und Attribute auslesen
- Strain min/max/mean/std direkt aus der Datei
- Erste/letzte Samples verifizieren

Ohne das bleibt jeder Report UNVERIFIED_DERIVED.

### 2. Trigger GPS Audit (KRITISCH)

- AUDIT_STOP.txt korrigieren: Trigger 1411261107.984
- FINAL_EXECUTION_REPORT.md korrigieren: Trigger + Offset-Berechnung
- README.md korrigieren: "497 PASS" → "123 PASS, 52 FAIL"

### 3. Real Execution Logs (HOCH)

- Pipeline mit verifizierten HDF5-Daten neu ausführen
- Command + stdout/stderr für jeden Lauf speichern
- SHA256 der verwendeten HDF5 in jedes Log schreiben

### 4. Report Number Verification (HOCH)

- Jede Zahl in jedem Report auf Log/CSV zurückführen
- Zahlen ohne Herkunft als UNVERIFIED markieren
- CSVs ohne HDF5-Hash als DERIVED_UNVERIFIED markieren

### 5. Minimal Verified Pipeline (MITTEL)

- Ein einziges Skript, das den kompletten Pfad abdeckt:
  HDF5 laden → Hash loggen → PSD schätzen → GR-Control → SSZ-Forward → lnL
- Nur das als VERIFIED markieren
- Alles andere UNVERIFIED lassen, bis neu ausgeführt

### 6. README Language (MITTEL)

- "497 PASS" korrigieren
- Keine Änderungen an der methodologischen Kritik nötig
- Status von implizit "Blocked" auf explizit "TRIGGER_IN_WINDOW_VERIFIED"

---

## Recommended Next Steps

### Priorität 1: INVALID-Elemente korrigieren

```
1. AUDIT_STOP.txt: Trigger korrigieren (1417240123 → 1411261107.984)
2. FINAL_EXECUTION_REPORT.md: Trigger + Offset korrigieren
3. README.md: "497 PASS" → "123 PASS, 52 FAIL" + Erklärung
```

### Priorität 2: HDF5-Provenance abschließen

```
4. SHA256 aller 6 Strain-HDF5-Dateien
5. HDF5-Keys + Strain-Daten direkt aus Dateien lesen
6. data_manifest/raw_ligo_hdf5_manifest.csv erstellen
```

### Priorität 3: Report-Audit

```
7. UNVERIFIED_REPORTS_INDEX.md erstellen
8. Alle Reports klassifizieren (VERIFIED/UNVERIFIED/INVALID/SYNTHETIC)
9. CSV-Provenance prüfen
```

### Priorität 4: Pipeline-Neuausführung

```
10. Minimales verified-Audit-Skript schreiben
11. Mit verifizierten HDF5-Daten ausführen
12. Log + CSV + Report aus ECHTEM Run
```

### Priorität 5: Statistische Erweiterung

```
13. Mehr Off-source-Fenster (wenn aus vorhandenen HDF5 möglich)
14. GW250207 Strain herunterladen (zweites Event)
```

### Priorität 6: DeepResearch + ChatGPT (niedrigere Priorität)

```
15. ChatGPT-PDFs lesen (nur für Fehlerlog/Entscheidungslog)
16. book-full/06_PAPERS studieren
17. LIGO-DeepResearch (Interferometer, Kalibration)
```

---

## Final Recommendation

Das Repository sollte **nicht als Physik-Claim veröffentlicht werden**.
Es ist nicht Claim-ready und beansprucht das auch nicht.

Als **Method-Development-Repository** ist es nach Korrektur der drei
INVALID-Elemente (falscher Trigger, falscher Offset, falsche Test-Zahlen)
öffentlich vertretbar. Die Anti-Circularity-Disziplin, die Formel-Locks
und die transparente Dokumentation der Grenzen sind mustergültig.

Die README-Kritik an der LIGO-Reproduzierbarkeit ist sachlich und belegt —
sie sollte erhalten bleiben, aber nicht als Hauptbotschaft des Repos dienen.

**Kernbotschaft für die Öffentlichkeit (wenn veröffentlicht):**

> Dieses Repository demonstriert eine Methodik für anti-zirkuläre,
> forward-modell-basierte Tests alternativer Gravitationstheorien
> mit öffentlichen GWOSC-Daten. Es macht keine physikalischen Claims.
> Es dokumentiert, was mit öffentlichen Daten möglich ist — und was nicht.

---

## Anhang: Die drei INVALID-Funde im Detail

### Fund 1: Falscher Trigger-GPS

```
Datei:     AUDIT_STOP.txt, Zeile 4
Falsch:    "trigger at 1417240123 (80 days outside)"
Korrekt:   "Trigger 1411261107.984 liegt innerhalb [1411260416, 1411264512]"
Ursache:   Windsurf/Agent-Artefakt (GPS/Unix-Time-Konfusion?)
Impact:    Löste Panik aus, führte zu "alles stoppen"
```

### Fund 2: Falscher Trigger in Execution-Report

```
Datei:     FINAL_EXECUTION_REPORT.md, Zeilen 41-44
Falsch:    "GW240925 trigger at GPS ~1417240123"
           "Delta: ~6,979,707 seconds = ~69.2 days"
Korrekt:   "Trigger 1411261107.984 im HDF5-Fenster"
Impact:    Falsche Schlussfolgerung: "Neue GWOSC-Dateien nötig"
```

### Fund 3: Falsche Testzahlen in README

```
Datei:     README.md, Zeile 239
Falsch:    "497 PASS  |  1 xfail  |  0 fail"
Echt:      123 PASS, 52 FAIL, 1 XFAIL (PYTEST_FULL_RUN_REPORT.md)
Ursache:   Entweder alter Stand oder Windsurf-Fehler
Impact:    Public-facing — Reputationsrisiko bei unkorrigierter Veröffentlichung
```

---

**Ende des Complete Project Reports. Nächster Schritt: Lino sichtet und gibt Korrekturen frei.**
