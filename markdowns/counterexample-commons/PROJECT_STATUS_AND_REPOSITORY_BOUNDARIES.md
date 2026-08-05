# counterexample-commons — Project Status and Repository Boundaries

**Date:** 2026-05-23 | **Purpose:** Project identity and boundary documentation

---

## 1. Projektidentität

**Projektpfad:** `E:\clone\counterexample-commons\`
**Projektstatus:** Eigenständiges Projekt / eigenständige Repository-Grenze
**Nicht zugehörig zu:** `E:\clone\book-full\` und der SSZ-Buchperfektionierung

**Beschreibung (aus README.md):**
Counterexample Commons is a source-available research laboratory for exact
mathematical validation and controlled AI-assisted exploration. Its first case
study examines the 2026 AI-generated counterexample to Paul Erdős' planar
unit-distance conjecture (Will Sawin's n^{1.014} exponent result).

**Lizenz:** Anti-Capitalist Software License (v 1.4)
**Autor:** Lino Casu
**Python:** >=3.11
**Dependencies:** sympy, numpy, matplotlib, gradio

---

## 2. Nachgewiesene Projektbestandteile

| Bereich | Nachgewiesene Dateien/Ordner | Zweck | Status |
|---------|------------------------------|-------|--------|
| Python-Paket | `counterexample_commons/` | Hauptmodul | Vorhanden |
| App/UI | `app/` | Gradio-Oberfläche | Vorhanden |
| AI Lab | `ai_lab/` | KI-gestützte Exploration | Vorhanden |
| Notebooks | `notebooks/` | Jupyter-Notebooks | Vorhanden |
| Colab | `colab/` | Google Colab Integration | Vorhanden |
| Tests | `tests/` | pytest-Tests | Vorhanden |
| Case Studies | `case_studies/` | Fallstudien | Vorhanden |
| Docs | `docs/` | Dokumentation | Vorhanden |
| Reports | `reports/` | Berichte | Vorhanden |
| Scripts | `scripts/` | Hilfsskripte | Vorhanden |
| Branding | `branding/` | Projektvisualisierung | Vorhanden |
| Deployment | `deployment/` | Deployment-Konfiguration | Vorhanden |
| References | `references/` | Literaturquellen | Vorhanden |
| CI/CD | `.github/` | GitHub Actions/Workflows | Vorhanden |
| Manifest | `pyproject.toml` | Build-Konfiguration (v0.1.0) | Vorhanden |
| README | `README.md` | Projektbeschreibung (5.7 KB) | Vorhanden |
| Requirements | `requirements.txt` | Abhängigkeiten | Vorhanden |
| Changelog | `CHANGELOG.md` | Versionshistorie | Vorhanden |
| Citation | `CITATION.cff` | Zitierhinweis | Vorhanden |
| License | `LICENSE` + `LICENSE_POLICY.md` | ACSL v1.4 | Vorhanden |
| Third Party | `THIRD_PARTY_SOURCES_AND_LICENSES.md` | Drittanbieter | Vorhanden |
| Zenodo | `.zenodo.json` | Archivierungs-Metadaten | Vorhanden |

---

## 3. Aktueller Git-Status

```
GIT DETECTED: NO
REPOSITORY ROOT: N/A (.git directory not found)
CURRENT BRANCH: N/A
REMOTES: N/A
WORKING TREE STATUS: N/A — no Git repository initialized locally
```

Git wurde NICHT initialisiert. Kein `git init` durchgeführt.

---

## 4. Aktueller Arbeits- und Funktionsstand

Anhand der vorhandenen Dateien belegbar:

- **Hauptpaket:** `counterexample_commons/` — Python-Paket (setuptools, v0.1.0)
- **Forschungsgegenstand:** Erdős' Unit-Distance-Vermutung, Sawin-Counterexample (n^{1.014})
- **UI:** Gradio-basierte Oberfläche in `app/`
- **Tests:** pytest-konfiguriert in `tests/`
- **Methodik:** Trennung von source-documented results, locally reproduced calculations, exploratory candidates, rejected experiments
- **Lizenz:** Anti-Capitalist Software License v1.4

Keine Ausführung, keine Tests gestartet, keine Pipelines aktiviert.

---

## 5. Offene Punkte

| Priorität | Aufgabe/Problem | Evidenzdatei | Nächster sicherer Schritt |
|-----------|-----------------|--------------|---------------------------|
| Mittel | Git-Repository initialisieren | `.git` fehlt | Autor entscheidet |
| Mittel | Tests ausführen und Status dokumentieren | `tests/` vorhanden | `pytest` in eigenem CC-Auftrag; Git-Init unabhängig davon nur nach Autorenentscheidung |
| Niedrig | Gradio-App testen | `app/` vorhanden | Lokaler Start |

---

## 6. Repository-Grenzen

```
THIS PROJECT:
E:\clone\counterexample-commons\

EXTERNAL, SEPARATE PROJECT:
E:\clone\book-full\

BOUNDARY RULE:
Dateien, Reports, Tests, Buildartefakte und Commits dieses Projekts bleiben
innerhalb von counterexample-commons. SSZ-Buchdateien, Übersetzungen,
Formelregistries und Buch-PDFs gehören ausschließlich zu book-full und dürfen
hier nicht abgelegt werden.

Umgekehrt dürfen SSZ-Buchaudits, PDF-Builds und Formelprüfungen keine
Artefakte aus oder in counterexample-commons verwenden oder ablegen.
```

---

## 7. Zulässige Folgearbeiten

Nur Aufgaben, die zu counterexample-commons selbst gehören:

1. Git-Repository initialisieren (nach Autorenentscheidung)
2. Tests ausführen und Ergebnisse dokumentieren
3. Gradio-App lokal testen
4. Case Studies vervollständigen
5. Dokumentation in `docs/` erweitern
6. CI/CD in `.github/` konfigurieren

Keine SSZ-Buch- oder PDF-Aufgaben.
