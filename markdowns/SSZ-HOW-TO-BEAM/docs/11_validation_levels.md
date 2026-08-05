# BEAM-SSZ Validation Levels

BEAM-SSZ is a candidate rejection and classification framework.
A candidate is never accepted merely because it shortens an effective distance.
It must pass:

1. canonical Xi/regime checks,
2. method-assignment checks,
3. finite metric checks,
4. timelike worldline normalization,
5. geodesic accessibility checks,
6. tidal/geodesic-deviation bounds,
7. causal checks,
8. energy-condition classification.

Candidate status labels:

- `PASS_TO_NEXT_STAGE`: mathematically interesting within current validators.
- `HOLD`: incomplete; needs tensor-level validation.
- `REJECT`: violates a hard guardrail.
