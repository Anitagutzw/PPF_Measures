# PPF-Measures
This repository contains the Python code and resources related to the Master's thesis "Quantitative Measures of Drug Resistance Using Stochastic Processes" by Anita Gutzwiller, supervised by Prof. Dr. Riccardo Gatto at the University of Bern.

The thesis introduces a novel mathematical framework that bridges stochastic process theory, coherent risk measures, and clinical decision-making to address timing-related uncertainties in medical treatment, particularly focusing on drug resistance.

# Installation
pip install ppf_measures

# Usage
The are three main functions in this package. For the computation of the two measure value at risk and tail value at risk using the FPT approximation the following two functions are used:
value_at_risk(m_ord, n_ord, v, D, x0, r, tval, p, tol=1e-12, maxiter=500)
tail_value_at_risk(m_ord, n_ord, v, D, x0, r, tval, p, tol=1e-12, maxiter=500)
Here is a description of each argument:
  m_ord : Integer. Numerator order of the Pade approximation.
  n_ord : Integer. Denominator order of the Pade approximation.
  v : Float. Drift constant.
  D : Float. Diffusion constant. Must be positive.
  x0 : Float. Initial position. Must be from 0≤x0<1
  r : Float. Resetting constant. Must be non-negative.
  tval : Array. Range of time values for evaluation.
  p : Float. The probability threshold (e.g., 0.95 for 95%).
  tol : Float, optional. The tolerance for convergence. Default is 1e-12.
  maxiter : Integer, optional. The maximum number of iterations for Newton-Raphson. Default is 500.
For the computation of the two measures using the hmra simulation the following function is used: 
simulate_var_tvar(v, D, x0, eps, eul_dt, p, r_values, n_samples, max_fail_ratio)
Here is a description of each argument:
  v : Float. Drift constant.
  D : Float. Diffusion constant.
  x0 : Float. Initial position.
  eps : Float. Accuracy threshold for HMRA.
  eul_dt : Float. Time step for Euler simulation.
  p : Float. Confidence level (e.g., 0.95).
  r_values : Array_like. Array of resetting rate values to evaluate.
  n_samples : Int. Number of simulation samples per r.
  max_fail_ratio : Float. Maximum allowed ratio of failed samples for a valid result.

  # Auxiliary Functions
  ppf_integral
  ppf_approx
