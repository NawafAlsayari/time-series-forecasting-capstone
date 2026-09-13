[README.md](https://github.com/user-attachments/files/32166118/README.md)
# time-series-forecasting-capstone

**SDAIA Academy — Time Series Forecasting for AI Systems, January 2026 – June 2026**

**Author:** Nawaf Abdullah Alsayari
**GitHub:** [NawafAlsayari](https://github.com/NawafAlsayari)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/NawafAlsayari/time-series-forecasting-capstone/blob/main/capstone.ipynb)

---

## Project idea

A single, self-contained notebook that takes one time series from raw data to
a **validated, uncertainty-aware walk-forward forecast**:

1. Diagnose the series structure (STL, ACF/PACF, ADF).
2. Fit a classical model (Holt-Winters / ETS) and check its residuals.
3. Engineer lag/rolling/calendar features and build a recursive LightGBM
   forecast (with explicit leakage safeguards).
4. Backtest every model with an expanding-window walk-forward harness.
5. Score on raw and scale-free metrics (MASE primary, WAPE complement).
6. Produce an 80% prediction interval and report **both** coverage and width.
7. Compare model families across decision axes and recommend one for
   deployment.

All of it lives in one runnable notebook (`capstone.ipynb`) so the analysis is
reproducible end-to-end with the course's `common/metrics.py` and
`common/backtest.py` pulled in automatically.

## Dataset — and why this one

`data/retail_demand.csv` (also auto-fetched below) is long-format retail demand
across 3 regions × 2 categories, daily from 2023-01-01 to 2025-12-31. The
notebook uses the **Riyadh / Grocery** slice (`region == "Riyadh"`,
`category == "Grocery"`, column `units_sold`) as a daily Series via
`.asfreq("D")`.

Why this golden thread:

- **Riyadh/Grocery is the course's consistent "golden thread" series**, so the
  same numbers recur from lesson to lesson and the capstone can be checked
  against the labs that use it.
- **Strong weekly seasonality** (a clear weekend lift) and a **smooth yearly
  upward drift**, which is a demanding but well-behaved shape for the models
  in Sections 1–7.
- **A clean, complete 1096-day daily index** — no gaps after
  `asfreq("D")` — which lets `statsmodels`, `sktime`, and the windowed splits
  reason in calendar terms instead of row position, and makes the lag/rolling
  features meaningful.

## How to open and run

Open the notebook in Google Colab with the badge above (or
`https://colab.research.google.com/github/NawafAlsayari/time-series-forecasting-capstone/blob/main/capstone.ipynb`),
then run the cells top to bottom. The first code cell installs the libraries
and pulls the course modules and data using the same `fetch()` helper the labs
use: it finds a local `common/` and `data/` checkout if one is present, and
downloads `metrics.py`, `backtest.py`, and `retail_demand.csv` from the course
repository otherwise. No API key, token, or credential is required.

After a fresh run from top to bottom, save the notebook (File → Save a copy /
Ctrl-S) so the generated plots, tables, and printed results are captured in the
`.ipynb`.

## Repository layout

```
capstone.ipynb    # the single deliverable notebook
README.md
.gitignore
common/metrics.py           # from the course (auto-fetched)
common/backtest.py          # from the course (auto-fetched)
data/retail_demand.csv      # from the course (auto-fetched)
```

`common/` and `data/` are provided by the course repository; the notebook
resolves them automatically so you do not have to vendor them by hand.

## SDAIA Academy

[https://github.com/SDAIAAcademy](https://github.com/SDAIAAcademy)
