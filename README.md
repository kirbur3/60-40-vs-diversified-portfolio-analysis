# 60/40 vs. Diversified Portfolio Risk and Return Analysis

Personal project asking "Is the 60/40 portfolio still enough?" Compares a classic 60/40 portfolio against a diversified six-ETF mix using 11+ years of daily adjusted closing prices (January 2015 to September 2026).

**Tools:** Python (pandas, NumPy, Matplotlib, yfinance), SQL (SQLite), Google Colab

## Data and Setup

* Six ETFs: SPY (US stocks), VXUS (international stocks), AGG (bonds), VNQ (real estate), GLD (gold), BIL (cash/T-bills).
* Pulled 2,950 trading days of adjusted closing prices with yfinance. No missing values.
* Stored prices in SQLite in long format (17,700 rows) and calculated daily returns in SQL using the `LAG()` window function (2,949 returns per ETF).
* Used BIL's annualized return (about 2.0%) as the risk-free rate.

## Portfolios

* **60/40:** 60% SPY, 40% AGG
* **Diversified:** 40% SPY, 15% VXUS, 25% AGG, 5% VNQ, 10% GLD, 5% BIL
* Weights are held fixed each day (daily rebalancing).

## Metrics

* Built a reusable `calc_metrics(returns, rf)` function computing total return, annualized return, annualized volatility, Sharpe ratio, max drawdown, and 95% historical VaR.
* Validated the function against step-by-step calculations for all six ETFs.

## Full-Period Results

| Metric | 60/40 | Diversified |
|---|---|---|
| Annualized return | 9.15% | 9.06% |
| Annualized volatility | 10.95% | 10.70% |
| Sharpe ratio | 0.657 | 0.664 |
| Max drawdown | -21.7% | -22.2% |
| Growth of $1 | $2.79 | $2.76 |

* The two portfolios ended almost tied over the full period.

## Stress Tests

* **Covid crash (Feb 19 to Mar 23, 2020):** 60/40 lost slightly less (-21.5% vs. -22.0%). This was the worst drop for both portfolios over the full period.
* **2022:** Diversified lost less (-13.9% vs. -15.6%). Stocks and bonds fell together (SPY -18%, AGG -13%), while gold and cash stayed about flat (GLD -0.8%, BIL +1.4%).

## Charts

* Growth of $1 and drawdown charts in Matplotlib, with the Covid crash and 2022 shaded.
* 60/40 did slightly better before and during Covid and in 2026, while Diversified held up better from 2022 until late 2025.

## Conclusion

60/40 is still a solid choice, but it depends on bonds protecting against stock drops. When that breaks down, as it did in 2022, spreading money across more assets can help. Diversifying didn't beat 60/40 overall, but it changed when and how the losses happened.

Extra Files: 60_40_vs_Diversified_Portfolio_Risk_and_Return_Analysis.ipynb
