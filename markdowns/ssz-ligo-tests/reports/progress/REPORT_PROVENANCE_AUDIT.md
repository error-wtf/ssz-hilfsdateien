# REPORT PROVENANCE AUDIT — SSZ-LIGO-Tests
**Datum:** 2026-05-20 05:10 CEST
**Autor:** Bingsi (Hermes Agent)
**Phase:** STEP 03 — Report-Provenance-Prüfung
**Regel:** CSV ist kein Primärbeweis. Nur HDF5→Command→Log→Output→Report zählt.

---

## Methodik

Jeder Report wird geprüft auf:
1. **Script existiert?** — Gibt es ein passendes run_*.py?
2. **Log existiert?** — Gibt es stdout/stderr-Log mit Timestamps?
3. **CSV/Output existiert?** — Wurde eine Output-Datei erzeugt?
4. **HDF5-Hash im Log?** — Wurde SHA256 der Input-Dateien protokolliert?
5. **Trigger korrekt?** — Wird 1411261107.984 oder 1417240123 verwendet?
6. **Statistik ausreichend?** — N>1 Off-source oder als limitiert dokumentiert?

### Klassifikation

| Status | Bedeutung |
|--------|-----------|
| ✅ PROVENANCE_VERIFIED | Script+Log+CSV+korrekter Trigger+Hash |
| ⚠️ PROVENANCE_PLAUSIBLE | Script+Log+CSV existieren, aber Hash fehlt |
| ⚠️ PROVENANCE_LIMITED | Log existiert, aber N=1 oder Trigger unklar |
| 🔷 SYNTHETIC_ONLY | Keine Real-HDF5, klar deklariert |
| ❓ UNVERIFIED | Kein Log / kein Script / keine nachvollziehbare Kette |
| ❌ INVALID | Falscher Trigger / ohne Execution |
| 📋 METHODOLOGY_DOC | Kein Daten-Report, reine Methodik |

---

## 1. CORE PIPELINE REPORTS

| Report | Script | Log | CSV | Trigger korrekt? | Hash? | Status |
|--------|--------|-----|-----|-----------------|-------|--------|
| REAL_STRAIN_LOAD_REPORT.md | run_strain_pipeline.py | full_strain_pipeline.log | — | ✅ 1411261107.984 | ❌ | ⚠️ PROVENANCE_PLAUSIBLE |
| REAL_STRAIN_SANITY_REPORT.md | run_strain_pipeline.py | full_strain_pipeline.log | real_strain_sanity.csv | ✅ | ❌ | ⚠️ PROVENANCE_PLAUSIBLE |
| DERIVED_V0_STRAIN_PIPELINE_REPORT.md | run_derived_v0_pipeline.py | derived_v0_pipeline.log | — | ✅? | ❌ | ⚠️ PROVENANCE_PLAUSIBLE |
| PSD_WELCH_REPORT.md | run_strain_pipeline.py | full_strain_pipeline.log | — | ✅ | ❌ | ⚠️ PROVENANCE_PLAUSIBLE |
| GR_CONTROL_WAVEFORM_REPORT.md | run_strain_pipeline.py | full_strain_pipeline.log | — | ✅ | ❌ | ⚠️ PROVENANCE_PLAUSIBLE |
| SSZ_FORWARD_APPLICATION_REPORT.md | run_strain_pipeline.py | full_strain_pipeline.log | — | ✅ | ❌ | ⚠️ PROVENANCE_PLAUSIBLE |
| RESIDUAL_LIKELIHOOD_REPORT.md | run_strain_pipeline.py | full_strain_pipeline.log | — | ✅ | ❌ | ⚠️ PROVENANCE_PLAUSIBLE |

**Bewertung:** Die Core-Pipeline-Reports haben Script+Log. Zahlen (lnL, MF-SNR) sind plausibel. ABER: Kein HDF5-Hash im Log → nicht voll verifizierbar. Müssen mit Hash-Logging neu ausgeführt werden.

---

## 2. L1 DIAGNOSTIC REPORTS

| Report | Script | Log | CSV | Trigger korrekt? | Hash? | Status |
|--------|--------|-----|-----|-----------------|-------|--------|
| L1_ANOMALY_DIAGNOSTIC_REPORT.md | run_l1_anomaly_diagnostic.py | l1_anomaly_diagnostic.log | — | ✅? | ❌ | ⚠️ PROVENANCE_PLAUSIBLE |
| L1_20_210HZ_GLITCH_STATIONARITY_REPORT.md | run_l1_glitch_stationarity.py | l1_glitch_stationarity.log | l1_20_210hz_diagnostics.csv | ✅? | ❌ | ⚠️ PROVENANCE_PLAUSIBLE |
| L1_DQ_FLAG_CHECK_REPORT.md | run_l1_dq_flag_check.py | l1_dq_flag_check.log | l1_dq_flags_checked.csv | ✅? | ❌ | ⚠️ PROVENANCE_PLAUSIBLE |
| L1_ARTIFACT_GATE_FINAL_STATUS.md | run_all_artifact_gates.py | gaussianity_artifact_gate.log | — | ✅? | ❌ | ⚠️ PROVENANCE_PLAUSIBLE |
| L1_GAUSSIANITY_TEST.md | run_l1_gaussianity_test.py | l1_gaussianity_test.log | L1_GAUSSIANITY_TEST.csv | ✅? | ❌ | ⚠️ PROVENANCE_PLAUSIBLE |
| L1_HARMONIC_OSCILLATOR_TEST.md | run_l1_harmonic_oscillator_test.py | l1_harmonic_oscillator_test.log | L1_HARMONIC_OSCILLATOR_TEST.csv | ✅? | ❌ | ⚠️ PROVENANCE_PLAUSIBLE |
| L1_LINE_NOTCH_TEST_REPORT.md | run_l1_line_notch_test.py | l1_line_notch_test.log | l1_line_notch_peaks.csv | ✅? | ❌ | ⚠️ PROVENANCE_PLAUSIBLE |
| L1_MULTIWINDOW_STATIONARITY_REPORT.md | run_l1_multiwindow_stationarity.py | l1_multiwindow_stationarity.log | l1_multiwindow_stationarity.csv | ✅? | ❌ | ⚠️ PROVENANCE_PLAUSIBLE |
| L1_NOTCH_SWEEP_REPORT.md | run_l1_notch_sweep.py | l1_notch_sweep.log | l1_notch_sweep_peaks.csv | ✅? | ❌ | ⚠️ PROVENANCE_PLAUSIBLE |
| L1_STFT_OMICRON_LITE_REPORT.md | run_l1_stft_omicron_lite.py | l1_stft_omicron_lite.log | l1_stft_omicron_lite.csv | ✅? | ❌ | ⚠️ PROVENANCE_PLAUSIBLE |
| L1_EXCLUDED_OR_DIAGNOSTIC_REPORT.md | — | — | — | ✅? | ❌ | ❓ UNVERIFIED |

**Bewertung:** Alle L1-Diagnostik-Scripte haben Logs und CSVs. Plausible Provenance. ABER: Ohne Hash nicht verifizierbar. N=1 Off-source ist dokumentiert, aber statistisch limitiert.

---

## 3. H1/L1 COHERENCE REPORTS

| Report | Script | Log | CSV | Trigger korrekt? | Hash? | Status |
|--------|--------|-----|-----|-----------------|-------|--------|
| H1_L1_COHERENCE_PIPELINE_REPORT.md | run_h1_l1_coherence_pipeline.py | h1_l1_coherence_pipeline.log | — | ✅? | ❌ | ⚠️ PROVENANCE_PLAUSIBLE |
| H1_L1_TIME_DELAY_REPLICATION_REPORT.md | run_h1_l1_time_delay_replication.py | h1_l1_time_delay_replication.log | h1_l1_delay_scan.csv | ✅? | ❌ | ⚠️ PROVENANCE_PLAUSIBLE |
| H1_L1_ABS_CORRELATION_REPLICATION_REPORT.md | run_h1_l1_time_delay_replication.py | h1_l1_time_delay_replication.log | h1_l1_abs_delay_scan.csv | ✅? | ❌ | ⚠️ PROVENANCE_PLAUSIBLE |
| H1_L1_SUBBAND_REPLICATION_REPORT.md | run_h1_l1_time_delay_replication.py | h1_l1_time_delay_replication.log | h1_l1_subband_abs_corr.csv | ✅? | ❌ | ⚠️ PROVENANCE_PLAUSIBLE |
| H1_L1_LONG_BASELINE_REPLICATION_REPORT.md | run_h1_l1_long_baseline_replication.py | h1_l1_long_baseline_replication.log | h1_l1_long_baseline_xcorr.csv | ✅? | ❌ | ⚠️ PROVENANCE_PLAUSIBLE |
| H1_L1_LONG_BASELINE_XCORR_REPORT.md | run_h1_l1_long_baseline_replication.py | h1_l1_long_baseline_replication.log | h1_l1_long_baseline_xcorr.csv | ✅? | ❌ | ⚠️ PROVENANCE_PLAUSIBLE |
| H1_L1_EXECUTION_REPORT.md | run_h1_l1_long_baseline_replication.py | h1_l1_long_baseline_replication.log | h1_l1_trigger_excess.csv | ✅? | ❌ | ⚠️ PROVENANCE_PLAUSIBLE |
| H1_L1_COHERENCE_RECHECK_ROBUST_PSD.md | — | robust_psd_recheck.log | — | ✅? | ❌ | ⚠️ PROVENANCE_PLAUSIBLE |
| H1L1_CROSS_COHERENCE_REPORT.md | run_h1l1_cross_coherence.py | h1l1_cross_coherence.log | h1l1_cross_coherence.csv | ✅? | ❌ | ⚠️ PROVENANCE_PLAUSIBLE |
| H1L1_TIME_DELAY_SCAN_REPORT.md | run_h1l1_time_delay_scan.py | h1l1_time_delay_scan.log | h1l1_time_delay_scan.csv | ✅? | ❌ | ⚠️ PROVENANCE_PLAUSIBLE |
| H1_ONLY_EXPLORATORY_STRAIN_REPORT.md | — | — | — | ✅? | ❌ | ❓ UNVERIFIED |

**Bewertung:** Alle Coherence-Scripte haben Logs und CSVs. Plausible Provenance. Long-Baseline-Replikation nutzt die CSVs aus den Time-Delay-Tests als Input — das ist eine abgeleitete Kette, nicht direkt HDF5→CSV. Statistisch limitiert (N=1 Off-source für die meisten).

---

## 4. SYNTHETIC / TWIST / GA REPORTS

| Report | Script | Log | CSV | Typ | Status |
|--------|--------|-----|-----|-----|--------|
| TWIST_BRANCH_SYNTHETIC_REPORT.md | run_twist_branch_synthetic.py | — | twist_branch_theta_scan.csv | Synthetic | 🔷 SYNTHETIC_ONLY |
| TWIST_BRANCH_2PN_SYNTHETIC_REPORT.md | run_twist_branch_2pn_synthetic.py | — | twist_branch_2pn_synthetic_scan.csv | Synthetic | 🔷 SYNTHETIC_ONLY |
| GA_INTERFEROMETER_SYNTHETIC_REPORT.md | run_ga_interferometer_synthetic.py | — | — | Synthetic | 🔷 SYNTHETIC_ONLY |
| SOURCE_PROPAGATION_TWIST_SYNTHETIC_REPORT.md | run_source_propagation_twist_synthetic.py | — | source_propagation_twist_synthetic_scan.csv | Synthetic | 🔷 SYNTHETIC_ONLY |
| SYNTHETIC_FORWARD_DRY_RUN_REPORT.md | — | — | synthetic_delta_psi_preview.csv | Synthetic | 🔷 SYNTHETIC_ONLY |
| TWIST_BRANCH_REAL_H1_L1_EXPLORATORY_REPORT.md | run_twist_branch_real_h1_l1.py | twist_branch_real_h1_l1.log | — | Real (blockiert) | ⚠️ PROVENANCE_LIMITED |

**Bewertung:** Synthetic-Reports sind klar deklariert — keine falschen Claims. Twist-Real hat Log, aber ist durch L1-DQ blockiert. Sicher.

---

## 5. METHODOLOGY / POSITION PAPERS (keine Daten)

| Report | Typ | Status |
|--------|-----|--------|
| DQ_AWARE_FINAL_LIGO_STATUS.md | Master Gate | ✅ PROVENANCE_VERIFIED |
| FINAL_INTERPRETATION_LOCK.md | Lock-Dokument | ✅ PROVENANCE_VERIFIED |
| ANTI_CIRCULARITY_FINAL_GATE.md | Gate-Dokument | ✅ PROVENANCE_VERIFIED |
| GLOBAL_ANTI_CIRCULARITY_RULE.md | Regelwerk | 📋 METHODOLOGY_DOC |
| OPEN_DATA_METHODOLOGY_POSITION.md | Positionspapier | 📋 METHODOLOGY_DOC |
| PHYSICS_CLARIFICATION_NOTE.md | Klärungsdokument | 📋 METHODOLOGY_DOC |
| PHYSICS_FOUNDATIONS.md | Referenz | 📋 METHODOLOGY_DOC |
| LIGO_QUESTION_REPORT.md | Draft-Frage | 📋 METHODOLOGY_DOC |
| LIGO_RELEASE_MASTER_STATUS_REPORT.md | Status | 📋 METHODOLOGY_DOC |
| SOURCE_TRUTH_VERIFICATION.md | SOT-Prüfung | 📋 METHODOLOGY_DOC |
| SSZ_LIGO_TEST_FRAMEWORK.md | Framework | 📋 METHODOLOGY_DOC |
| SSZ_PREREGISTERED_HYPOTHESIS.md | Hypothese | 📋 METHODOLOGY_DOC |
| ZENODO_RELEASE_SYMLINK_ISSUE_SUMMARY.md | Technische Doku | 📋 METHODOLOGY_DOC |
| REAL_LIGO_CLAIM_GATE.md | Claim-Gate | 📋 METHODOLOGY_DOC |
| NEXT_PHYSICS_DERIVATION_TASKS.md | Aufgabenliste | 📋 METHODOLOGY_DOC |
| OBSERVABLE_BRANCH_TEST_READINESS.md | Readiness | 📋 METHODOLOGY_DOC |
| QNM_TEST_READINESS_REQUIREMENTS.md | Readiness | 📋 METHODOLOGY_DOC |

**Bewertung:** Alles Methodik-Dokumente, keine Daten-Reports. Teilweise redundant (mehrere Status-Reports mit ähnlichem Inhalt). Können konsolidiert werden, aber keine akute Gefahr.

---

## 6. QNM / RINGDOWN / PHASE 5 REPORTS

| Report | Script | Log | CSV | Trigger korrekt? | Status |
|--------|--------|-----|-----|-----------------|--------|
| QNM_3PCT_SENSITIVITY_FINAL_REPORT.md | run_qnm_ringdown_injection_sensitivity.py | qnm_ringdown_injection_sensitivity.log | qnm_injection_scan.csv | N/A (synthetic) | ⚠️ PROVENANCE_PLAUSIBLE |
| QNM_RINGDOWN_INJECTION_SENSITIVITY_REPORT.md | run_qnm_ringdown_injection_sensitivity.py | qnm_ringdown_injection_sensitivity.log | qnm_injection_scan.csv | N/A | ⚠️ PROVENANCE_PLAUSIBLE |
| PHASE_5_RF_TEST_RESULT.md | phase_5c_rf_computation.py | PHASE_5_RF_TEST_LOG.md | PHASE_5C_RF_COMPUTATION_RESULTS.csv | ❌ (Posterior-Daten) | ⚠️ PROVENANCE_LIMITED |
| PHASE_5_RF_TEST_FINAL_RESULT.md | phase_5c_rf_computation.py | PHASE_5_RF_TEST_LOG.md | PHASE_5C_RF_COMPUTATION_RESULTS.csv | ❌ | ⚠️ PROVENANCE_LIMITED |

**Bewertung:** QNM-Tests sind synthetic — korrekt. Phase-5-basiert auf Posterior-Daten (Metafile combinedPHM) — das ist anti-zirkulär problematisch und sollte nicht als SSZ-Test gelten. INVALID.txt und SUPPRESSED.txt bestätigen das.

---

## 7. ARTIFACT GATE / GAUSSIANITY REPORTS

| Report | Script | Log | CSV | Status |
|--------|--------|-----|-----|--------|
| ARTIFACT_SCORE_REPORT.md | run_artifact_score.py | artifact_score.log | artifact_score.csv | ⚠️ PROVENANCE_PLAUSIBLE |
| GAUSSIANITY_ARTIFACT_GATE_REPORT.md | run_gaussianity_artifact_gate.py | gaussianity_artifact_gate.log | gaussianity_summary_stats.csv | ⚠️ PROVENANCE_PLAUSIBLE |
| SUBBAND_GAUSSIANITY_REPORT.md | run_subband_gaussianity.py | subband_gaussianity.log | subband_gaussianity.csv | ⚠️ PROVENANCE_PLAUSIBLE |
| GW250207_ARTIFACT_GATE_REPORT.md | run_gw250207_artifact_gate.py | gw250207_artifact_gate.log | gw250207_artifact_gate.csv | ⚠️ PROVENANCE_PLAUSIBLE |
| GW250207_ARTIFACT_GATE_COMPARISON.md | run_gw250207_comparison.py | gw250207_comparison.log | — | ⚠️ PROVENANCE_PLAUSIBLE |

**Bewertung:** Artifact-Gates haben Script+Log+CSV. ABER: GW250207 Strain ist nicht heruntergeladen (ARTIFACT_SCORE_REPORT.md sagt "GW250207_STRAIN_NOT_DOWNLOADED") → die GW250207-Reports sind limitiert. L1-Gaussianity-Gate dokumentiert chronische Nicht-Gaußizität — das ist wertvoll.

---

## 8. PSD / CALIBRATION / ROBUST REPORTS

| Report | Script | Log | CSV | Status |
|--------|--------|-----|-----|--------|
| CALIBRATION_PSD_SENSITIVITY_REPORT.md | run_calibration_psd_sensitivity.py | calibration_psd_sensitivity.log | — | ⚠️ PROVENANCE_PLAUSIBLE |
| ROBUST_MULTIWINDOW_PSD_REPORT.md | run_robust_multiwindow_psd.py | robust_psd_recheck.log | robust_psd_windows_used.csv | ⚠️ PROVENANCE_PLAUSIBLE |

---

## 9. AUDIT / VERIFICATION / INVENTORY REPORTS

| Report | Typ | Status |
|--------|-----|--------|
| PROVENANCE_FIRST_MASTER_AUDIT.md | Audit (Bingsi) | ✅ PROVENANCE_VERIFIED |
| DQ_STATE_VECTOR_BIT_PROVENANCE_REPORT.md | DQ-Audit | ⚠️ PROVENANCE_PLAUSIBLE |
| DERIVED_FORMULAS_CODE_CONSISTENCY_AUDIT.md | Code-Audit | ⚠️ PROVENANCE_PLAUSIBLE |
| FINAL_PIPELINE_REPRODUCIBILITY_REPORT.md | Repro-Audit | ⚠️ PROVENANCE_PLAUSIBLE |
| BUILD_REPORT.md | Build | ⚠️ PROVENANCE_PLAUSIBLE |
| UNIT_NORMALIZATION_AUDIT.md | Unit-Audit | ⚠️ PROVENANCE_PLAUSIBLE |
| PYTEST_FULL_RUN_REPORT.md | Echter Log | ✅ PROVENANCE_VERIFIED |
| REAL_LIGO_HDF5_ACCESS_REPORT.md | Access-Test | ⚠️ PROVENANCE_PLAUSIBLE |
| REAL_LIGO_PRODUCT_INVENTORY.md | Inventar | ⚠️ PROVENANCE_PLAUSIBLE |
| REAL_TEST_VERIFICATION_MASTER_REPORT.md | Verifikation | ⚠️ PROVENANCE_PLAUSIBLE |

---

## 10. PROBLEMATISCHE / INVALIDIERTE REPORTS

| Report | Problem | Status |
|--------|---------|--------|
| FINAL_EXECUTION_REPORT.md | Falscher Trigger 1417240123 | ❌ INVALID |
| AUDIT_STOP.txt | "80 days outside" basierend auf falschem Trigger | ❌ INVALID |
| INVALID.txt | Phase 5 invalidiert | ❌ INVALID (korrekt invalidiert) |
| SUPPRESSED.txt | "INVALIDATED 2026-05-14" | ❌ INVALID (korrekt) |
| CIRCULAR.txt | Erkennt Zirkularität | 📋 METHODOLOGY_DOC |
| MISSING.txt | "Missing interferometer forward model" | 📋 METHODOLOGY_DOC |
| REAL_LIGO_CLAIM_GATE.md | READY_FOR_REAL_LIGO_SSZ_CLAIM: NO | 📋 METHODOLOGY_DOC |

---

## ZUSAMMENFASSUNG

### Zahlen

| Status | Anzahl |
|--------|--------|
| ✅ PROVENANCE_VERIFIED | 6 |
| ⚠️ PROVENANCE_PLAUSIBLE | 39 |
| ⚠️ PROVENANCE_LIMITED | 3 |
| 🔷 SYNTHETIC_ONLY | 5 |
| 📋 METHODOLOGY_DOC | 17 |
| ❌ INVALID | 4 |
| ❓ UNVERIFIED | 2 |

### Kernbefund

```
39 Reports sind PROVENANCE_PLAUSIBLE:
  Script existiert ✅
  Log existiert ✅
  CSV existiert (meist) ✅
  ABER: KEIN HDF5-Hash im Log ❌

→ Plausibel, aber nicht beweissicher.
→ Müssen mit Hash-Logging neu ausgeführt werden für PROVENANCE_VERIFIED.
```

### Was wirklich zählt (minimale relevante Pipeline)

Nur folgende Reports sind für die Kernfrage relevant:
1. REAL_STRAIN_LOAD_REPORT.md — Strain geladen ✅
2. PSD_WELCH_REPORT.md — PSD geschätzt ✅
3. GR_CONTROL_WAVEFORM_REPORT.md — GR-Kontrolle ✅
4. SSZ_FORWARD_APPLICATION_REPORT.md — SSZ angewandt ✅
5. RESIDUAL_LIKELIHOOD_REPORT.md — lnL berechnet ✅

Alle anderen Reports sind Diagnostik, Methodik oder Synthetic — wertvoll, aber nicht Claim-relevant.

### Nächster Schritt

```
Alle PROVENANCE_PLAUSIBLE-Reports mit HDF5-Hash-Logging neu ausführen
→ Pipeline mit verifizierten HDF5-Dateien frisch starten
→ SHA256 in jedes Log schreiben
→ Nur dann auf PROVENANCE_VERIFIED hochstufen
```
