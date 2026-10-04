# Quantitative Portfolio Risk & Optimisation Analysis

This project evaluates whether quantitative portfolio optimisation improves the risk-adjusted performance of a manually constructed multi-asset portfolio. It compares the portfolio with the S&P 500, explores 10,000 long-only allocations and tests optimised weights on unseen data.

## Key findings

### Full historical period (2016–2026)

| Strategy | CAGR | Annualised volatility | Sharpe ratio | Maximum drawdown |
|---|---:|---:|---:|---:|
| Manual portfolio | 15.4% | 13.3% | 0.98 | -23.3% |
| SPY | 15.2% | 17.8% | 0.76 | -33.7% |

The manual portfolio produced a similar return to SPY with lower volatility and a smaller drawdown. The full-period maximum-Sharpe allocation achieved a Sharpe ratio of 1.25, but this is an in-sample result and is therefore vulnerable to overfitting.

### Out-of-sample period (2022–2026)

| Strategy | CAGR | Sharpe ratio |
|---|---:|---:|
| Manual portfolio | 13.3% | 0.73 |
| SPY | 12.3% | 0.53 |
| Training-period maximum Sharpe | 11.8% | 0.75 |
| Training-period minimum volatility | 8.0% | 0.47 |

The training-period maximum-Sharpe portfolio retained a marginally higher Sharpe ratio out of sample, but the manual portfolio achieved the highest return. The result illustrates both the value of diversification and the sensitivity of optimised weights to the estimation period.

![Out-of-sample cumulative portfolio performance](figures/out_of_sample_performance.png)

## Portfolio

The manual portfolio contains seven assets:

| Asset | Exposure | Weight |
|---|---|---:|
| SPY | S&P 500 ETF | 30.0% |
| MSFT | Microsoft | 12.5% |
| JPM | JPMorgan Chase | 10.0% |
| CAT | Caterpillar | 7.5% |
| VWO | Vanguard FTSE Emerging Markets ETF | 10.0% |
| GLD | SPDR Gold Shares | 10.0% |
| IEF | iShares 7–10 Year Treasury Bond ETF | 20.0% |

The weights were selected before examining historical portfolio performance.

## Methodology

- Download adjusted daily prices using `yfinance`.
- Calculate CAGR, annualised volatility, maximum drawdown and Sharpe ratios.
- Use the three-month US Treasury bill yield from FRED as the risk-free rate.
- Analyse asset correlations and covariances.
- Generate 10,000 random long-only portfolios and identify the maximum-Sharpe and minimum-volatility allocations.
- Estimate optimised weights using 2016–2021 data and evaluate them over 2022–2026.

![Simulated portfolio risk-return opportunity set](figures/risk_return_opportunity_set.png)

## Repository structure

```text
portfolio-risk-optimisation/
├── figures/                    # Charts exported by the notebook
├── portfolio_analysis.ipynb    # Complete analysis and interpretation
├── requirements.txt            # Python dependencies
└── README.md
```

## Running the project

```bash
git clone https://github.com/ata-tuna/portfolio-risk-optimisation.git
cd portfolio-risk-optimisation
python -m venv .venv
source .venv/bin/activate       # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook portfolio_analysis.ipynb
```

Running the notebook downloads current source data, reproduces the analysis and updates the charts in `figures/`.

## Data sources

- Market prices: [Yahoo Finance](https://finance.yahoo.com/) through `yfinance`
- Risk-free rate: [FRED three-month Treasury bill secondary-market rate (DTB3)](https://fred.stlouisfed.org/series/DTB3)

## Limitations

The analysis uses historical returns and covariance estimates, which may not represent future market conditions. It excludes transaction costs, taxes and implementation constraints. The simulated portfolios are long-only and restricted to seven assets. A single train/test split reduces in-sample bias but does not establish that an allocation will generalise across other market regimes.

This project is for educational purposes and does not constitute investment advice.
