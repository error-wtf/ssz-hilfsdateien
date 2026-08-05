# SSZ Pre-Registered Test Hypothesis for LIGO Data

⚠️ STATUS: UNVERIFIED_DERIVED_REPORT (2026-05-20 Bingsi/Hermes) ⚠️
⚠️ HDF5→Command→Log→CSV→Report provenance chain NOT VERIFIED. ⚠️
⚠️ Do NOT cite numbers from this report without re-verification. ⚠️
⚠️ See reports/progress/REPORT_STATUS_INDEX.md for current classification. ⚠️


**Generated:** 2026-05-14  
**Status:** HYPOTHESIS REGISTERED — NOT YET TESTED  
**Purpose:** Document SSZ predictions BEFORE data analysis to prevent HARKing

---

## ⚠️ CRITICAL SCIENTIFIC PROTOCOL

This document registers **SSZ theoretical predictions** as testable hypotheses **before** any LIGO data analysis.

**What this is:**
- ✅ Pre-registered theoretical prediction from SSZ formalism
- ✅ Test target for upcoming data analysis
- ✅ Fixed benchmark for hypothesis testing

**What this is NOT:**
- ❌ Observed result from LIGO data
- ❌ Confirmed detection
- ❌ Post-hoc interpretation

---

## 1. Pre-Registered SSZ Hypotheses

### ⚠️ REQUIRED CLARIFICATION BEFORE TESTING

**Definition of R_f (fixed before analysis):**

```
R_f := f_QNM,measured / f_QNM,GR(reference)

where:

- f_QNM,measured: posterior median of observed QNM frequency from ringdown/QNM analysis
- f_QNM,GR(reference): GR-predicted QNM frequency from same event's final mass/spin posterior
- Primary mode: l=m=2, n=0 (dominant mode), unless official release documents another mode
- Confidence criterion: must account for posterior uncertainty AND calibration uncertainty
- C00/C01/envcal/cal variants: must be reported separately
- Validity condition: mode identification stable, result not dominated by calibration uncertainty
```

**Anti-HARKing Rule:**
```
Do not change R_f definition, mode choice, or thresholds after inspecting QNM/ringdown data.
Any later change must be documented as a separate exploratory analysis, not as the preregistered test.
```

---

### Hypothesis A: QNM Frequency Shift

**Source:** `ssz-complete-documentation/06_STRONG_FIELD/qnm_spectrum.md`  
**Theoretical Basis:** SSZ photon sphere radius r* = 1.387 r_s vs GR r = 1.5 r_s

**SSZ Prediction:**
```
f_QNM_SSZ / f_QNM_GR = 1 / D_SSZ(r*) ≈ 1.39

Where:
- f_QNM_GR = standard Kerr QNM frequency
- D_SSZ(r) = 1 / (1 + Ξ(r))  [SSZ dilation factor]
- r* = 1.387 r_s  [SSZ photon sphere]
- D_SSZ(r*) ≈ 0.72  [calculated value]

Therefore:
H₀: f_QNM_SSZ ≈ 1.39 × f_QNM_GR  [NULL HYPOTHESIS for SSZ]
H₁: f_QNM_observed ≈ f_QNM_GR    [Alternative: GR is correct]
```

**Testable Quantity:**
```
R_f ≡ f_QNM_measured / f_QNM_GR_predicted

If R_f ≈ 1.00 ± ε → GR consistent
If R_f ≈ 1.39 ± ε → SSZ consistent
If R_f ≠ 1.00 and ≠ 1.39 → new physics
```

**Data Status:**
| Item | Status |
|------|--------|
| SSZ prediction | ✅ Documented (39% increase) |
| LIGO data | ⏳ Not yet inspected |
| Measurement | ⏳ Not yet performed |
| Test result | ⏳ **PENDING** |

---

### Hypothesis B: QNM Damping Time Shift

**SSZ Prediction:**
```
τ_QNM_SSZ / τ_QNM_GR ≈ 1.39

[Same scaling as frequency due to D_SSZ(r*) factor]
```

**Testable Quantity:**
```
R_τ ≡ τ_QNM_measured / τ_QNM_GR_predicted

Expected:
- GR: R_τ ≈ 1.00
- SSZ: R_τ ≈ 1.39
```

**Data Status:**
| Item | Status |
|------|--------|
| SSZ prediction | ✅ Documented (39% increase) |
| LIGO data | ⏳ Not yet inspected |
| Measurement | ⏳ Not yet performed |
| Test result | ⏳ **PENDING** |

---

### Hypothesis C: Event Scaling

**SSZ Prediction:**
If SSZ is correct, the 39% shift should:
- Scale consistently between GW240925 and GW250207
- Be independent of SNR (physics, not noise)
- Be present in both Hanford and Livingston (if applicable)

**Testable:** Compare R_f across events and detectors.

**Data Status:** ⏳ **PENDING**

---

## 2. Falsification Criteria (Pre-Defined)

### Strong SSZ Falsification
```
If R_f < 1.10 at >3σ confidence:
→ SSZ QNM prediction falsified
→ SSZ would require significant revision
```

### Strong SSZ Support
```
If 1.20 < R_f < 1.60 at >3σ confidence:
→ SSZ QNM prediction supported
→ Requires independent confirmation
```

### Inconclusive
```
If 1.10 < R_f < 1.20 at any confidence:
→ Ambiguous region
→ Cannot distinguish SSZ from GR within uncertainty
→ Larger sample or better precision needed
```

---

## 3. Data Status Register

| Data Product | Extraction | Validation | Inspection | Analysis | SSZ Test |
|--------------|-----------|-----------|-----------|----------|----------|
| combined_samples.tar.gz | ⏳ Running | ⏳ Pending | ⏳ Pending | ⏳ Pending | ⏳ **NOT STARTED** |
| ringdown.tar.gz | ⏳ Running | ⏳ Pending | ⏳ Pending | ⏳ Pending | ⏳ **NOT STARTED** |
| residuals.tar.gz | ⏳ Running | ⏳ Pending | ⏳ Pending | ⏳ Pending | ⏳ **NOT STARTED** |
| tiger.tar.gz | ⏳ Running | ⏳ Pending | ⏳ Pending | ⏳ Pending | ⏳ **NOT STARTED** |

**Current Phase:** 1B (Extraction Validation — NOT YET STARTED)

---

## 4. Hypothesis vs. Data Separation

### SSZ-Hypothese (Theorie)
```
QNM-Frequenz-/Ringdown-Shift ~39% erwartet
Basierend auf: r* = 1.387 r_s, D_SSZ(r*) ≈ 0.72
Quelle: qnm_spectrum.md
Status: vorregistriert
```

### Datenbefund (Empirie)
```
noch unbekannt
LIGO-Daten noch nicht inspiziert
QNM-Posterior-Samples noch nicht geladen
```

### Test-Status
```
nicht getestet
Warte auf: Extraktion → Validation → Mapping → Analyse
```

---

## 5. Chronology Protection

### Timeline (Actual)

**2026-05-14 ~10:45 UTC:**
- SSZ Hypothesen dokumentiert (dieses Dokument)
- QNM-Vorhersagen festgelegt (39% Shift)
- LIGO-Daten noch nicht inspiziert

**Later (Pending):**
- Extraktion abschließen
- Validation durchführen
- Daten inspizieren
- Hypothesen testen

### Anti-HARKing Guarantee

**HARKing** (Hypothesizing After Results are Known) verhindert durch:
1. ✅ Zeitstempel dieses Dokuments VOR Datenanalyse
2. ✅ SSZ-Quellen zitiert (qnm_spectrum.md)
3. ✅ Falsifizierungskriterien vordefiniert
4. ✅ Datenstatus explizit als "unbekannt" markiert

---

## 6. Important Notice for Future Analysis

```
The "39% QNM shift" is a pre-analysis SSZ hypothesis, 
not an observed result.

DO NOT describe it as:
- found
- detected
- confirmed
- suggested by the LIGO data
- observed in the posteriors

ONLY use it later as:
- a fixed test target
- after extraction validation
- after science mapping
- after reproduction checks
- in formal hypothesis testing
```

---

## 7. Next Steps (Conditional)

```
IF Phase 1B Validation = PASS:
   → Phase 2 Science Mapping
   → HDF5 Struktur lesen (nur Metadaten)
   → QNM/Ringdown-Dateien zuordnen
   → Notebook-Abhängigkeiten prüfen

IF Phase 1B Validation = FAIL:
   → Reparatur/Re-Extraktion
   → Keine Analyse bis Daten sauber

IF later analysis shows R_f ≈ 1.39:
   → SSZ hypothesis supported (NOT confirmed)
   → Requires independent replication
   → Cross-check with other predictions

IF later analysis shows R_f ≈ 1.00:
   → SSZ QNM prediction falsified
   → Re-evaluate strong-field formalism
```

---

## Document Integrity

**Hash:** [to be computed after finalization]  
**Signed:** 2026-05-14  
**Status:** PRE-REGISTRATION COMPLETE  
**Awaiting:** Data extraction and validation

---

*Dieses Dokument dient als wissenschaftliche Zeitkapsel: Die Hypothese ist festgelegt, bevor die Daten gesehen werden.*
