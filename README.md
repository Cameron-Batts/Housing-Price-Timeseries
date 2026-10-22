# Housing Price Growth Forecasting and Historical Validation

**Author:** Cameron Batts

## Validation update - October 22, 2026

The revised offline R workflow executed and rendered using 444 overlapping monthly observations, training through December 2013 and a 24-month 2014–2015 test window.

| Model | MAE | RMSE |
| --- | ---: | ---: |
| SeasonalNaive | 0.4776 | 0.5827 |
| ARIMA | 0.3053 | 0.3743 |
| VAR | 0.1322 | 0.1609 |

Errors are in `100 × monthly log price change`, not dollars or price levels. VAR led on this single window; that does not establish broad forecast superiority. The revised target/preprocessing differ from the archived notebooks. Historical release lags and data revisions were not reconstructed, so this is not a real-time vintage backtest.

[Aggregate validation record](Reports/validation_results.json). [Executed R workflow](Reports/executed_workflow.html) · [Recorded R environment](Reports/validated_session.txt).

Run `Rscript validation/rerun_analysis.R` from the project root.

## Problem
Compare price-growth forecasts from a seasonal baseline, ARIMA and a two-variable VAR using a fixed historical split.

## Approach
Use the included FRED CSV snapshots by default, validate uninterrupted monthly dates and calculate monthly log growth. Fit on data through December 2013 and evaluate 24 static forecast steps for January 2014–December 2015. Keep the extended historical demonstrations separately labeled.

## Historical findings and original context
The included snapshots contain 780 housing-start observations (1959–2023) and 444 price-index observations (1987–2023). They overlap for 444 consecutive months from January 1987 through December 2023 with no missing values. Fresh revised model scores are available in the validation record.

## Limitations
The extended historical notebooks seasonally adjust price growth using the full sample before the train/test split, exposing training transformations to future data. Historical bagging uses four paths; that alone does not establish robust uncertainty or better forecasts. The new offline workflow changes the growth definition and evaluation setup and has now been executed as a separate validation analysis. Granger predictability and model impulse responses do not establish structural causality. Historical release lags and data revisions are not reconstructed.

## Data
HOUSTNSA is U.S. Census Bureau/HUD housing starts, monthly, not seasonally adjusted, in thousands of units. CSUSHPINSA is the S&P national home-price index, monthly, not seasonally adjusted, January 2000=100. The bundled snapshots end in December 2023 and are not current observations. Preserve source attribution and applicable index-data terms.

## Verification
Counts and relevant numerical findings were checked independently in Python. The revised R workflow was executed and rendered during this pass. Historical images are retained separately from the revised workflow.

## Run
Install R and Pandoc (or use RStudio), then run from the repository root:
```r
source("install.R")
rmarkdown::render("Notebooks/housing_price_timeseries_offline.Rmd")
```
R package versions are recorded in Reports/validated_packages.csv and Reports/validated_session.txt. No API key is needed for the default workflow.

## Files
- [R Markdown analysis](Notebooks/housing_price_timeseries_offline.Rmd)
- [Readable analysis](Reports/housing_price_timeseries.html)
- [Portfolio report](https://cameron-batts.github.io/housing_price_timeseries.html)
- [Historical PDF](Reports/Housing%20Price%20Forecasting%20via%20Time%20Series%20%26%20VAR%20Analysis.pdf): may predate interpretation corrections.

## Extended historical demonstrations
The original `.qmd` and `.rmarkdown` files remain available for reference. They require an API key and additional packages and are not the default reproducible workflow. Their full-sample seasonal adjustment makes historical forecast comparisons exploratory. Their source attribution was not documented; the revised analysis preserves these files rather than asserting new authorship of that historical material.

## References
- [FRED housing starts, HOUSTNSA](https://fred.stlouisfed.org/series/HOUSTNSA)
- [FRED national home-price index, CSUSHPINSA](https://fred.stlouisfed.org/series/CSUSHPINSA)
