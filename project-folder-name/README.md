# Forecasting CPI Using Rent Data (ZORI) and Time Series Models

## Introduction

With inflation affecting everything from groceries to rent, understanding how housing costs contribute to overall price levels has become increasingly important. During my time studying economics and data science, I became curious about how rental market trends—particularly Zillow’s Observed Rent Index (ZORI)—could be used to predict inflation indicators such as the Consumer Price Index (CPI).

This project explores the relationship between ZORI and CPI using time series forecasting methods. Specifically, it tests whether past rent trends can improve CPI forecasting using both univariate and multivariate approaches, including ARIMA and Vector Autoregression (VAR).

### Key Objectives:
1. **Data Preparation**: Clean and align Zillow ZORI and U.S. CPI datasets, both available from April 2015 to September 2022.
2. **Time Series Forecasting**: Build and evaluate ARIMA models to forecast CPI based on historical CPI trends.
3. **Multivariate Time Series Modeling**: Introduce rent data (ZORI) into a VAR model to jointly forecast both CPI and rent, testing if a multivariate approach improves forecast accuracy.

---

## Data

- **ZORI**: Zillow Observed Rent Index (ZORI), monthly rent estimates measured on the last day of each month.
- **CPI**: U.S. Consumer Price Index, seasonally adjusted and measured on the first day of each month.
- **Timeframe**: April 2015 to September 2022 (90 monthly observations total).
- Datasets were joined using CPI's 1st-of-month timestamp as the common index to ensure alignment.

---

## Section 1: Data Processing

The datasets were aligned and combined into a single time series indexed by monthly dates. CPI was already seasonally adjusted, so no additional adjustments were made. Log transformations were applied to both ZORI and CPI to stabilize variance and normalize the data before modeling.

---

## Section 2: Time Series Modeling with ARIMA

I started by building univariate ARIMA models using only CPI data. After tuning the order of differencing and testing various combinations of ARIMA(p,d,q) parameters, I found that **ARIMA(2,3,1)** yielded the best performance, achieving an RMSE of **3.37**, which was lower than the baseline ARIMA(1,1,1) RMSE of **4.03**.

Although ARIMA(2,3,1) improved the forecast, it still did not incorporate external indicators like rent trends. This limitation motivated a multivariate approach using Vector Autoregression (VAR), where multiple time series can influence each other.

---

## Section 3: Multivariate Time Series Modeling with VAR

After preparing log-transformed and stationary versions of both CPI and ZORI, I applied a VAR model to jointly forecast both. The series required two rounds of differencing to achieve stationarity, confirmed using the Augmented Dickey-Fuller test.

The optimal lag order was determined to be **3**, based on AIC and BIC criteria. Residual diagnostics using the Durbin-Watson statistic confirmed that autocorrelation was minimal in both CPI and ZORI components.

Forecasts were generated for the next 4 months (June to September 2022) and evaluated using RMSE:

- **log CPI RMSE**: **0.0326**
- **log ZORI RMSE**: **0.0213**

---

## Conclusion

After evaluating both approaches, the VAR model outperformed the standalone ARIMA model in terms of precision. While the ARIMA(2,3,1) model achieved an RMSE of **3.37** on raw CPI values, the VAR model, using log-transformed and differenced series, reached a much lower RMSE of **0.0326** for log CPI and **0.0213** for log ZORI.

This project highlights how including economic indicators like rent can improve inflation forecasting. It also reinforced the importance of proper data preprocessing, stationarity checks, model diagnostics, and selecting the appropriate modeling approach. By combining economic reasoning with time series analysis, we showed how multivariate models can capture relationships that improve forecast accuracy.
