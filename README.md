# REIT analyst tool

A Python notebook that pulls market data for 6 US retail and net-lease REITs, compares their performance,
risk and fundamentals, tests whether short-term returns can be predicted, and exports everything to a
formatted Excel report. Built during my MSc at Audencia.

**REITs covered:** Realty Income (O), NNN REIT (NNN), Agree Realty (ADC), W. P. Carey (WPC),
Simon Property Group (SPG), Kimco Realty (KIM).

## What the notebook does

1. **Data:** adjusted daily closing prices since 2000 from Yahoo Finance (`yfinance`).
2. **Returns:** daily, monthly and last-5-day returns, plus long-run growth with every stock indexed to 100.
3. **Sector vs rates:** US REIT sector ETF (VNQ) vs 7-10 year Treasuries (IEF) since 2024.
4. **Risk and performance KPIs:** 1-year total return, annualised volatility, maximum drawdown.
5. **Fundamentals:** market cap, P/E, price-to-book, beta, average volume, dividend yield.
6. **Correlation matrix** of daily returns across the 6 REITs.
7. **Return modelling (OLS, statsmodels):** 10-day forward return for Realty Income from price, momentum,
   volatility and macro features (VNQ and IEF returns), with a time-based train/test split to avoid look-ahead.
8. **Excel export:** one workbook with formatted tables and charts (`openpyxl`).

## Findings worth knowing

- **Short-term returns are hard to predict.** The 10-day return model scores a test R² of -0.04
  (MAE 0.031), i.e. no better than predicting the average. That is the honest result, and it matches
  what market-efficiency theory would expect from price-based features.
- A next-day *price* regression looks very accurate, but only because tomorrow's price is close to today's;
  it is included to show why returns, not prices, are the right target.
- Yahoo Finance often returns no recent dividend history for these REITs, so the dividend-yield chart can be empty.

## Run it

```bash
pip install -r requirements.txt
jupyter notebook reit_analyst_tool.ipynb
```

Needs an internet connection for Yahoo Finance. The Excel report is written to your Downloads folder.

## Stack

Python, pandas, NumPy, yfinance, statsmodels, matplotlib, openpyxl.
