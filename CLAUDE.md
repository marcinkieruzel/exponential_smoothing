# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a time series analysis and forecasting project focused on **exponential smoothing techniques**. The project contains Jupyter notebooks that demonstrate:

1. Statistical analysis (covariance and correlation)
2. Time series visualization
3. Exponential smoothing methods (Simple, Holt's, and Holt-Winters)
4. Financial data analysis using stock market data

## Environment Setup

**Python Virtual Environment:**
- Location: `.venv/` in the project root
- Activate: `source .venv/bin/activate`
- The project uses Python 3.12

**Key Dependencies:**
- pandas
- numpy
- matplotlib
- seaborn
- yfinance (for financial data)
- statsmodels (for exponential smoothing models)
- jupyter

## Project Structure

### Main Working Directory: `workspace/`

Contains all analysis notebooks and data files:

- **Data files:**
  - `temperature.csv` - Hourly temperature data for multiple cities (2013-2017, ~45K records)
  - `xauusd_d.csv` - Gold price historical data

- **Analysis notebooks:**
  - `index.ipynb` - Main notebook with exponential smoothing demonstrations
  - `cov.ipynb` - Financial covariance analysis (Amazon, NASDAQ 100, VIX)
  - `covariance.ipynb` - VIX vs NASDAQ 100 covariance study
  - `seaborn.ipynb` - Visualization experiments

### Key Concepts Implemented

**Exponential Smoothing Methods (see `index.ipynb`):**
1. **Simple Exponential Smoothing (SES)** - For data with no trend or seasonality
2. **Holt's Linear Trend** - For data with trend but no seasonality
3. **Holt-Winters** - For data with both trend and seasonality (additive model)

**Time Series Processing:**
- Simple Moving Averages (SMA) with various window sizes
- Centered Moving Averages for seasonal decomposition
- Exponential Moving Averages (EMA)
- Data interpolation for handling missing values

**Statistical Analysis:**
- Covariance and correlation matrices
- Rolling correlations (30-day windows)
- Daily returns analysis
- Scatter plots with trend lines

## Running the Notebooks

**Start Jupyter:**
```bash
source .venv/bin/activate
jupyter notebook workspace/
```

**Running specific notebooks:**
- Main exponential smoothing examples: `workspace/index.ipynb`
- Financial covariance analysis: `workspace/cov.ipynb`

## Data Handling Patterns

**Temperature Data:**
- DateTime parsing: `pd.to_datetime(temperature['datetime'])`
- Missing value handling: Use `.interpolate()` for time series data
- Common visualization window: 24-hour rolling averages for daily patterns, 24*366 for yearly trends

**Financial Data (yfinance):**
- Typical fetch pattern: `yf.Ticker("SYMBOL").history(start=start_date, end=end_date)`
- Always check for timezone-aware datetime indices
- Data scaling may be applied (e.g., Amazon prices multiplied by 100 for comparison)

## Visualization Standards

**Matplotlib Configuration:**
- Figure sizes: `figsize=(20, 6)` for time series, `figsize=(10, 6)` for general plots
- Style: `plt.style.use('seaborn-v0_8-whitegrid')` or `'seaborn-v0_8-darkgrid'`
- Date formatting: Use `matplotlib.dates.DateFormatter` and `MonthLocator` for time axes

**Common Plot Types:**
- Line plots with legends for multiple time series
- Scatter plots for correlation visualization
- Dual-axis plots (twinx) for comparing different scales
- Rolling correlation plots to show relationship changes over time

## Important Notes

- The project analyzes relationships between market volatility (VIX) and indices (NASDAQ 100)
- VIX typically shows **negative correlation** with stock indices (inverse relationship)
- When working with financial data, always align dates before calculating covariance/correlation
- Temperature data has significant missing values - use interpolation before analysis
