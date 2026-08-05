# SSZ Equation Registry v0.2

## LOCKED CORE EQUATIONS

### PHI
- **Formula:** `(1 + sqrt(5)) / 2`
- **Value:** ≈ 1.618
- **Source:** SSZ_BOOK_DE_CLEAN.md Ch.1
- **Status:** LOCKED ✅

### XI_MAX
- **Formula:** `1 - exp(-PHI)`
- **Value:** ≈ 0.802
- **Source:** SSZ_BOOK_DE_CLEAN.md Ch.1
- **Status:** LOCKED ✅

### D_MIN
- **Formula:** `1 / (1 + XI_MAX)`
- **Value:** ≈ 0.555
- **Source:** SSZ_BOOK_DE_CLEAN.md Ch.1
- **Status:** LOCKED ✅

### XI_WEAK
- **Formula:** `r_s / (2 * r)`
- **Source:** SSZ_BOOK_DE_CLEAN.md Ch.1
- **Status:** LOCKED ✅

### XI_STRONG
- **Formula:** `min(1 - exp(-PHI * r_s / r), XI_MAX)`
- **Source:** SSZ_BOOK_DE_CLEAN.md Ch.1
- **Status:** LOCKED ✅

### D_SSZ
- **Formula:** `1 / (1 + XI)`
- **Source:** SSZ_BOOK_DE_CLEAN.md Ch.1
- **Status:** LOCKED ✅

### S_SCALE
- **Formula:** `s = 1 + XI = 1/D`
- **Source:** SSZ Book Ch.1
- **Status:** LOCKED ✅

## LOCKED INSPIRAL EQUATIONS (NEW)

### GW_POWER_SSZ
- **Formula:** `P_GW^SSZ = P_GW^GR × D(r)² / s(r)²`
- **Source:** SSZ_BOOK_DE_CLEAN.md Ch.31-32 (Lagrangian)
- **Status:** LOCKED ✅
- **Note:** P_GW reduced in strong field

### RDOT_SSZ
- **Formula:** `ṙ_SSZ = ṙ_GR × D(r)² / s(r)⁴`
- **Source:** SSZ_BOOK_DE_CLEAN.md Ch.31-32
- **Status:** LOCKED ✅
- **Note:** Stronger correction than P_GW

### ORBITAL_FREQUENCY
- **Formula:** `Ω(r) = √(GM/r³)`
- **Source:** Newtonian/Kepler
- **Status:** LOCKED ✅

### DPHI_DR
- **Formula:** `dφ/dr = Ω(r) / ṙ(r)`
- **Source:** Orbital mechanics
- **Status:** LOCKED ✅

### ACCUMULATED_PHASE
- **Formula:** `φ = ∫ dφ/dr dr`
- **Source:** Integration of above
- **Status:** LOCKED ✅

## FORWARD MODEL READY

### RSG_COORDINATE
- **Formula:** `ρ(r) = ∫ D(r')/s(r') dr'` (proxy)
- **Source:** RSG paper concept
- **Status:** EXPLORATORY ⚠️ (proxy implementation)

### PHASE_TO_FREQUENCY
- **Formula:** `r(f) = (GM/(πf)²)^(1/3)`
- **Source:** Leading-order Kepler
- **Status:** LOCKED ✅ (with caveats)

### DELTA_PSI_SSZ
- **Formula:** `δΨ_SSZ(f) = Δφ(r(f))`
- **Source:** Derived from above
- **Status:** READY_FOR_DRY_RUN ✅

## BLOCKED / CONFLICTING

### RINGDOWN_EPSILON_220
- **Conflicting Sources:**
  - A: ~3% (Book Ch.30 text)
  - B: ~31% (Book Ch.30 "∝ D_min²")
  - C: ~39% (qnm_spectrum.md photon sphere)
- **Status:** CONFLICTING ❌❌❌
- **Action:** Resolution required from SSZ authors

### ETA_220
- **Formula:** NOT_IN_CORPUS
- **Status:** MISSING ❌

## READINESS SUMMARY

| Component | Status |
|-----------|--------|
| Core equations | ✅ LOCKED |
| Inspiral phase | ✅ READY |
| δΨ_SSZ(f) | ✅ DRY RUN READY |
| Ringdown | ❌ BLOCKED |
| LIGO comparison | ⏳ Pending |

## Next Steps

1. ✅ Run dry-run tests on δΨ_SSZ(f)
2. ✅ Assess magnitude in LIGO band
3. ⏳ Compare coherence H1/L1
4. ❌ Ringdown only after conflict resolved
