# Financial Portfolio Optimization

## Introduction

This project explores the construction and optimization of a financial portfolio using historical stock data from Yahoo Finance. By analyzing a diverse selection of companies across the technology, automotive, and entertainment sectors, we aim to understand how asset returns, volatility, and correlation influence overall portfolio performance.

Through simulation and performance analysis, we evaluate thousands of randomly generated portfolios and identify the most efficient investment strategies based on expected return, volatility, and risk-adjusted performance using the Sharpe Ratio.

---

## Project Objectives

- **Import & Clean Data**: Retrieve historical stock prices from Yahoo Finance and prepare for analysis.
- **Visualize & Analyze**: Plot trends, compute log returns, volatility, and inter-asset relationships.
- **Simulate Portfolios**: Generate random portfolios to explore diversification and risk-return tradeoffs.
- **Optimize Performance**: Identify portfolios with minimum volatility and maximum Sharpe ratio using real risk-free rates.
- **Evaluate Contributors**: Analyze which assets drive portfolio return and risk.
- **Compare Strategies**: Contrast optimized portfolios and summarize investment insights.

---

## Data

- **Source**: Yahoo Finance API (`yfinance`) for daily historical stock prices (April 2019 – April 2024)
- **Assets**: AAPL, AMD, AMZN, DIS, META, MSFT, NFLX, NVDA, TSLA
- **Risk-Free Rate**: 3-month U.S. Treasury Bill rate pulled from FRED (`pandas_datareader`)
- **Metrics Computed**: Log returns, annualized volatility, portfolio variance, Sharpe Ratio

---

## Section 1: Data Processing & Visualization

Historical stock price data was imported, cleaned, and aligned using daily close values. The prices were visualized through time-series plots to show absolute performance trends. Subplots were also created to observe individual behavior per stock. This section laid the groundwork for return calculations by establishing a clean dataset and visual context for performance comparison.

---

## Section 2: Risk & Return Analysis

This section computed log returns, annualized volatility, variances, and covariances to evaluate each asset’s risk profile. Heatmaps were used to visualize inter-stock relationships in terms of return correlation and covariance. These metrics set the stage for understanding how diversification affects overall portfolio volatility and informed our next step: simulation-based optimization.

---

## Section 3: Portfolio Optimization

Using random sampling, 100,000 unique portfolios were generated with varying asset weight combinations. Each portfolio was evaluated based on expected return, volatility, and Sharpe Ratio.

- **Minimum Volatility Portfolio**:  
  - Return: **15.8%**, Volatility: **27.0%**

- **Maximum Sharpe Ratio Portfolio**:  
  - Return: **42.0%**, Volatility: **39.1%**, Sharpe Ratio: **1.02**

These portfolios were plotted on the **Efficient Frontier**, with the optimal configurations highlighted.

To better understand the portfolio composition, I broke down the **top 5 contributors to both return and risk**. NVIDIA and Tesla dominated both sides of the portfolio equation, confirming the strategy’s tech-heavy, high-growth tilt. Bar charts were used to visualize the contribution breakdown, reinforcing the importance of thoughtful weight allocation and diversification.

---

## Conclusion

This project demonstrated how quantitative techniques can be used to construct and evaluate optimized portfolios based on real financial data. By simulating 100,000 potential portfolios and analyzing performance through key metrics like expected return, volatility, and the Sharpe Ratio, we identified both stable and high-performing investment strategies.

Key takeaways:
- A small number of assets can dominate a portfolio’s risk-return profile.
- Portfolio optimization isn’t just about returns—it’s about finding the right balance of performance and stability.
- Realistic inputs like FRED-sourced Treasury rates add credibility and context to risk-adjusted metrics.

Based on the results of the optimal Sharpe Ratio portfolio, **NVIDIA**, **Tesla**, and **Apple** stood out as high-conviction assets that contributed most significantly to return while justifying their risk. These stocks may offer strong growth potential in a well-diversified, performance-oriented portfolio.