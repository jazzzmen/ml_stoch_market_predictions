# Stock Price Prediction with Machine Learning

## Project Overview
I explore whether machine learning can predict the daily movement of Apple’s stock using Yahoo Finance data.
I evaluate both classification (up vs. down) and regression (next-day price).

- Classification: Logistic Regression, Random Forest, XGBoost
- Regression: Ridge Regression (predict next-day close)

## How to Run
```bash
pip install -r requirements.txt
jupyter notebook ML_stock_market_predictions.ipynb
```
Inside the notebook you can change:
```TICKER = "AAPL"```

## Data
- Source: [Yahoo Finance](https://finance.yahoo.com/) (via `yfinance` library)  
- Data: Daily OHLCV (Open, High, Low, Close, Volume) for Apple (`AAPL`)  
- Time horizon: full available history (`period="max"`)
- Split: Time-ordered (first 80% train, last 20% test), no shuffling
- I cache data to data/AAPL.csv to avoid repeated downloads.

## Features
- Returns, SMA(5/20), RSI(14), MACD(12,26,9), Bollinger Band width, plus raw OHLCV
- Targets:
  - y_dir (classification): 1 if Close_{t+1} > Close_t, else 0
  - y_next_close (regression): Close_{t+1}

## **Models**
   - Logistic Regression (classification)  
   - Random Forest (classification)  
   - XGBoost (classification)  
   - Ridge Regression (regression for price)  

## **Evaluation metrics**
   - Classification: Accuracy, F1-score, ROC-AUC  
   - Regression: RMSE, MAE  

## Results (on test set)
| Model                | Task           |  Accuracy  |   F1  |  AUC  | RMSE |  MAE |
|----------------------|----------------|------------|-------|-------|------|------|
| Logistic Regression  | Classification | ~0.52      | ~0.52 | ~0.50 | –    | –    |
| Random Forest        | Classification | ~0.41–0.50 | ~0.40 | ~0.50 | –    | –    |
| XGBoost              | Classification | ~0.47–0.50 | ~0.48 | ~0.50 | –    | –    |
| Ridge Regression     | Regression     | –          | –     | –     | ~5.8 | ~4.2 |

## Conclusion
- **Daily up/down direction is essentially random** with only OHLCV + basic indicators.  
- Logistic Regression achieved ~52% accuracy, Random Forest and XGBoost hovered around 47–50%.  
- Ridge Regression predicted prices with RMSE ~\$6 (on ~\$220 stock).  
- This matches financial research: short-term daily movements are noisy and hard to predict.  

## Next Steps
- Try **deep learning (LSTM, GRU)** on sliding windows of sequences.  
- Experiment with **longer horizon targets** (weekly/monthly trends).  
- Include **alternative data sources** (news sentiment, macroeconomic variables).
