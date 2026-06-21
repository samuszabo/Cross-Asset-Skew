# Cross-Asset Skew Trading Strategy

Replication and extension of the cross-asset skew trading strategy from:

- **Baltas & Salinas (2020)** — *Cross-Asset Skew* (original academic paper)
- **Dean Markwick (2024)** — [Cross Asset Skew: A Trading Strategy](https://dm13450.github.io/2024/02/08/Cross-Asset-Skew-A-Trading-Strategy.html)

## Strategy

Within each asset class, assets are ranked by their rolling 256-day return skewness.
The strategy goes **long low-skew** assets and **short high-skew** assets, rebalanced monthly.
Each class sub-portfolio is volatility-targeted to 10% annualised, then combined equally.

## Universe

5 asset classes, ~64 ETFs — an extended version of Markwick's implementation, mapping
the futures universe from Baltas & Salinas to liquid US-listed ETFs:

| Class | Instruments |
|---|---|
| Equity | 26 ETFs (US, Europe, Asia-Pacific, Emerging Markets) |
| Fixed Income | 20 ETFs (Treasuries, credit, international, EM) |
| Commodity | 16 ETFs (precious metals, energy, agriculture, industrial) |
| Real Estate | 7 ETFs |
| Currency | 9 ETFs (major FX, proxies for CME currency futures) |

## Data

Daily OHLCV bars via **Alpaca Markets API** (`alpaca-py`), dividend & split adjusted.

## Setup

```bash
pip install -r requirements.txt
```

Add your Alpaca credentials to `.env`:

```
ALPACA_API_KEY=your_key_here
ALPACA_API_SECRET=your_secret_here
```

Then open the notebook:

```bash
jupyter notebook cross_asset_skew.ipynb
```

## Notebook Structure

1. **Imports & Setup**
2. **Configuration** — asset universe, parameters
3. **Data Fetching** — Alpaca API with local cache
4. **Rolling Skew Calculation** — 256-day normalised 3rd moment
5. **Signal Construction** — monthly rank-based market-neutral weights
6. **Backtest** — vol-targeted, equal-weight combined portfolio
7. **Performance Analysis** — cumulative returns, drawdowns, Sharpe, heatmap
8. **Factor Regression** — alpha/beta vs market and equity factors
9. **Skew Premium Analysis** — long/short decomposition, skew vs forward return scatter
10. **Summary**
