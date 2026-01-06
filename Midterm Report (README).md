# Predict2Optimize — WiDS 2025  
## Midterm Report (Weeks 1–2)
### Manikarnika Sharma (24B0670)
---

**Project:** Predicting Market Dynamics for Data-Driven Portfolio Optimization  

---

## 1. Introduction

The objective of the Predict2Optimize project is to build an end-to-end pipeline that converts financial market data into portfolio decisions using prediction and optimization. The overall pipeline follows the sequence:

**data → features → prediction → optimization → backtesting**

This midterm report documents the work I have completed in **Week 1** and **Week 2**.

---

## 2. Week 1 — Financial Data & Feature Extraction

### 2.1 Data Collection

In Week 1, I began by downloading daily historical price data using the `yfinance` library. I worked with large-cap technology stocks: **AAPL, MSFT, GOOG, AMZN, TSLA**, and **NVDA**.

To study different market regimes, I used two time horizons:
- **Long-term:** 2015–2024  
- **Medium-term:** 2020–2024 (captures the COVID-19 market crash)

I extracted **Adjusted Close** prices to account for corporate actions and handled missing values using forward-fill and backward-fill to ensure continuity in the time series.

---

### 2.2 Returns, Trends, and Volatility

Using the medium-term data, I computed both **simple returns** and **log returns** over 1-day, 5-day, and 20-day horizons. I focused mainly on log returns due to their additive nature and suitability for statistical analysis.

To understand price trends, I plotted asset prices along with a **20-day moving average**, which helped smooth short-term noise and highlight medium-term behavior.

I then estimated volatility using rolling standard deviations of daily log returns with 5-day, 20-day, and 60-day windows. This revealed that volatility is not constant over time and shows clear **clustering**, with sharp spikes during market stress periods such as the COVID-19 crash.

---

### 2.3 Volume, Seasonality, and Market Behavior

To explore market microstructure effects, I analyzed the relationship between trading volume and absolute daily returns. The results showed that large price movements tend to occur on high-volume days, although high volume alone does not guarantee large returns.

I also grouped returns and volatility by calendar month to look for seasonality. The analysis did not reveal any consistent monthly patterns, suggesting that seasonal effects are weak for the selected assets.

---

### 2.4 Stationarity Analysis

Using long-term MSFT data, I examined whether log returns are stationary.

Rolling means of log returns remained close to zero, indicating a stationary mean, while rolling volatility varied significantly over time, indicating non-stationary variance.

I confirmed this using an **Augmented Dickey-Fuller test**, which produced a p-value far below 0.05. This allowed me to reject the unit root hypothesis and conclude that log returns are stationary, while volatility requires separate modeling.

---

### 2.5 Volatility Regimes

To study volatility behavior in more detail, I focused on TSLA during the early 2020 COVID-19 crash.

I compared:
- A rolling 20-day volatility estimator  
- An EWMA volatility estimator (RiskMetrics, λ = 0.94)

The EWMA estimator reacted faster and produced smoother estimates, making it more suitable for risk management. I identified high-volatility regimes by thresholding the EWMA volatility at its 60th percentile.

---

### 2.6 Time Horizons and Distributional Effects

Using NVDA data, I analyzed how return distributions change with time horizon. I computed daily, weekly, and monthly log returns and measured their skewness and kurtosis.

I observed that daily returns exhibit strong fat tails and high kurtosis, while weekly and monthly returns move closer to a normal distribution. This illustrates **aggregational Gaussianity** and highlights why normality assumptions often fail at short time scales.

---

### 2.7 Long-Term Investing Illustration

As a practical illustration, I estimated the value of a $1,000 investment in NVDA made on my birth date. I expressed the final value in terms of how many RTX 4090 GPUs could be purchased today. This exercise helped connect abstract return calculations to a tangible long-term investing outcome.

---

## 3. Week 2 — Baseline Prediction Models & Evaluation

### 3.1 Feature Construction

In Week 2, I moved from descriptive analysis to prediction. Using long-horizon data for a selected stock, I constructed features using **only past information**:
- 20-day rolling mean of returns  
- 20-day rolling volatility  
- 5-day momentum  

The prediction target was the **next-day return**.

---

### 3.2 Naive Baselines

Before using complex models, I implemented two naive baselines:
- A **zero predictor**, which always predicts zero return  
- A **rolling mean predictor**, which predicts the recent average return  

These baselines serve as reference points and help determine whether more complex models add real predictive value.

---

### 3.3 Linear and Tree-Based Models

I implemented a **linear regression model (OLS)** to establish a simple parametric benchmark. Additionally, I experimented with a **Random Forest regressor**, using depth and leaf-size constraints to reduce overfitting.

The goal at this stage was not to maximize performance but to understand how different models behave under proper evaluation.

---

### 3.4 Walk-Forward Evaluation

To evaluate the models, I used a **walk-forward (time-series) evaluation strategy** with `TimeSeriesSplit`. This ensures that training always occurs on past data and testing on future data, closely mimicking real-world deployment.

Model performance was measured using **RMSE**, and rolling RMSE plots were used to examine how prediction accuracy changes across different market regimes.

---

## 4. Key Learnings So Far

- Financial returns are approximately stationary, but volatility is not.
- Volatility clustering and regime changes are clearly visible in real data.
- Simple baselines are essential for meaningful model comparison.
- Walk-forward evaluation is critical in financial prediction to avoid look-ahead bias.
- Model performance can degrade during high-volatility periods, highlighting the importance of robust evaluation.

---

## 5. Planned Work for Upcoming Weeks

In the upcoming weeks, I plan to extend this work as follows:

- **Week 3:**  
  Train neural network models (MLP) for return prediction and implement rolling walk-forward training using PyTorch.

- **Week 4:**  
  Convert predicted returns into portfolio weights using **Markowitz mean-variance optimization**, formulate the problem in `cvxpy`, and study efficient frontiers and allocation sensitivity.

- **Week 5:**  
  Integrate prediction and optimization into a full pipeline and backtest the strategy over time, analyzing cumulative returns, risk, and limitations of the approach.
