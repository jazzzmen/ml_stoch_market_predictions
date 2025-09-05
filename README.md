# Stock Price Prediction with Machine Learning

## 📌 Project Overview
This project explores whether **machine learning models** can predict the daily movement of Apple’s stock price using **Yahoo Finance data**.  

We tested **classification (up vs down)** and **regression (next-day price)** approaches with different models:  
- Logistic Regression  
- Random Forest  
- XGBoost  
- Ridge Regression  

## 📂 Dataset
- Source: [Yahoo Finance](https://finance.yahoo.com/) (via `yfinance` library)  
- Data: Daily OHLCV (Open, High, Low, Close, Volume) for Apple (`AAPL`)  
- Time horizon: full available history (`period="max"`)

## ⚙️ Methods
1. **Data preprocessing**
   - Clean OHLCV data
   - Create technical indicators: returns, SMAs, RSI, MACD, volatility, Bollinger Bands
   - Create targets:  
     - `y_dir`: tomorrow up (1) or down (0)  
     - `y_next_close`: tomorrow’s closing price

2. **Models**
   - Logistic Regression (classification)  
   - Random Forest (classification)  
   - XGBoost (classification)  
   - Ridge Regression (regression for price)  

3. **Evaluation metrics**
   - Classification: Accuracy, F1-score, ROC-AUC  
   - Regression: RMSE, MAE  

## 📊 Results (on test set)
| Model                | Task           |  Accuracy  |   F1  |  AUC  | RMSE |  MAE |
|----------------------|----------------|------------|-------|-------|------|------|
| Logistic Regression  | Classification | ~0.52      | ~0.52 | ~0.50 | –    | –    |
| Random Forest        | Classification | ~0.41–0.50 | ~0.40 | ~0.50 | –    | –    |
| XGBoost              | Classification | ~0.47–0.50 | ~0.48 | ~0.50 | –    | –    |
| Ridge Regression     | Regression     | –          | –     | –     | ~5.8 | ~4.2 |

## 📈 Conclusion
- **Daily up/down direction is essentially random** with only OHLCV + basic indicators.  
- Logistic Regression achieved ~52% accuracy, Random Forest and XGBoost hovered around 47–50%.  
- Ridge Regression predicted prices with RMSE ~\$6 (on ~\$220 stock).  
- This matches financial research: short-term daily movements are noisy and hard to predict.  

## Next Steps
- Try **deep learning (LSTM, GRU)** on sliding windows of sequences.  
- Experiment with **longer horizon targets** (weekly/monthly trends).  
- Include **alternative data sources** (news sentiment, macroeconomic variables).
