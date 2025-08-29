# Stock Return Prediction with Volume Signals (AAPL Case Study)

## 1. Overview
This project explores the relationship between stock trading volume and returns, using Apple (AAPL) historical data as a case study.  
We preprocess raw financial data, engineer predictive features, and evaluate models ranging from baseline linear regression to classification approaches.  
We also compare Gaussian-based confidence intervals with bootstrap intervals to assess model uncertainty.

---

## 2. Data
- **Source**: AAPL daily OHLCV data (1980–2022)  
- **Key fields**: `Date`, `Adj Close`, `Volume`  
- **Processed fields**:  
  - `Return = AdjClose.pct_change()`  
  - `Roll_Volume = log(rolling sum of 5-day Volume)`  
  - Engineered features:  
    - `lag_1` (previous day return)  
    - `roll_mean_5` (5-day rolling mean)  
    - `momentum_10` (10-day return sum)  
    - `zscore_20` (20-day standardized return)  
    - `roll_vol_20` (20-day rolling volatility)  

---

## 3. Workflow
1. **Data Cleaning**  
   - Handle missing values  
   - Remove outliers (IQR & Z-score)  
   - Winsorization of extreme returns  

2. **Exploratory Data Analysis (EDA)**  
   - Summary statistics (skewness, kurtosis)  
   - Histograms, boxplots, scatter plots  

3. **Feature Engineering**  
   - Lagged features  
   - Rolling averages & volatility  
   - Momentum and standardized z-scores  

4. **Modeling**  
   - Baseline Linear Regression: one-step-ahead return prediction  
   - Logistic Regression: classify next-day up/down moves  
   - Metrics: R², RMSE, classification report, confusion matrix  

5. **Uncertainty Quantification**  
   - Gaussian CI (normal error assumption)  
   - Bootstrap CI (resampling)  
   - Compare interval widths and implications for risk  

---

## 4. Results
- Logistic regression on simple features achieved ~47% accuracy, with high recall for down moves but poor recall for up moves.  
- Linear regression showed near-zero predictive power (R² ≈ 0).  
- Gaussian confidence intervals were narrow and underestimated uncertainty.  
- Bootstrap intervals were wider, better reflecting fat-tailed risks in financial data.  

---

## 5. Reflection
- Financial return prediction is extremely noisy — simple lag and volume features were insufficient for robust prediction.  
- Classification results were biased toward predicting “down” moves, highlighting the need for balanced class handling or adjusted thresholds.  
- Outlier handling and winsorization stabilized return distributions but did not significantly improve predictive accuracy.  
- Gaussian assumptions proved overly optimistic; bootstrap intervals provided a more realistic picture of risk.  
- Future improvements:  
  - richer feature sets (technical indicators, macroeconomic signals)  
  - non-linear models (tree-based ensembles, deep learning)  
  - evaluation using trading strategies (P&L, Sharpe ratio) instead of purely statistical metrics  

---
