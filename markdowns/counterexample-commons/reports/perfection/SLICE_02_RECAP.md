# Slice 2 Recap - Exact Mathematical Baselines

DATE: 2026-05-24

## Raw Test Output

`
============================= test session starts =============================
platform win32 -- Python 3.12.10, pytest-8.4.2, pluggy-4.4.2
rootdir: E:\clone\counterexample-commons
configfile: pyproject.toml

collected 21 items

tests/test_validators.py::TestCountUnitEdges::test_two_points_at_distance_one PASSED
tests/test_validators.py::TestCountUnitEdges::test_two_points_not_at_distance_one PASSED
tests/test_validators.py::TestCountUnitEdges::test_equilateral_triangle PASSED
tests/test_validators.py::TestCountUnitEdges::test_single_point PASSED
tests/test_validators.py::TestCountUnitEdges::test_empty PASSED
tests/test_validators.py::TestLineConfiguration::test_line_edge_count[1-0] PASSED
tests/test_validators.py::TestLineConfiguration::test_line_edge_count[2-1] PASSED
tests/test_validators.py::TestLineConfiguration::test_line_edge_count[5-4] PASSED
tests/test_validators.py::TestLineConfiguration::test_line_edge_count[16-15] PASSED
tests/test_validators.py::TestLineConfiguration::test_line_edge_count[100-99] PASSED
tests/test_validators.py::TestLineConfiguration::test_line_n_zero_raises PASSED
tests/test_validators.py::TestGridConfiguration::test_grid_edge_count[1-0] PASSED
tests/test_validators.py::TestGridConfiguration::test_grid_edge_count[2-4] PASSED
tests/test_validators.py::TestGridConfiguration::test_grid_edge_count[3-12] PASSED
tests/test_validators.py::TestGridConfiguration::test_grid_edge_count[4-24] PASSED
tests/test_validators.py::TestGridConfiguration::test_grid_edge_count[5-40] PASSED
tests/test_validators.py::TestGridConfiguration::test_grid_k_zero_raises PASSED
tests/test_validators.py::TestCustomConfiguration::test_four_point_square PASSED
tests/test_validators.py::TestCustomConfiguration::test_rational_coordinates PASSED
tests/test_validators.py::TestCustomConfiguration::test_duplicate_raises PASSED
tests/test_validators.py::TestCustomConfiguration::test_bad_coordinate_raises PASSED

============================= 21 passed in 1.41s =============================
`

## Verification Summary

| Validator | Tests | Status |
|-----------|-------|--------|
| count_unit_edges_exact | 5 | PASSED |
| validate_line_configuration | 6 | PASSED |
| validate_grid_configuration | 6 | PASSED |
| validate_custom_configuration | 4 | PASSED |
| **TOTAL** | **21** | **21 PASSED** |

## Exact Arithmetic Verification

All calculations use sympy.Rational — no floating-point approximations:
- Line n=100: 99 edges exact
- Grid k=5: 40 edges exact
- Custom 3/5, 4/5: distance = 1 exact

## Status

EXACT_BASELINE_GATE: PASSED
RECOMMENDED_NEXT: Slice 3 - Gradio UI real testen
