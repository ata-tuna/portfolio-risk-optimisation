# Quantitative Portfolio Risk & Optimisation Analysis

## Overview

This project analyses the historical risk and performance of a multi-asset portfolio using Python. It compares a manually constructed portfolio with the S&P 500 and investigates whether quantitative portfolio optimisation can improve risk-adjusted performance.

The analysis uses historical market data from 2016–2026 and includes portfolio performance metrics, correlation and covariance analysis, Monte Carlo portfolio simulation, and an out-of-sample test of optimised allocations.

## Portfolio

The manually selected portfolio consists of:

- SPY — S&P 500 ETF
- MSFT — Microsoft
- JPM — JPMorgan Chase
- CAT — Caterpillar
- VWO — Vanguard FTSE Emerging Markets ETF
- GLD — SPDR Gold Shares
- IEF — iShares 7–10 Year Treasury Bond ETF

The initial weights were selected before analysing historical portfolio performance.

## Methodology

The analysis includes:

- Historical adjusted market prices sourced using `yfinance`
- Daily asset and portfolio returns
- Compound annual growth rate (CAGR)
- Annualised volatility
- Sharpe ratio using historical US Treasury bill rates from FRED
- Maximum drawdown
- Asset correlation and covariance analysis
- Comparison against SPY as a passive benchmark
- Monte Carlo simulation of 10,000 long-only portfolio allocations
- Identification of maximum-Sharpe and minimum-volatility portfolios
- Out-of-sample testing using a 2016–2021 training period and 2022–2026 test period

## Key Findings

Over the full historical period, the manually constructed portfolio achieved a CAGR of approximately 15.4%, compared with 15.2% for SPY, while exhibiting lower volatility and maximum drawdown.

The full-period maximum-Sharpe portfolio achieved stronger in-sample risk-adjusted performance, although this result is affected by using the same historical data for portfolio selection and evaluation.

To provide a more realistic test, portfolio weights were subsequently selected using only 2016–2021 data and evaluated over the unseen 2022–2026 period. The training-period maximum-Sharpe portfolio achieved an out-of-sample Sharpe ratio of approximately 0.75, compared with 0.73 for the manual portfolio and 0.53 for SPY. The manual portfolio nevertheless achieved the highest out-of-sample CAGR of approximately 13.3%.

These results highlight both the potential diversification benefits of portfolio construction and the limitations of relying on historical optimisation.

## Technologies

- Python
- pandas
- NumPy
- Matplotlib
- yfinance
- Jupyter Notebook
- Federal Reserve Economic Data (FRED)

## Limitations

The analysis relies on historical returns and covariance estimates, which may not represent future market conditions. Transaction costs, taxes and other implementation costs are excluded. The simulated portfolios are long-only and restricted to the selected asset universe.

The full-period optimisation is evaluated in-sample and is therefore susceptible to overfitting. The train/test analysis reduces this issue but does not eliminate it, as a single out-of-sample period cannot establish that a strategy will generalise across future market environments.

## Running the Project

Install the required Python packages:

```bash
pip install pandas numpy matplotlib yfinance jupyter