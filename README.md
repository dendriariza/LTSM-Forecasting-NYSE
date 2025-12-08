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

<img width="443" height="337" alt="image" src="https://github.com/user-attachments/assets/526bf33b-c1e3-4c0a-939d-6f50ba8abf3c" />

### Why I Used This Data
The NYSE dataset (1962–1986) provides a long horizon of daily market activity, capturing multiple macroeconomic cycles, volatility  regimes, and behavioral patterns. It contains three variables that are central to quantitative finance:  
- Daily DJIA return – highly noisy but essential for understanding price movements.  
- Log trading volume – a proxy for market participation and liquidity.  
- Log volatility – a key input for risk models, VaR, and derivatives pricing.  

This makes the dataset ideal for building a multi-output time series predictor that captures how these variables interact dynamically.  
Instead of predicting each variable separately, I wanted a single unified model that learns the shared information structure across returns, volume, and volatility.  

This reflects real-world financial markets where:  
- Volume and volatility are strongly intertwined.  
- Volatility exhibits autocorrelation and clustering.  
- Returns are largely unpredictable but still influenced by market regimes.  

### Modeling Approach
The model is implemented using TensorFlow/Keras and is structured around a multi-output LSTM network. The key design choice is using 5 trading days of historical data to predict all three market statistics for the next day.  

- Data Standardization  
The input features are standardized using only the training set to avoid look-ahead bias, ensuring realistic model behavior.  
- Sequence Windowing  
Each input sample is a 5×3 matrix representing:  
5 days × (return, log volume, log volatility)  
- LSTM Architecture
<img width="652" height="242" alt="image" src="https://github.com/user-attachments/assets/f984e355-4124-4ab8-96a2-6bba5beba778" />

  - The first LSTM layer learns short-term temporal dependencies.  
  - The second LSTM encodes a compressed representation of market dynamics.  
  - The Dense layer produces three simultaneous predictions.
  
- Training Procedure  
  - Optimized using Adam.  
  - Validation loss monitored with ModelCheckpoint.  
  - 100-epoch training ensures convergence without overfitting.  
- Model Saving  
  - The best-performing model is stored as bestmodel.keras, which preserves the architecture and learned weights.  

### Results & Quantitative Insights
<img width="508" height="655" alt="image" src="https://github.com/user-attachments/assets/257e0b83-e457-479c-ba89-d2d43b9eba0f" />

The model shows realistic performance for financial time series:  
- Returns (R² = 0.063)
Daily returns are highly noisy and close to random. The model captures only weak structure, which is expected in real markets and confirms it is not overfitting.  
- Log Volume (R² = 0.578)
Volume exhibits strong autocorrelation and behavioral persistence. The LSTM learns these patterns well, accurately tracking liquidity cycles with only occasional misses during news-driven spikes.  
- Log Volatility (R² = 0.967)
Volatility is highly predictable due to clustering. The model captures regime shifts, calm vs. high-vol periods, and long-memory behavior almost perfectly.  
- Key Interpretations
The model effectively learns nonlinear market dynamics, especially volatility persistence and volume–volatility relationships.
Joint forecasting improves performance by letting the LSTM use shared structure across variables.
Prediction behavior aligns with empirical finance: volatility is predictable, returns are not.


