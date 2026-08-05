# UI Scientific Integrity Policy

## Core principles

1. The UI **cannot** promote hypotheses to proofs.
2. Exact finite validation of a specific point set is **not** an asymptotic theorem.
3. Documented external theorem claims remain `SOURCE_DOCUMENTED` unless
   separately reproduced and reviewed.
4. AI-generated candidates are labelled `AI_GENERATED_HYPOTHESIS` until
   independently validated.
5. Failed or rejected experiments are preserved, not hidden.

## Status hierarchy

| Status | UI Display | Meaning |
|--------|-----------|---------|
| SOURCE_DOCUMENTED | 📄 | Analysed from primary sources; not independently reproduced |
| LOCALLY_REPRODUCED_EXACT | ✅ | Verified by local exact arithmetic |
| LOCALLY_REPRODUCED_NUMERICAL | ≈ | Verified by local floating-point computation |
| AI_GENERATED_HYPOTHESIS | 🤖 | Model output; requires independent validation |
| FORMALLY_VERIFIED | 🔒 | Machine-checked proof (e.g. Lean 4) |
| REJECTED_OR_FAILED | ❌ | Attempted and failed; preserved for transparency |
| INCONCLUSIVE | ❓ | Validation attempted; result indeterminate |

## Prohibited UI language

- "AI solved mathematics"
- "AI proved the theorem"
- "Verified proof" (unless FORMALLY_VERIFIED)
- "Breakthrough confirmed" (for locally reproduced finite results)
