# SSZ Consolidation & Peer-Review Roadmap (Updated)

**Status:** CANONICAL NORTH STAR DIRECTIVE (P0/P1)  
**Location:** `/home/error/physics/hilfsdateien/PEER_REVIEW_CONSOLIDATION_PLAN.md`

This document resolves the critical mathematical, logical, and epistemological inconsistencies identified during the extensive external audits. It establishes the absolute single source of truth for the Segmented Spacetime (SSZ) framework moving forward.

---

## 1. Official Scientific Positioning

*Der vollständige SSZ-Testlauf zeigt eine robuste interne Validierung der Implementierung: 25/25 Test-Suites bestehen, PPN-Grenzen werden exakt reproduziert, die Dual-Velocity-Invariante hält numerisch, und die Blend-Zone ist C2-glatt getestet. Die empirische Redshift-Analyse zeigt jedoch keine globale Signifikanz, sondern eine klare Regime-Struktur: starke Performance im Photon-Sphere- und High-Velocity-Bereich, aber Versagen sehr nahe am Horizont. Der aktuelle Status ist daher nicht „bewiesen“, sondern „intern stark validiert und mit klaren offenen externen Tests versehen“.*

**Mantra:** 
> "Weak Field is the entry ticket. Strong Field is the tribunal."

---

## 2. Four-Tier Scientific Stance (The "No Overclaiming" Rule)

All future documentation, papers, and repositories must categorize their claims strictly according to this four-tier system:

| Category | Scientific Status | Permitted Language |
| :--- | :--- | :--- |
| **1. Unit-/Implementation Tests** | **SEHR STARK** | "Numerically verified to machine precision", "Analytically continuous" (e.g. C1/C2 bounds). |
| **2. Weak-Field GR Compatibility** | **STARK** | "Reproduces GR PPN limits exactly", "Fully compatible with weak-field observations". |
| **3. Regime-Redshift Performance** | **INTERESSANT / GEMISCHT** | "Shows dominant performance in photon-sphere regime", "Fails closely at horizon ($r < 2r_s$)". |
| **4. Hawking/Singularity/LIGO** | **VORBEREITET / OFFEN** | "Framework is ready for tests", "Pending explicit observational data", "Requires independent external confirmation". |

**Banned Terminology:** "internally validated", "robust numerical validation", "requires further experimental validation", "SSZ offers a regularized non-singular horizon model", "Hawking radiation model prepared".  
**Required Replacements:** "internally numerically validated", "regime-dependent support", "framework-ready", "pending external confirmation".

---

## 3. Priority 1 Critical Bugs (The $\Xi$ Asymptotic Inconsistency)

A critical mathematical vulnerability has been identified and purged across the documentation:

*   **The Absolute Canon (OPERATIONAL):**
    $$\Xi_{\text{strong}}(r) = 1 - e^{-\varphi \frac{r_s}{r}}$$
    *   Limit at Horizon ($r \to r_s$): $\Xi \to 1 - e^{-\varphi} \approx 0.8017$
    *   Limit at Infinity ($r \to \infty$): $\Xi \to 1 - e^0 = 0$ (Correctly recovers flat Minkowski space).
*   **The Banned Formulation (DEPRECATED & FORBIDDEN):** $\Xi(r) = 1 - e^{-arphi r_s / r}$

---

## 4. Resolution of the Blend-Zone Logic

The operational mapping must transition from the strong field (inner) to the weak field (outer):

*   **$g_2$ (Strong Field):** Applies for $r < 1.8 r_s$. Governed by $\Xi_{\text{strong}}(r)$.
*   **Blend Zone ($C^2$ Hermite Interpolation):** Applies for $1.8 r_s \leq r \leq 2.2 r_s$. The Hermite polynomial $H_5(t)$ ensures $D$, $D'$, and $D''$ are strictly continuous.
*   **$g_1$ (Weak Field):** Applies for $r > 2.2 r_s$. Governed by $\Xi_{\text{weak}}(r) = \frac{r_s}{2r}$.

---

## 5. Parameter Transparency: The $\varphi$-Correction

The shift from 0% win rate to 51% overall win rate using the $\varphi$-based mass correction $\Delta(M) = A e^{-\alpha r_s} + B$ is impressive, but carries a high risk of being perceived as a data-fit.

**Mandate:** Documentation must explicitly state whether the parameters $A=98.01$, $\alpha=2.72\times 10^4$, $B=1.96$ were theoretically derived *a priori* or calibrated via optimization *a posteriori* against the same dataset. If calibrated, it must be declared as a "model fit requiring out-of-sample blind testing."

---

## 6. Software Engineering Consolidation Plan

1.  **The `ssz-core` Monorepo:** Create a single, canonical Python package (`ssz-core`).
2.  **Formula Registry:** Every formula receives an ID, domain of validity, and boundary limits.
3.  **Claim Registry:** Every physical claim must be tagged with its epistemological status.
4.  **"Known Limitations" Documentation:** Prominently display unresolved issues (e.g., $r < 2 r_s$ failure, non-radial extensions).
