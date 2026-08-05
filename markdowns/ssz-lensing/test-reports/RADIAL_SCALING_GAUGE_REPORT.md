# Radial Scaling Gauge - Validation Report

**Generated:** 2026-01-22T11:54:40.748710

**Status:** 28/28 Tests Passed (100%)

---

## Section 2 (8/8)

| Test | Result | Expected | Actual |
|------|--------|----------|--------|
| Scaling factor s(r) = 1 + Xi(r) | PASS | 1 | 1 |
| Xi weak field: Xi = r_s/(2r) | PASS | 9.87342e-09 | 9.87342e-09 |
| s(r) -> 1 at infinity | PASS | 1 | 1 |
| Schwarzschild radius (Sun) | PASS | 2953.25 | 2954.13 |
| Xi at solar surface | PASS | 2.12222e-06 | 2.12222e-06 |
| s(R_sun) = 1 + Xi(R_sun) | PASS | 1 | 1 |
| Xi monotonically decreasing | PASS | 1 | 1 |
| Xi always positive | PASS | 1 | 1 |

## Section 3 (7/7)

| Test | Result | Expected | Actual |
|------|--------|----------|--------|
| k_eff = k0 * s(r) | PASS | 1e+07 | 1e+07 |
| Local c invariant | PASS | 2.99792e+08 | 2.99792e+08 |
| Phase in flat space | PASS | 1e+16 | 1.001e+16 |
| Phase excess in curved space | PASS | 5.568e+16 | 5.57358e+16 |
| Redshift z = Delta_Xi | PASS | 1.09245e-13 | 1.09245e-13 |
| D(r) = 1/(1 + Xi) | PASS | 1 | 1 |
| Wavelength scaling | PASS | 5e-07 | 5e-07 |

## Appendix A.1 (3/3)

| Test | Result | Expected | Actual |
|------|--------|----------|--------|
| Shapiro delay (Cassini 2003) | PASS | 0.000263774 | 0.000263774 |
| Shapiro delay (solar grazing) | PASS | 0.000270716 | 0.000270716 |
| PPN factor (1+gamma) for Shapiro | PASS | 0.000243395 | 0.000243395 |

## Appendix A.2 (3/3)

| Test | Result | Expected | Actual |
|------|--------|----------|--------|
| Light deflection at solar limb | PASS | 1.75 | 1.75096 |
| Deflection PPN formula | PASS | 4.24443e-06 | 4.24443e-06 |
| Deflection ~ 1/b | PASS | 2 | 2 |

## Appendix B (2/2)

| Test | Result | Expected | Actual |
|------|--------|----------|--------|
| WKB classical limit | PASS | 6.96e+19 | 6.96697e+19 |
| Phase ~ k0 | PASS | 2 | 2 |

## Frame Problem (2/2)

| Test | Result | Expected | Actual |
|------|--------|----------|--------|
| Loop closure I_ABC = 0 | PASS | 0 | 384 |
| Coordinate independence | PASS | 1.09245e-13 | 1.09245e-13 |

## Experimental Validation (3/3)

| Test | Result | Expected | Actual |
|------|--------|----------|--------|
| Pound-Rebka redshift | PASS | 2.46e-15 | 2.45838e-15 |
| GPS gravitational drift | PASS | 45.7 | 45.7229 |
| Tokyo Skytree clocks | PASS | 4.9e-14 | 4.91644e-14 |
