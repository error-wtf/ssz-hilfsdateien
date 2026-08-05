# External Validation Protocol for SSZ

This protocol defines the strict standards required for validating the Segmented Spacetime (SSZ) framework against independent, public astrophysical observational data products (NICER, ALMA).

## Core Principles

1. **Strict Separation of Concerns**: 
   - Core tests establish internal consistency.
   - Fetching scripts retrieve and manifest public files.
   - Independent reducers derive the astronomical quantities.
   - Validation comparisons perform anti-circular residual evaluations.
2. **Absolute Ban on Curve-Fitting**:
   - Tuning parameters ($\Xi, \varphi$) or using regression algorithms to map predictions to results is strictly banned.
3. **Transparency in Data-Dependency**:
   - Highly model-dependent inputs (e.g. published mass/radius estimates derived using General Relativity priors) must be explicitly flagged and cannot serve as hard proof.
