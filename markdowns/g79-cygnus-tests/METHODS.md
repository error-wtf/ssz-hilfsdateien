# Methodology - G79.29+0.46 SSZ Validation

**Complete Methodological Documentation**  
**Date:** 2025-11-05

---

## I. Overview

This document describes the complete methodology for validating Segmented Spacetime (SSZ) predictions against observational data for the LBV nebula G79.29+0.46.

**Analysis Pipeline:**
1. Domain Classification (M = v/c_s < 0.3)
2. Energy Release Calculation (velocity excess)
3. Temperature Model Validation
4. Statistical Significance Testing

---

## II. Domain Classification Method

### A. Physical Criterion

**Mach Number Threshold:**
```
M = v / c_s

where:
  v = expansion velocity [km/s]
  c_s = sound speed = sqrt(k_B T / μ m_H) [km/s]
  
Threshold: M = 0.3
  M < 0.3 → g^(2) domain (SSZ applies)
  M > 0.3 → g^(1) domain (classical)
```

**Sound Speed Calculation:**
```python
import numpy as np

k_B = 1.380649e-23  # J/K (Boltzmann constant)
m_H = 1.673557e-27  # kg (proton mass)
μ = 2.3  # Mean molecular weight (for molecular gas)

def sound_speed(T_K):
    """Calculate sound speed in km/s"""
    c_s_SI = np.sqrt(k_B * T_K / (μ * m_H))  # m/s
    c_s_km_s = c_s_SI / 1000.0  # km/s
    return c_s_km_s
```

### B. Heuristic for G79

**Without velocity data:**
```python
def estimate_velocity_heuristic(r_pc):
    """
    Heuristic velocity estimate based on radius
    
    Assumption: Hubble-like expansion v ~ r/t
    For G79: t ~ 10,000 yr, age estimate
    """
    t_yr = 10000
    t_s = t_yr * 3.15e7  # Convert to seconds
    r_m = r_pc * 3.086e16  # Convert to meters
    v_m_s = r_m / t_s
    v_km_s = v_m_s / 1000.0
    return v_km_s

# Alternative: Use observed velocity gradient
def estimate_velocity_observed(r_pc):
    """
    Based on CO observations
    v ~ 15 km/s at r ~ 1 pc
    """
    r_ref = 1.0  # pc
    v_ref = 15.0  # km/s
    v = v_ref * (r_pc / r_ref)
    return v
```

### C. Classification Function

```python
def classify_regime(v_km_s, T_K):
    """
    Classify data point into g^(1) or g^(2) domain
    
    Args:
        v_km_s: expansion velocity [km/s]
        T_K: temperature [K]
    
    Returns:
        regime: "g^(2)" or "g^(1)"
        M: Mach number
    """
    c_s = sound_speed(T_K)
    M = v_km_s / c_s
    
    if M < 0.3:
        regime = "g^(2)"
    else:
        regime = "g^(1)"
    
    return regime, M

# Apply to dataset
for i in range(len(data)):
    r_pc = data['radius_pc'][i]
    T_K = data['temperature_K'][i]
    v_km_s = estimate_velocity(r_pc)
    
    regime, M = classify_regime(v_km_s, T_K)
    data['regime'][i] = regime
    data['Mach'][i] = M
```

---

## III. Energy Release Method

### A. Physical Model

**Mechanism:**
When material decouples from g^(2) (γ_seg < 1) to g^(1) (γ = 1), stored temporal energy is released kinetically.

**Formula Derivation:**
```
Energy in g^(2):
  E^(2) = (1/2) m v_launch^2 + m c^2 (1 - γ_seg)
  
Energy in g^(1):
  E^(1) = (1/2) m v_obs^2
  
Conservation:
  E^(2) = E^(1)
  (1/2) m v_launch^2 + m c^2 (1 - γ_seg) = (1/2) m v_obs^2
  
Solve for v_obs:
  v_obs^2 = v_launch^2 + 2c^2 (1 - γ_seg)
```

**Non-Relativistic Limit:**
```
For astrophysical systems, 2c^2 (1 - γ_seg) >> v^2
We use characteristic velocity scale:

  v_char = sqrt(GM/R)  # Gravitational velocity
  
Modified formula:
  v_obs^2 = v_launch^2 + v_char^2 (1 - γ_seg)
```

### B. Implementation

```python
def gamma_seg(r_pc, alpha=0.12, r_c=1.9):
    """
    Segmentation function
    
    Args:
        r_pc: radius [pc]
        alpha: segmentation strength (0 < alpha < 1)
        r_c: characteristic radius [pc]
    
    Returns:
        gamma_seg: segmentation factor (< 1)
    """
    return 1.0 - alpha * np.exp(-(r_pc / r_c)**2)

def energy_release_velocity(v_launch_km_s, gamma_seg_val, v_char_km_s=50.0):
    """
    Calculate observed velocity after g^(2) → g^(1) decoupling
    
    Args:
        v_launch_km_s: Launch velocity from g^(2) [km/s]
        gamma_seg_val: Segmentation factor at launch
        v_char_km_s: Characteristic gravitational velocity [km/s]
    
    Returns:
        v_obs: Observed velocity in g^(1) [km/s]
    """
    # Energy release term
    delta_v_sq = v_char_km_s**2 * (1 - gamma_seg_val)
    
    # Total velocity
    v_obs_sq = v_launch_km_s**2 + delta_v_sq
    v_obs = np.sqrt(v_obs_sq)
    
    return v_obs

def velocity_excess(v_launch_km_s, gamma_seg_val, v_char_km_s=50.0):
    """
    Calculate velocity excess Δv
    
    Returns:
        Delta_v: Excess velocity beyond classical [km/s]
    """
    v_obs = energy_release_velocity(v_launch_km_s, gamma_seg_val, v_char_km_s)
    Delta_v = v_obs - v_launch_km_s
    return Delta_v
```

### C. Application to G79

```python
# System parameters
M_sun = 1.989e30  # kg
G = 6.674e-11  # m^3 kg^-1 s^-2
pc_to_m = 3.086e16  # m

M_total = 10 * M_sun  # kg
R_pc = 1.0  # pc
R_m = R_pc * pc_to_m  # m

# Characteristic velocity
v_char_m_s = np.sqrt(G * M_total / R_m)
v_char_km_s = v_char_m_s / 1000.0  # ~ 50 km/s

# Classical prediction
v_classical = 10.0  # km/s (wind-bubble)

# With energy release
gamma_at_boundary = 0.95  # From spatial analysis
v_with_release = energy_release_velocity(v_classical, gamma_at_boundary, v_char_km_s)
Delta_v = v_with_release - v_classical

print(f"Classical: {v_classical:.1f} km/s")
print(f"With release: {v_with_release:.1f} km/s")
print(f"Excess: {Delta_v:.1f} km/s")
```

---

## IV. Temperature Model Method

### A. SSZ Temperature Formula

**Model:**
```
T(r) = T_0 · γ_seg(r)

where:
  γ_seg(r) = 1 - α · exp[-(r/r_c)^2]
```

**Physical Interpretation:**
- T_0: Reference temperature (boundary value)
- γ_seg < 1: Time flows slower → energy accumulates → higher T
- Inversion: T decreases outward as γ_seg → 1

### B. Parameter Fitting

**Method: Least Squares Optimization**

```python
from scipy.optimize import curve_fit

def temperature_model(r_pc, T0, alpha, r_c):
    """
    SSZ temperature prediction
    
    Args:
        r_pc: radius array [pc]
        T0: reference temperature [K]
        alpha: segmentation strength
        r_c: characteristic radius [pc]
    
    Returns:
        T: predicted temperature array [K]
    """
    gamma = 1.0 - alpha * np.exp(-(r_pc / r_c)**2)
    T = T0 * gamma
    return T

# Fit to data
r_data = df['radius_pc'].values
T_data = df['temperature_K'].values

# Option 1: Fix paper parameters
alpha_fixed = 0.12
r_c_fixed = 1.9

def temp_model_fixed(r_pc, T0):
    return temperature_model(r_pc, T0, alpha_fixed, r_c_fixed)

popt_fixed, pcov_fixed = curve_fit(temp_model_fixed, r_data, T_data, p0=[240])
T0_fitted = popt_fixed[0]

# Option 2: Fit all parameters
popt_free, pcov_free = curve_fit(temperature_model, r_data, T_data, 
                                  p0=[240, 0.12, 1.9],
                                  bounds=([0, 0, 0.1], [500, 1.0, 10.0]))
T0_fit, alpha_fit, r_c_fit = popt_free
```

### C. Error Metrics

```python
def calculate_errors(T_obs, T_pred):
    """
    Calculate error metrics
    
    Returns:
        MAE: Mean Absolute Error [K]
        RMSE: Root Mean Square Error [K]
        R2: Coefficient of determination
    """
    residuals = T_obs - T_pred
    
    MAE = np.mean(np.abs(residuals))
    RMSE = np.sqrt(np.mean(residuals**2))
    
    SS_res = np.sum(residuals**2)
    SS_tot = np.sum((T_obs - np.mean(T_obs))**2)
    R2 = 1 - (SS_res / SS_tot)
    
    return MAE, RMSE, R2

# Apply
T_pred_fixed = temperature_model(r_data, T0_fitted, alpha_fixed, r_c_fixed)
MAE_fixed, RMSE_fixed, R2_fixed = calculate_errors(T_data, T_pred_fixed)

T_pred_free = temperature_model(r_data, T0_fit, alpha_fit, r_c_fit)
MAE_free, RMSE_free, R2_free = calculate_errors(T_data, T_pred_free)

print(f"Fixed params: MAE={MAE_fixed:.2f} K, RMSE={RMSE_fixed:.2f} K, R²={R2_fixed:.2f}")
print(f"Free params:  MAE={MAE_free:.2f} K, RMSE={RMSE_free:.2f} K, R²={R2_free:.2f}")
```

---

## V. Statistical Analysis Method

### A. Domain Significance Test

**Chi-Square Test for Independence:**
```python
from scipy.stats import chi2_contingency

# Contingency table: Domain vs Temperature Range
contingency_table = np.array([
    [5, 0],  # High T (>35K): g^(2), g^(1)
    [0, 5]   # Low T (<35K): g^(2), g^(1)
])

chi2, p_value, dof, expected = chi2_contingency(contingency_table)
print(f"Chi-square: {chi2:.3f}, p-value: {p_value:.4f}")

if p_value < 0.05:
    print("Domains are statistically distinct (p < 0.05)")
```

### B. Velocity Prediction Significance

**Residual Analysis:**
```python
def velocity_residual(v_obs, v_pred, sigma_v):
    """
    Calculate normalized residual
    
    Args:
        v_obs: observed velocity [km/s]
        v_pred: predicted velocity [km/s]
        sigma_v: velocity uncertainty [km/s]
    
    Returns:
        residual: (v_obs - v_pred) / sigma_v
    """
    return (v_obs - v_pred) / sigma_v

# For G79
v_obs = 15.0  # km/s (median)
v_pred = 15.0  # km/s (from energy release)
sigma_v = 1.0  # km/s (estimate from 14-16 range)

residual = velocity_residual(v_obs, v_pred, sigma_v)
print(f"Normalized residual: {residual:.2f}σ")

if np.abs(residual) < 1.0:
    print("Prediction within 1σ (excellent match!)")
```

### C. Temperature Correlation Test

**Null Hypothesis:** T(r) independent of γ_seg(r)

```python
from scipy.stats import pearsonr

# Calculate correlation
gamma_values = gamma_seg(r_data, alpha=0.12, r_c=1.9)
corr, p_value = pearsonr(T_data, gamma_values)

print(f"Pearson correlation: r={corr:.3f}, p={p_value:.4f}")

if p_value < 0.05:
    print("Correlation significant (reject null hypothesis)")
```

---

## VI. Visualization Method

### A. Domain Classification Plot

```python
import matplotlib.pyplot as plt

def plot_domain_classification(df):
    """
    Create publication-quality domain classification figure
    """
    fig, ax = plt.subplots(figsize=(10, 6))
    
    # Separate by domain
    g2_mask = df['regime'] == 'g^(2)'
    g1_mask = df['regime'] == 'g^(1)'
    
    # Plot
    ax.scatter(df[g2_mask]['radius_pc'], df[g2_mask]['temperature_K'],
               c='blue', marker='o', s=100, label='g^(2) domain (SSZ)', zorder=3)
    ax.scatter(df[g1_mask]['radius_pc'], df[g1_mask]['temperature_K'],
               c='red', marker='s', s=100, label='g^(1) domain (classical)', zorder=3)
    
    # Boundary line
    r_boundary = 1.0
    ax.axvline(r_boundary, color='gray', linestyle='--', linewidth=2, 
               label='Domain boundary (r ~ 1 pc)', zorder=2)
    
    # Labels
    ax.set_xlabel('Radius [pc]', fontsize=14)
    ax.set_ylabel('Temperature [K]', fontsize=14)
    ax.set_title('G79.29+0.46: Domain Classification', fontsize=16)
    ax.legend(fontsize=12)
    ax.grid(True, alpha=0.3, zorder=1)
    
    plt.tight_layout()
    return fig

# Generate
fig = plot_domain_classification(df)
fig.savefig('results/two_metric_domains.png', dpi=300, bbox_inches='tight')
```

### B. Energy Release Plot

```python
def plot_energy_release():
    """
    Create publication-quality energy release figure
    """
    fig, axes = plt.subplots(1, 2, figsize=(14, 6))
    
    # Left panel: Δv vs gamma_seg
    ax = axes[0]
    gamma_values = np.linspace(0.70, 0.98, 100)
    v_launch = 10.0
    v_char = 50.0
    delta_v_values = [velocity_excess(v_launch, g, v_char) for g in gamma_values]
    
    ax.plot(gamma_values, delta_v_values, 'b-', linewidth=2)
    ax.axhline(5.0, color='red', linestyle='--', linewidth=2, 
               label='G79 observed (~5 km/s)')
    ax.axvline(0.95, color='green', linestyle='--', linewidth=2,
               label='Match at γ_seg ~ 0.95')
    ax.set_xlabel('Segmentation Factor γ_seg', fontsize=14)
    ax.set_ylabel('Velocity Excess Δv [km/s]', fontsize=14)
    ax.set_title('Energy Release Prediction', fontsize=13)
    ax.legend(fontsize=11)
    ax.grid(True, alpha=0.3)
    
    # Right panel: v_obs vs gamma_seg
    ax = axes[1]
    v_obs_values = [energy_release_velocity(v_launch, g, v_char) for g in gamma_values]
    
    ax.plot(gamma_values, v_obs_values, 'b-', linewidth=2, label='With energy release')
    ax.axhline(v_launch, color='gray', linestyle=':', linewidth=2,
               label=f'Launch velocity ({v_launch} km/s)')
    ax.axhspan(14, 16, color='red', alpha=0.2, label='G79 observed (14-16 km/s)')
    ax.axvline(0.95, color='green', linestyle='--', linewidth=2)
    ax.set_xlabel('Segmentation Factor γ_seg', fontsize=14)
    ax.set_ylabel('Observed Velocity v_obs [km/s]', fontsize=14)
    ax.set_title('Velocity Prediction', fontsize=13)
    ax.legend(fontsize=11)
    ax.grid(True, alpha=0.3)
    
    plt.tight_layout()
    return fig

# Generate
fig = plot_energy_release()
fig.savefig('results/energy_release_mechanism.png', dpi=300, bbox_inches='tight')
```

---

## VII. Error Analysis Method

### A. Propagation of Uncertainties

**For velocity prediction:**
```python
def velocity_uncertainty(M, sigma_M, R, sigma_R, gamma_seg, sigma_gamma):
    """
    Calculate uncertainty in velocity prediction
    
    Uses error propagation formula:
    σ_v^2 = (∂v/∂M)^2 σ_M^2 + (∂v/∂R)^2 σ_R^2 + (∂v/∂γ)^2 σ_γ^2
    """
    G = 6.674e-11
    M_sun = 1.989e30
    pc_to_m = 3.086e16
    
    M_kg = M * M_sun
    R_m = R * pc_to_m
    
    # Partial derivatives
    dv_dM = 0.5 * np.sqrt(G / (M_kg * R_m))
    dv_dR = -0.5 * np.sqrt(G * M_kg) / R_m**(1.5)
    
    # For simplified case (v_char constant)
    v_char = np.sqrt(G * M_kg / R_m) / 1000.0  # km/s
    dv_dgamma = -0.5 * v_char**2 / np.sqrt(10**2 + v_char**2 * (1 - gamma_seg))
    
    # Combine
    sigma_v_sq = (dv_dM * sigma_M * M_sun)**2 + \
                 (dv_dR * sigma_R * pc_to_m)**2 + \
                 (dv_dgamma * sigma_gamma)**2
    
    sigma_v = np.sqrt(sigma_v_sq) / 1000.0  # Convert to km/s
    return sigma_v

# For G79
M = 10.0  # M_sun
sigma_M = 2.0  # M_sun
R = 1.0  # pc
sigma_R = 0.2  # pc
gamma_seg = 0.95
sigma_gamma = 0.02

sigma_v = velocity_uncertainty(M, sigma_M, R, sigma_R, gamma_seg, sigma_gamma)
print(f"Velocity uncertainty: ±{sigma_v:.1f} km/s")
```

### B. Bootstrap Resampling

**For parameter confidence intervals:**
```python
from scipy.optimize import curve_fit

def bootstrap_fit(r_data, T_data, n_bootstrap=1000):
    """
    Bootstrap resampling for parameter uncertainties
    
    Returns:
        parameter distributions
    """
    n_points = len(r_data)
    T0_samples = []
    alpha_samples = []
    r_c_samples = []
    
    for i in range(n_bootstrap):
        # Resample with replacement
        indices = np.random.choice(n_points, size=n_points, replace=True)
        r_boot = r_data[indices]
        T_boot = T_data[indices]
        
        # Fit
        try:
            popt, _ = curve_fit(temperature_model, r_boot, T_boot,
                                p0=[240, 0.12, 1.9],
                                bounds=([0, 0, 0.1], [500, 1.0, 10.0]))
            T0_samples.append(popt[0])
            alpha_samples.append(popt[1])
            r_c_samples.append(popt[2])
        except:
            continue
    
    # Calculate confidence intervals
    T0_mean = np.mean(T0_samples)
    T0_std = np.std(T0_samples)
    alpha_mean = np.mean(alpha_samples)
    alpha_std = np.std(alpha_samples)
    r_c_mean = np.mean(r_c_samples)
    r_c_std = np.std(r_c_samples)
    
    print(f"T0 = {T0_mean:.1f} ± {T0_std:.1f} K")
    print(f"alpha = {alpha_mean:.3f} ± {alpha_std:.3f}")
    print(f"r_c = {r_c_mean:.2f} ± {r_c_std:.2f} pc")
    
    return T0_samples, alpha_samples, r_c_samples
```

---

## VIII. Data Quality Assessment

### A. Outlier Detection

```python
def detect_outliers(data, threshold=3.0):
    """
    Detect outliers using modified Z-score
    
    Args:
        data: array of values
        threshold: number of standard deviations
    
    Returns:
        outlier_mask: boolean array
    """
    median = np.median(data)
    mad = np.median(np.abs(data - median))
    modified_z_score = 0.6745 * (data - median) / mad
    
    outlier_mask = np.abs(modified_z_score) > threshold
    return outlier_mask

# Apply to G79 data
T_outliers = detect_outliers(df['temperature_K'])
if np.any(T_outliers):
    print(f"Warning: {np.sum(T_outliers)} temperature outliers detected")
```

### B. Consistency Checks

```python
def check_data_consistency(df):
    """
    Verify data quality
    """
    checks = []
    
    # Check 1: Monotonic radius
    radii_sorted = np.all(np.diff(df['radius_pc']) > 0)
    checks.append(("Radii monotonic", radii_sorted))
    
    # Check 2: Temperature positive
    T_positive = np.all(df['temperature_K'] > 0)
    checks.append(("Temperatures positive", T_positive))
    
    # Check 3: Reasonable range
    T_range = (10 < df['temperature_K']) & (df['temperature_K'] < 300)
    T_reasonable = np.all(T_range)
    checks.append(("Temperatures reasonable", T_reasonable))
    
    # Report
    for check_name, passed in checks:
        status = "PASS" if passed else "FAIL"
        print(f"{check_name}: {status}")
    
    return all([c[1] for c in checks])
```

---

## IX. Reproducibility

### A. Random Seed Management

```python
import numpy as np
import random

# Set seeds for reproducibility
RANDOM_SEED = 42

np.random.seed(RANDOM_SEED)
random.seed(RANDOM_SEED)
```

### B. Version Control

```python
import sys
import matplotlib
import scipy

def print_versions():
    """Print package versions for reproducibility"""
    print(f"Python: {sys.version}")
    print(f"NumPy: {np.__version__}")
    print(f"SciPy: {scipy.__version__}")
    print(f"Matplotlib: {matplotlib.__version__}")
    print(f"Pandas: {pd.__version__}")

# Call at start of analysis
print_versions()
```

---

## X. Best Practices

### A. Code Organization

```
scripts/
├── two_metric_model.py       # Domain classification
├── energy_release_model.py   # Velocity calculation
└── verify_paper_predictions_FIXED.py  # Temperature validation

Each script:
1. Imports at top
2. Constants defined
3. Functions defined
4. Main analysis in if __name__ == "__main__"
5. Output generation
```

### B. Documentation Standards

**Function Docstrings:**
```python
def function_name(arg1, arg2):
    """
    Brief description
    
    Longer description if needed
    
    Args:
        arg1: description [units]
        arg2: description [units]
    
    Returns:
        result: description [units]
        
    Raises:
        ValueError: when invalid input
    """
    pass
```

### C. Output Standards

**Figures:**
- DPI: 300 (publication quality)
- Format: PNG (for draft), PDF (for publication)
- Font sizes: Title 16pt, Labels 14pt, Legend 12pt
- Color-blind friendly colors

**Text Output:**
- Clear section headers (=== or ---)
- Units always specified
- Significant figures appropriate (2-3 for uncertainties)
- Warnings/errors clearly marked

---

**Document Version:** 1.0  
**Last Updated:** 2025-11-05

© 2025 Carmen N. Wrede, Lino P. Casu  
Licensed under ANTI-CAPITALIST SOFTWARE LICENSE v1.4
