# Predicting Loneliness Beyond Social Contact Frequency

Evidence from the European Social Survey (ESS) Round 7.

## Background

Loneliness can occur despite frequent social contact. Using ESS Round 7 data
(N = 37,868; 21 countries), this project tests whether confidant availability and
perceived social activity relative to age peers improve prediction of loneliness
beyond contact frequency and background characteristics.

## Repository structure

```
analysis_script/
  Model_fitting.Rmd    # model fitting, importance, partial dependence
  IPV_analysis.Rmd     # incremental predictive value
  ESS7e02_3.csv        # data
  func/                # helper functions
draft_materials/
  draft.tex            # manuscript
  *.png                # figures
```

## Requirements

R 4.4.1.

Tested with:

| Package       | Version    |
|---------------|------------|
| ordinal       | 2025.12.29 |
| ordinalForest | 2.4.4      |
| pdfCluster    | 1.0.4      |
| psych         | 2.6.9      |
| ggplot2       | 4.0.0      |
| iml           | 0.11.4     |

The `func/` scripts additionally require `ranger`, `dplyr`, and `pracma`.

```r
install.packages(c("ordinal", "ordinalForest", "pdfCluster", "psych",
                   "ggplot2", "iml", "ranger", "dplyr", "pracma"))
```

## Usage

Place `ESS7e02_3.csv` and the `func/` folder in the working directory.

### Model fitting, importance, and partial dependence

Run `analysis_script/Model_fitting.Rmd`. It performs:

- five-fold cross-validated fitting (CLM, CLMM, ordinal forest, OMERF, majority baseline);
- full-sample fitting of the selected model;
- permutation importance of the predictors;
- partial dependence plots.

### Incremental predictive value

Run `analysis_script/IPV_analysis.Rmd`. It computes the incremental predictive value
of the two social-connection predictors over a baseline of meeting frequency and
background covariates (nested ordinal forests, five-fold cross-validation).
