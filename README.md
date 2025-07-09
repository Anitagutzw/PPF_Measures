# PPF-Measures

This repository contains the Python code and resources related to the Master's thesis "Quantitative Measures of Drug Resistance Using Stochastic Processes" by Anita Gutzwiller, supervised by Prof. Dr. Riccardo Gatto at the University of Bern.

The thesis introduces a novel mathematical framework that bridges stochastic process theory, coherent risk measures, and clinical decision-making to address timing-related uncertainties in medical treatment, particularly focusing on drug resistance.

## Installation

You can install the `ppf_measures` package using pip:

```bash
pip install ppf_measures
```

**Prerequisites:** This package depends on `ppf_approx`. Please ensure `ppf_approx` is installed beforehand. You can find installation instructions for `ppf_approx` at [jarmsmagalang/ppf\_approx](https://github.com/jarmsmagalang/ppf_approx). 

## Usage

This package provides functions for computing Value at Risk (VaR) and Tail Value at Risk (TVaR) of first-passage times using two different approaches: PPF Approximation and HMRA Simulation.

### PPF Approximation

The PPF approximation method calculates VaR and TVaR by leveraging Pade approximations of the first-passage time probability density.

#### `value_at_risk`

```python
value_at_risk(m_ord, n_ord, v, D, x0, r, tval, p, tol=1e-12, maxiter=500)
```

**Parameters:**

  * `m_ord` (Integer): Numerator order of the Pade approximation.
  * `n_ord` (Integer): Denominator order of the Pade approximation.
  * `v` (Float): Drift constant.
  * `D` (Float): Diffusion constant. Must be positive.
  * `x0` (Float): Initial position. Must be from $0 \\le x\_0 \< 1$.
  * `r` (Float): Resetting rate. Must be non-negative.
  * `tval` (Array): Range of time values for evaluation.
  * `p` (Float): The probability threshold  (e.g., 0.95 for 95% VaR).
  * `tol` (Float, optional): The tolerance for convergence of the Newton-Raphson method. Default is $1 \\times 10^{-12}$.
  * `maxiter` (Integer, optional): The maximum number of iterations for the Newton-Raphson method. Default is 500.

**Returns:**

  * `Float`: The Value at Risk (VaR) corresponding to the probability `p`. VaR represents the maximum possible loss over a specific time horizon at a given confidence level.

#### `tail_value_at_risk`

```python
tail_value_at_risk(m_ord, n_ord, v, D, x0, r, tval, p, tol=1e-12, maxiter=500)
```

**Parameters:**

  * `m_ord` (Integer): Numerator order of the Pade approximation.
  * `n_ord` (Integer): Denominator order of the Pade approximation.
  * `v` (Float): Drift constant.
  * `D` (Float): Diffusion constant. Must be positive.
  * `x0` (Float): Initial position. Must be from $0 \\le x\_0 \< 1$.
  * `r` (Float): Resetting rate. Must be non-negative.
  * `tval` (Array): Range of time values for evaluation.
  * `p` (Float): The probability threshold for TVaR (e.g., 0.95 for 95% TVaR).
  * `tol` (Float, optional): The tolerance for convergence. Default is $1 \\times 10^{-12}$.
  * `maxiter` (Integer, optional): The maximum number of iterations for Newton-Raphson. Default is 500.

**Returns:**

  * `Float`: The Tail Value at Risk (TVaR) corresponding to the probability `p`. TVaR, also known as Conditional Value at Risk (CVaR), is the expected loss given that the loss is greater than or equal to the VaR.

### HMRA Simulation

The HMRA simulation method computes VaR and TVaR by simulating first-passage times.

#### `simulate_var_tvar`

```python
simulate_var_tvar(v, D, x0, eps, eul_dt, p, r_values, n_samples, max_fail_ratio)
```

**Parameters:**

  * `v` (Float): Drift constant.
  * `D` (Float): Diffusion constant.
  * `x0` (Float): Initial position.
  * `eps` (Float): Accuracy threshold for HMRA.
  * `eul_dt` (Float): Time step for Euler simulation.
  * `p` (Float): Confidence level for VaR/TVaR (e.g., 0.95).
  * `r_values` (array\_like): Array of resetting rate values to evaluate.
  * `n_samples` (Int): Number of simulation samples per `r`.
  * `max_fail_ratio` (Float): Maximum allowed ratio of failed samples for a valid result.

**Returns:**

  * `var_values` (list of float): Value at Risk values for each `r`. VaR represents the maximum possible loss over a specific time horizon at a given confidence level.
  * `tvar_values` (list of float): Tail Value at Risk values for each `r`. TVaR, also known as Conditional Value at Risk (CVaR), is the expected loss given that the loss is greater than or equal to the VaR.
