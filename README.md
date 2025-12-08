# Dendri-Portfolio

## Multi-Output LSTM Forecasting for NYSE Time Series (1962–1986)
This project builds a single multi-output LSTM neural network to forecast:
Daily DJIA return
Log trading volume
Log volatility
based on the previous 5 trading days of historical features.
The model is trained on NYSE data from 1962–1986, standardized using training-set statistics to avoid look-ahead bias.

### Project Summary
- Built a sequential model with 2 LSTM layers (32 units each).  
- Predicts 3 outputs simultaneously.  
- Captures nonlinear relationships between returns, volume, and volatility.  
- Demonstrates stylized financial facts:  
  - Weak return predictability  
  - Volume–volatility correlation  
  - Strong volatility persistence  
