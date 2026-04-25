# ST 453 Final Project — Bootstrap Inference for Crash Injury Severity

## Overview

This project extends the midterm analysis of NYC crash injury severity by replacing the parametric simulation study with a bootstrap-based approach. The goal is to evaluate the sampling distribution of OLS estimators and compare bootstrap inference to the parametric results from the midterm.

The analysis uses the same linear regression model and dataset, allowing for a direct comparison between parametric and nonparametric inference.

---

## Data

Source: NYC OpenData
Dataset: Motor Vehicle Collisions – Crashes

* Original dataset: ~2.2 million observations
* Analysis sample: 19,999 observations
* Response: `NUMBER.OF.PERSONS.INJURED`
* Predictors:

  * Night indicator
  * Multi-vehicle indicator
  * Borough indicators
  * Contributing factor indicators
  * Vehicle type indicators

---

## Model

A linear regression model is used:

Y = Xβ + U

* Estimated via Ordinary Least Squares (OLS)
* Implemented using base R (`qr.solve`)
* No external packages used

The model provides an interpretable approximation to the conditional mean of injury counts.

---

## Bootstrap Methodology

This project uses **residual bootstrapping**:

1. Fit OLS model on real data to obtain:

   * β̂ (estimated coefficients)
   * residuals û

2. For each bootstrap sample:

   * Sample residuals with replacement
   * Construct new response:
     Y* = Xβ̂ + u*
   * Refit OLS on (X, Y*)
   * Store estimated coefficients

3. Repeat for N bootstrap replications

4. Use bootstrap distribution to compute:

   * Sampling distributions
   * Confidence intervals (percentile method)
   * Hypothesis tests

This follows the regression bootstrap approach from lecture. 

---

## File Structure

```
.
├── bootstrap.r        # Generates bootstrap samples and saves results
├── out_file.r         # Produces figures and tables from bootstrap output
├── workflow.txt       # Steps to reproduce the full project
├── results/           # Saved R objects (.rds)
├── figures/           # Output plots
├── tables/            # Output tables
└── README.md
```

---

## How to Run

### Step 1 — Run bootstrap

```
Rscript bootstrap.r 1
```

### Step 2 — Generate outputs

```
Rscript out_file.r 1
```

### Step 3 — Compile report

Use generated figures/tables in LaTeX or R Markdown.

Full workflow is documented in:

```
workflow.txt
```

---

## Output

### Tables

* Data description
* OLS coefficient estimates
* Bootstrap summary statistics

### Figures

* Sampling distributions of coefficients
* Bootstrap RMSE distribution
* True vs mean estimated coefficients

---

## Key Analysis

The bootstrap study evaluates:

* Whether OLS estimates remain centered (unbiased)
* Variability of coefficients under resampling
* Stability of inference without Gaussian assumptions

Special focus:

* Night coefficient
* MultiVehicle coefficient

---

## Comparison to Midterm

Midterm used parametric simulation:

* Y = Xβ̂ + ε, ε ~ Normal(0, σ̂²)

Final uses bootstrap:

* Resamples empirical residuals

Key question:

* Do bootstrap confidence intervals match parametric CIs?

Example from midterm:

* Night CI ≈ (0.0583, 0.1056)

Bootstrap results should be compared directly to this benchmark.

---

## Key Findings (Expected)

* Bootstrap distributions approximately centered at β̂
* Confidence intervals similar to parametric results
* Slight differences due to:

  * Non-normality
  * Zero-inflated outcome

---

## Limitations

* Linear model applied to count data
* Zero-inflation not explicitly modeled
* Omitted variables (speed, weather, etc.)
* Bootstrap assumes residual structure is representative

---

## Requirements Compliance

This project satisfies:

* Bootstrap sampling study
* Separate `bootstrap.r` and `out_file.r` scripts
* Workflow file for reproducibility
* No external R packages used
* Full inference via bootstrap methods

All requirements follow the final project outline. 

---

## Author

Quincy Cornish
ST 453 — Advanced Computing for Statistical Reasoning
