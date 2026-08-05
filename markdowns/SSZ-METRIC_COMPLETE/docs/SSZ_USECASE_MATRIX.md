# SSZ Multi-Scale Usecase Matrix

This matrix summarizes the physical scale domains, primary quantities, evaluation methods, test files, and ehrliche validation status of the multi-scale SSZ framework.

| Domain | Scale | Primary Quantity | Method | Implemented? | Tests | Validation Status | Limitations |
| :--- | :--- | :--- | :--- | :---: | :--- | :--- | :--- |
| **Planck & Fine-Structure** | $l_P \approx 10^{-35}$ m | `PHI`, $\alpha_{\text{SSZ}}$ | `XI_STRONG_FIELD_DIAGNOSTIC` | Yes | `test_fine_structure_domain.py` | internal identity tested | No full quantum gravity theory |
| **Phi-Lattice Segmentation** | Lattice indices $k$ | $\Xi(r)$, $\rho(r_1, r2)$ | `XI_DIRECT` | Yes | `test_phi_lattice_segmentation.py` | internal identity tested | Static discrete spacing proxy only |
| **Quantum/Frequency/Phase** | Wave transport | $D(r)$, $s(r)$, local $c$ | `SSZ_KINEMATIC_IDENTITY` | Yes | `test_phase_frequency_domain.py` | forward formula tested | No wave dispersion in matter |
| **EM & Clock** | Redshift & dilation | $D(r)$, $s(r)$ | `XI_DIRECT` | Yes | `test_em_clock_domain.py` | external reference formula tested | No Earth quadrupole moments |
| **Weak-Field PPN** | $r \gg r_s$ (Solar system) | $\beta_{\text{PPN}}$, $\gamma_{\text{PPN}}$ | `PPN_COMPLETION`, `PPN_ORBIT` | Yes | `test_weak_field_ppn_domain.py` | external reference formula tested | First-order weak field expansions only |
| **Strong-Field Compact** | $r \approx r_s$ | $\Xi(r_s)$, WEC/SEC | `XI_STRONG_FIELD_DIAGNOSTIC` | Yes | `test_strong_field_compact_domain.py` | internal identity tested | Static proxy; no dynamical collapse |
| **Neutron Star** | Stellar boundaries | Compactness, redshift | `XI_STRONG_FIELD_DIAGNOSTIC` | Yes | `test_neutron_star_domain.py` | external observational validation pending | No nuclear equation of state |
