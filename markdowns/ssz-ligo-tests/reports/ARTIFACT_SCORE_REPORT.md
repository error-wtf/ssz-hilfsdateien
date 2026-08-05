# Artifact Score — GW240925
Generated: 2026-05-19 08:11:34

## Score Components

| Component | Score | Value | Category |
|-----------|-------|-------|----------|
| L1/H1 bandpower ratio | 2 | 1.5639 | elevated |
| L1 stationarity quantile | 0 | 74.5000 | clean |
| L1 line fraction | 0 | 0.0465 | clean |
| L1 20-40Hz excess kurtosis | 3 | 44.8567 | high_risk |
| H1/L1 coherence | 2 | 0.0561 | elevated |
| Cross-phase stability R | 0 | 0.9115 | clean |
| Phase-rand BP quantile | 0 | 0.0000 | clean |
| DQ status | 3 | DQ_UNRESOLVED | high_risk |

**Total: 10 / 24**  (of max 24)

## ARTIFACT_RISK: MEDIUM

| Risk Level | Score Range |
|------------|-------------|
| LOW        | 0-4         |
| MEDIUM     | 5-10        |
| HIGH       | 11-17       |
| CRITICAL   | 18-24       |

## Claim Gate

**CLAIM_ALLOWED: NO**

**Blockers:**
- L1_DQ_UNRESOLVED: DQ_UNRESOLVED
- OMICRON_IDQ_NOT_AVAILABLE
- GW250207_STRAIN_NOT_DOWNLOADED

## Hardcoded Gate
```
READY_FOR_REAL_LIGO_SSZ_CLAIM: NO
Requires: Omicron/iDQ + DQ pass + ARTIFACT_RISK: LOW
          + manual review + external confirmation
```

## Anti-Circularity
- No SSZ parameters used
- SSZ_SUPPORT_CLAIM_MADE: NO
- SSZ_FALSIFICATION_CLAIM_MADE: NO
