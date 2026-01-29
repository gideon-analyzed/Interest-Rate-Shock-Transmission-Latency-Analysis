# Interest Rate Shock Transmission Latency Analysis  
*Quantifying Monetary Policy Impact on Equity Markets Using Event Study Methodology*

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python)
![Pandas](https://img.shields.io/badge/Pandas-Data_Analysis-green)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)

A rigorous quantitative finance research project analysing how Federal Reserve monetary policy decisions transmit to NASDAQ equity markets. This analysis quantifies the critical time lag between interest rate shocks and market reactions—essential intelligence for algorithmic trading systems, risk management frameworks, and monetary policy forecasting.

## 🔬 Core Research Finding

**Markets require 7.74 days (mean) to reach 50% of maximum response** following Federal Reserve interest rate decisions, with a median latency of 6 days. This transmission latency represents a systematic inefficiency that quantitative trading strategies can exploit while posing material risk to banks' real-time risk models.

## 💼 Business Impact for Financial Institutions

| Insight | Quantified Impact | Strategic Application |
|---------|-------------------|----------------------|
| **Transmission Latency** | 7.74 days mean to 50% market response | Optimal entry timing for rate-sensitive strategies: 1-2 days post-announcement |
| **Volatility Surge** | +38.3% average volatility increase following shocks | Dynamic risk limit adjustments required within 24 hours of FOMC announcements |
| **Shock Magnitude Irrelevance** | Near-zero correlation (-0.038) between shock size and volatility | Risk models must treat all rate changes as high-volatility events regardless of magnitude |
| **Cross-Asset Transmission** | Gold shows inverse correlation (-0.42) during high-volatility regimes | Portfolio rebalancing protocol: increase gold allocation by 5-8% during rate shock periods |

## ⚙️ Methodology Highlights

### Event Study Design (Academic Rigour)
- **25 FOMC announcement days** analysed with 10-day pre/post windows (2010-2024)
- **Z-score thresholding** (|Z| > 3) to isolate statistically significant market reactions
- **Winsorisation** at 1st/99th percentiles to handle extreme outliers while preserving distribution shape
- **Standard error of means** calculated across announcement events for confidence intervals

### Advanced Feature Engineering
```python
# Critical latency metric calculation
def calculate_transmission_latency(returns_window, threshold=0.5):
    """
    Quantifies days required to reach specified % of maximum market response
    Directly applicable to algorithmic trading entry timing optimisation
    """
    cumulative_response = returns_window.cumsum()
    max_response = cumulative_response.max()
    threshold_response = max_response * threshold
    
    # Return days to threshold (critical for trading strategy design)
    latency_days = (cumulative_response >= threshold_response).idxmax()
    return latency_days
```

### Statistical Validation
- **Shapiro-Wilk normality testing** on residuals (p=0.5893 confirms normality)
- **Cross-asset correlation matrices** across 7 asset classes (equities, commodities, FX)
- **Lagged correlation analysis** to identify optimal hedging timeframes
- **Volatility clustering detection** using GARCH-inspired methodology

## 📊 Key Results Summary

| Metric | Value | Significance |
|--------|-------|--------------|
| **Mean Transmission Latency** | 7.74 days | Critical for position sizing in rate-sensitive strategies |
| **Median Latency** | 6 days | More robust measure for algorithmic trading systems |
| **Volatility Increase** | +38.3% (average) | Requires immediate risk limit adjustments |
| **Announcement Day Return** | +0.457% (average) | Statistically significant positive drift |
| **Shock Magnitude Correlation** | -0.038 | Shock size does NOT predict volatility impact |

## 🏦 Direct Relevance to Banking Risk Management

This research directly addresses critical challenges faced by Lloyds Banking Group and other financial institutions:

✅ **Real-time Risk Model Gaps**: Most bank risk systems assume instantaneous market reactions—this analysis proves 7.74-day latency creates material model risk during monetary policy transitions

✅ **Trading Book Vulnerability**: Positions marked-to-market using stale assumptions during transmission windows face unrecognised P&L volatility

✅ **Regulatory Capital Implications**: Basel III/IV frameworks require accurate volatility forecasting—ignoring transmission latency underestimates capital requirements during policy shifts

✅ **Algorithmic Trading Edge**: Systematic strategies exploiting the 1-2 day optimal entry window post-announcement generate alpha while markets remain inefficient

## 🛠️ Technical Implementation

- **Primary Stack**: Python 3.9, Pandas (time-series optimised), NumPy, SciPy
- **Data Sources**: Yahoo Finance API (NASDAQ, FTSE 100), Federal Reserve Economic Data (FRED)
- **Statistical Methods**: Event studies, lagged correlations, volatility clustering analysis
- **Data Engineering**: Winsorisation pipelines, forward/backward filling with market holiday awareness, decimal precision standardisation (4 decimal places for financial accuracy)
- **Reproducibility**: Fully parameterised analysis with configuration-driven event windows

## 📁 Repository Structure

```
src/
├── config.py              # FOMC dates, asset tickers, analysis parameters
├── data_loader.py         # Market data ingestion with holiday alignment
├── event_study.py         # 10-day window construction around FOMC events
├── latency_analysis.py    # Transmission latency metric calculation (core innovation)
├── volatility_analysis.py # Volatility surge quantification and clustering
└── visualization.py       # Professional financial charts (Bloomberg-style)
```

## ▶️ Quick Start

```bash
# Install dependencies
pip install -r requirements.txt

# Run complete analysis pipeline
python -m src.latency_analysis --start_date 2010-01-01 --end_date 2024-01-01

# View results
cat results/latency_metrics.csv
```

## 📚 Methodology Documentation

Full academic methodology documented in [`documentation/methodology.md`](documentation/methodology.md) including:
- FOMC event selection criteria
- Statistical significance testing framework
- Data cleaning protocols for financial time series
- Limitations and robustness checks

## ⚠️ Important Notice

> This research is for educational and professional demonstration purposes. While based on rigorous quantitative methods, it should not be used as the sole basis for live trading decisions without additional validation and risk controls. Monetary policy transmission dynamics evolve with market structure changes.

## 💡 Why This Matters to Quantitative Employers

This project demonstrates **production-ready quantitative research capabilities** that translate directly to banking roles:

🔹 **Statistical Rigour**: Event study methodology with proper significance testing—not just curve-fitting  
🔹 **Financial Domain Knowledge**: Understanding of monetary policy mechanics and market microstructure  
🔹 **Risk-Aware Design**: Explicit quantification of model limitations and transmission uncertainties  
🔹 **Business Translation**: Converting latency metrics into actionable trading/risk management protocols  
🔹 **Production Mindset**: Data engineering practices (winsorisation, holiday alignment) matching institutional standards  

*Developed as part of BSc Data Science & AI coursework at University of Portsmouth. All analysis follows CFA Institute standards for quantitative research integrity.*

---

© 2025 Paul Gideon Wabwire
