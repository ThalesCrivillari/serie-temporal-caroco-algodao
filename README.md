# Time Series Analysis — Cotton Seed Price (Mato Grosso, Brazil)

Modeling the historical price series of cotton seed in Mato Grosso, aiming to understand its dynamics and forecast future values. Project P2 for the course **ME607 — Time Series** (IMECC/Unicamp).

## About

Cotton seed is a by-product of cotton ginning, and its price follows the cotton harvest cycle in Mato Grosso, Brazil's largest producer. This project analyzes the monthly commercialization price series (source: IMEA/MT, Jan/2023 to Apr/2026) and fits a model for short-term forecasting.

The central question is: **can we model and forecast the cotton seed price from its own history?**

## Models

| Model | Role | Method |
|-------|------|--------|
| **SARIMA** | Main model | Maximum likelihood |
| **Hybrid SARIMA→BTVC** | Complement | MCMC (PyMC) |
| **Hierarchical (by crop season)** | Complement | MCMC (PyMC) |

The **SARIMA(1,1,0)(1,0,0)₁₂** is the main model, selected via information criteria (AICc). The complementary models explore, respectively, time-varying coefficients and the price difference between crop seasons.

## Repository structure

```
├── caroco_p2.csv              # Data (monthly price by crop season)
├── programa_p2.ipynb          # Notebook reproducing the full analysis
├── relatorio_p2.tex           # Report (LaTeX, in Portuguese)
├── fluxograma_metodologia.png # Methodology flowchart
└── README.md
```

## The data

The file `caroco_p2.csv` has three columns:

- `data` — reference month
- `safra` — corresponding crop season (22/23, 23/24, 24/25)
- `preco_rs_ton` — price in BRL per ton

During crop-season transitions there are two rows for the same date (one per season); the program averages these seasons to build a single monthly series.

## How to run

1. Open `programa_p2.ipynb` in [Google Colab](https://colab.research.google.com/)
2. Run the first cell to install dependencies (`pymc`, `arch`, `statsmodels`)
3. When prompted, upload `caroco_p2.csv`
4. Run all cells (`Runtime → Run all`)

The notebook produces all figures and numerical results. MCMC estimation of the Bayesian models takes a few minutes.

## Methodology

1. Pre-processing (averaging crop seasons)
2. Exploratory analysis (classical decomposition via moving averages)
3. Stationarity testing (ADF and KPSS)
4. SARIMA identification and estimation
5. Residual diagnostics
6. Out-of-sample forecasting exercise
7. Complementary models (hybrid and hierarchical)

## Tech stack

Python · pandas · statsmodels · PyMC · matplotlib
