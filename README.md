# 📈 Automated Stock Market Portfolio Optimization & Forecasting


An end-to-end Machine Learning and Data Engineering pipeline that automatically forecasts stock prices and calculates the optimal portfolio allocation to maximize risk-adjusted returns. 

The system operates entirely in the cloud, utilizing a robust CI/CD architecture to update predictions daily and serve them through a live Streamlit dashboard.

## 🏗️ System Architecture & MLOps Pipeline

This project is built with automation and continuous deployment in mind. The pipeline executes daily without human intervention:

1. **Testing Integration (CI):** Every code push is automatically validated using **CircleCI** and `pytest` to ensure pipeline integrity before anything goes live.
2. **Continuous Deployment (CD) with GitHub Actions:** A scheduled workflow (`daily-optimisation.yml`) acts as the automated data deployment engine, waking up daily at 9:00 AM IST.
3. **Data Ingestion:** The GitHub Action fetches the latest historical stock market data using `yfinance`.
4. **Forecasting (Machine Learning):** The data is fed into Facebook's Prophet model to generate 30-day price forecasts.
5. **Optimization:** The forecasted data is processed using Scipy to calculate the Efficient Frontier and optimize portfolio weights (Markowitz Modern Portfolio Theory).
6. **Data Storage & Sync:** The freshly calculated predictions and optimal weights are pushed directly to a **Supabase (PostgreSQL)** database.
7. **Frontend Delivery:** The **Streamlit Community Cloud** dashboard instantly reflects the updated, continuously deployed data from Supabase for end-users.


## 🧮 Mathematical Foundations

The core logic of this dashboard relies on two primary mathematical concepts: time-series forecasting and mean-variance optimization.

### 1. Facebook Prophet Forecasting
Prophet is an additive regression model designed for forecasting time series data. It decomposes the time series into three main components: trend, seasonality, and holidays.

$$y(t) = g(t) + s(t) + h(t) + \epsilon_t$$

Where $g(t)$ represents the trend function (non-periodic changes), $s(t)$ represents periodic changes (weekly/yearly seasonality), $h(t)$ represents the effects of holidays, and $\epsilon_t$ is the error term.

### 2. Markowitz Portfolio Optimization (Modern Portfolio Theory)
The goal of the optimizer is to find the exact percentage of capital to allocate to each stock to maximize the **Sharpe Ratio** (the return per unit of risk).

**Expected Portfolio Return:**
The expected return is the weighted sum of the individual asset returns:

$$E(R_p) = \sum_{i=1}^{n} w_i E(R_i)$$

**Portfolio Variance (Risk):**
Risk is calculated using the covariance matrix of the asset returns, accounting for how the stocks move in relation to one another:

$$\sigma_p^2 = \sum_{i=1}^{n} \sum_{j=1}^{n} w_i w_j \text{Cov}(R_i, R_j)$$

**The Objective Function (Sharpe Ratio):**
The Scipy optimizer dynamically adjusts the weights $w_i$ to maximize the Sharpe Ratio, where $R_f$ is the risk-free rate:

$$\text{Sharpe Ratio} = \frac{E(R_p) - R_f}{\sigma_p}$$

## 💻 Tech Stack
* **Language:** Python 3.12
* **Machine Learning:** Prophet, Scikit-learn, Pandas, Numpy
* **Optimization:** Scipy
* **Database:** Supabase (PostgreSQL)
* **Frontend:** Streamlit, Plotly, Altair
* **CI/CD & MLOps:** GitHub Actions (Data CD), CircleCI (Testing CI), Streamlit Cloud (Frontend CD)
* **Dependency Management:** Poetry

## 🚀 Local Setup & Installation

To run this project locally, ensure you have Python 3.12 and Poetry installed.

