# RATIONAL_MESH_FIGURE_VALIDATION

## CONFIGURATION

Finite Rational Mesh Baseline

## PARAMETER

m = 10

## POINT_COUNT

121

## EXACT_UNIT_DISTANCE_EDGE_COUNT

82

## CONSTRUCTION_SOURCE

`case_studies/erdos_unit_distance_2026/rational_mesh_baseline.py`

Function: `rational_mesh_points(m)`

## EXACT_VALIDATOR_SOURCE

`counterexample_commons/validators/unit_distance.py`

Function: `count_unit_edges_exact(points)`

## VALIDATION_ARITHMETIC

exact rational arithmetic using SymPy `Rational`.

The exact validator computes squared distance as `dx^2 + dy^2` and counts an
edge only when that rational value is exactly equal to `1`.

## FIGURE_TITLE

Finite Rational Mesh Baseline (m=10): 121 points, 82 exactly validated
unit-distance edges

## SCIENTIFIC_SCOPE

Finite rational mesh baseline - not Sawin's construction.
Finite exact validation only; not evidence for exponent n^1.014.

## SAWIN_STATUS_MUTATED

NO
