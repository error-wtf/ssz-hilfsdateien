# SSZ-LIGO Test Suite — Current Status

**Version:** 0.5.0  
**Date:** 2026-05-19  
**Data:** GW240925 O4b — GWOSC [https://zenodo.org/records/18600070](https://zenodo.org/records/18600070)

---

## Overall Status

```
PIPELINE_STATUS:               PASS_EXPLORATORY
CODE_DOC_CONSISTENCY:          PASS (5/5)
READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
SSZ_SUPPORT_CLAIM_MADE:        NO
SSZ_FALSIFICATION_CLAIM_MADE:  NO
```

---

## Formula Status

| Formula | Status | Since |
|---------|--------|-------|
| Xi_weak, Xi_strong, D, s | LOCKED | 2026-05-14 |
| rdot_SSZ = rdot_GR·D²/s⁴ | LOCKED (Ch.31) | 2026-05-14 |
| delta_psi_SSZ(f) | DERIVED_V1_INSPIRAL_0PN_LOCKED | 2026-05-18 |
| delta_a_SSZ(f) | DERIVED_V0_PROXY | 2026-05-18 |
| h_SSZ(f) | DERIVED_V0_PROXY | 2026-05-18 |
| epsilon_220 | BLOCKED_BRANCH_CONFLICT | 2026-05-14 |

---

## Pipeline Run Results (H1, 20–210 Hz, GW240925)

| Metric | Value |
|--------|-------|
| lnL_GR | −3.24×10⁷ |
| lnL_SSZ | −3.24×10⁷ |
| delta_lnL | +5.3×10⁻⁶ |
| MF-SNR GR | 44.2 |
| SSZ_EFFECT_ABOVE_CALIBRATION | YES (6.3e-06 > cal_spread 7.1e-08) |

---

## Test Coverage

| Test file | Status |
|-----------|--------|
| test_derived_delta_psi_v0.py | ✅ PASS |
| test_derived_delta_a_v0.py | ✅ PASS |
| test_h_ssz_v0_waveform_application.py | ✅ PASS |
| test_epsilon_220_branch_registry.py | ✅ PASS |
| test_xi_strong_branch_lock.py | ✅ PASS |
| test_08_anti_circularity.py | ✅ PASS |
| run_h1_l1_time_delay_replication.py | ✅ RAN — TRIGGER_SPECIFIC: NO (persistent systematic) |
| run_detector_parity_test.py | ✅ RAN — DETECTOR_PARITY: YES |
| run_offsource_background_test.py | ✅ RAN — L1_TRIGGER_SPECIFIC: NO, L1_PERSISTENT_NOISE: YES |

---

## Artifact Gate Summary (GW240925)

```
Unit/Normalization Audit:          7/7 PASS
PSD normalization:                 CORRECT
Bandpower values:                  TRUSTWORTHY
Artifact score:                    10/24 (MEDIUM)
Claim gate verdict:                NO

H1 status:                         USABLE_EXPLORATORY
L1 status:                         DIAGNOSTIC_ONLY
  L1 20-40 Hz trigger ex_kurtosis: +44.9  (off-source: +1.1)  delta=+43.7
  L1 excess class:                 TRIGGER_SPECIFIC_LOW_FREQ_SUBBAND
  Trigger-specific burst:          NO
  Lines explain part:              YES (~55% bandpower in lines)
  Broadband remainder:             YES
H1/L1 coherence:                   BLOCKED (L1 DQ unresolved)
```

---

## Open Blockers

**Not solvable by local code — require external data or DQ clarification:**

1. **GW250207 strain**: O4c event not yet in public GWOSC release → download when available, run full artifact gate
2. **L1 DQ clarification**: offline Omicron/iDQ/line/AUX context needed to classify L1 20-40 Hz excess
3. **LIGO DQ question**: formal inquiry to LIGO/DQ team with concise question (see LIGO_QUESTION_REPORT.md)

**Solvable internally when physics is ready:**

4. **delta_psi**: 0PN only → need 3.5PN r(f) for real inspiral claim
5. **epsilon_220**: 3 conflicting branches (3%/31%/39%), all different observables — needs author resolution
6. **GR control**: 0PN only → needs matched 3.5PN when delta_psi is upgraded
7. **Detector propagation**: RSG phase not included in current forward model
8. **Injection-Recovery**: defer until clean template and injection setup confirmed

---

## Reports

| Report | Date |
|--------|------|
| DERIVED_FORMULAS_CODE_CONSISTENCY_AUDIT.md | 2026-05-18 |
| H1_L1_COHERENCE_PIPELINE_REPORT.md | 2026-05-18 |
| CALIBRATION_PSD_SENSITIVITY_REPORT.md | 2026-05-18 |
| FINAL_INTERPRETATION_LOCK.md | 2026-05-18 |
| ANTI_CIRCULARITY_FINAL_GATE.md | 2026-05-18 |
| L1_ARTIFACT_GATE_FINAL_STATUS.md | 2026-05-19 |
| LIGO_QUESTION_REPORT.md | 2026-05-19 |
| PHYSICS_CLARIFICATION_NOTE.md | 2026-05-19 |
| OPEN_DATA_METHODOLOGY_POSITION.md | 2026-05-19 |
| H1_L1_TIME_DELAY_REPLICATION_REPORT.md | 2026-05-19 |
