# SEIR Model – Sensitivity Analysis with Uncertain Parameters

This folder contains a Python implementation of an SEIR epidemiological model with cumulative cases and sensitivity analysis under parametric uncertainty. It follows a structured set of tasks and provides visual and statistical insights into the robustness of model predictions.

Group:

- Mitzi
- Thea
- Matheus
- Huyen

---

## 🧮 Model Overview

We simulate the SEIR model extended with a **cumulative cases compartment** `C(t)` using the following ODE system:

- **S**: Susceptible
- **E**: Exposed
- **I**: Infectious
- **R**: Recovered
- **C**: Cumulative reported cases

The differential equations are:

dS/dt = -β * S * I / N  
dE/dt = β * S * I / N - α * E  
dI/dt = α * E - γ * I  
dR/dt = γ * I  
dC/dt = α * E

Where:

- **S**: Susceptible population
- **E**: Exposed (infected but not yet infectious)
- **I**: Infectious individuals
- **R**: Recovered individuals
- **C**: Cumulative reported cases
- **N**: Total population
- **β**: Transmission rate
- **α**: Rate of becoming infectious
- **γ**: Recovery rate
---

## ⚙️ Nominal Parameters

| Parameter | Value         | Description                  |
|----------:|:--------------|:-----------------------------|
| β | 14/9 ≈ 1.56   | Transmission rate            |
| α | 7/3 ≈ 2.33    | Rate from exposed to infected |
| γ | 7/9 ≈ 0.78    | Recovery rate                |
| I₀ | 1000           | Initial number of infectives |
| N | 80,000,000     | Total population             |
| T | 60 weeks       | Simulation duration          |

---

## 📊 Tasks Implemented

### ✅ Task 1–3: Nominal Simulation
- Solves SEIR with `C(t)` using nominal parameters.
- Plots `S(t), E(t), I(t), R(t)` and `C(t)` over time.

### ✅ Task 4: Define Hypercubes
- Perturbation sets defined as:
  - \( H_1 \): ±5% around nominal parameters
  - \( H_2 \): ±10% around nominal parameters

### ✅ Task 5–6: ODE System & Numerical Integration
- ODE solver (`solve_ivp`) integrates the SEIR+C system.
- Weekly timepoints are extracted for sampling.

### ✅ Task 7: Initial Conditions
- Uses \( I₀ = 1000 \), and computes corresponding `E0`.
- Sets initial `R0 = 0`, `C0 = I0`, and `S0 = N - E0 - I0`.

### ✅ Task 8: Sample 1000 Parameter Sets
- Uniform sampling within `H1` and `H2` using Monte Carlo.

### ✅ Task 9: Plotting Distribution of `C(t)`
- Shows:
  - Mean
  - Median
  - 95% quantile band (uncertainty)

### ✅ Task 10–11: Quantity of Interest (QoI) Analysis
- **G1**: Final cumulative cases \( C(T) \)
- **G2**: Time to peak infectious cases \( maximum of I(t) \)
- Plots histograms of G1 and G2.

### ✅ Task 12: Correlation Analysis
- Computes Pearson correlation between G1 and G2.
- Offers insight into dependency between metrics.

### ✅ Task 13: Intuitive Interpretation

> This model shows how an infectious disease might spread in a large population like Germany’s. We start with estimates for how contagious the disease is and how long it lasts. Then, we simulate what would happen if these estimates were slightly off—say, 5% or 10% higher or lower. We repeat the simulation 1000 times with these variations and look at the spread of outcomes. This helps us understand how uncertain the predictions might be. Two important results we look at are how many people eventually got infected and when the peak of the outbreak happens.

---

## 📈 Output Examples

- **SEIR Dynamics**: Time series of compartments
- **C(t) Distribution**: Mean ± 95% interval
- **Histograms**:
  - Final cumulative cases `C(T)`
  - Time of infection peak
- **Statistical Metrics**:
  - 2.5% and 97.5% quantiles for G1, G2
  - Pearson correlation between G1 and G2

---

## 🧪 Requirements

- Python 3.8+
- Packages:
  - `numpy`
  - `scipy`
  - `matplotlib`
  - `tqdm`

Install dependencies:

```bash
pip install -r requirements.txt
