# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Capstone: Stock Price Prediction 

### Henri Oei, DSIF2 - Singapore

## Problem Statement

The objective is to create a predictive model to forecast future stock closing prices.
*For the purpose of this presentation I will be showcasing the AMD stock ticker.*

## Executive Summary

I'll be predicting AMD Stock Prices with the following models:

1. ARIMA (Autoregressive Integrated Moving Average)
2. SARIMAX (Seasonal AutoRegressive Integrated Moving Average)
3. GRU (Gated Recurrent Unit)
4. LSTM (Long-Short Term Memory)

In time series data the value that we get today directly depends on the value that we got yesterday. But how we get from yesterday to today we are adding/subtracting is what we call "white noise" and that is not correlated.

Therefore, pre-processing work was done to the time series data before I created the ARIMA and SARIMAX models since it was non-stationary. Differencing was put in place in order to make the data stationary and remove any correlation or memory.

One of the fundamental differences between many time series and a random sampling from a single, known distribution, is that time series often have "memory" - We quantify this memory as autocorrelation. This is used to detect non-randomness in data and to identify an appropriate time series model if the data is not random.

With autocorrelation, we are not dealing with two random variables, what we are doing is measuring the correlation between a time series in itself at different lags or shifts in time. As the lag increases, you get to a point where if you are far away enough in time you can consider two values to be statistically independent.

W are then left with white noise-a random process, whose samples are regarded as a sequence of serially uncorrelated random variables with zero mean and finite variance.


## Evaluation of Predictions

**Intial AdFuller Results**
- ADF Test Statistic : 1.3842659609766095
- p-value : 0.997041479296224
- Number of Observations Used : 1237
- Comment : Time series is non-stationary

**After Applying Lag(1) to the Dataset**
- ADF Test Statistic : -9.059840432443018
- p-value : 4.594794188707755e-15
- Number of Observations Used : 1242
- Comment : Time series is stationary

**After Applying Lag(24) to the Dataset**
- ADF Test Statistic : -8.610593374916578
- p-value : 6.491890430629663e-14
- Number of Observations Used : 1209
- Comment : Time series is stationary

**Model Performance**
- **ARIMA** : The average difference between the predicted value and the actual value is 24.29%
- **SARIMAX** : The average difference between the predicted value and the actual value is 26.19%
- **GRU** : The average difference between the predicted value and the actual value is 6.3%
- **LSTM** : The average difference between the predicted value and the actual value is 4.58%

## Conclusions and Recommendations

We should not depend 100% on predictions done with the current models as there are many other factors involved that are not included in the model that affects the price movements. However, as I include more data into the models like news sentiment data from, news articles, reddit posts, tweets, discord channels, and by adding statistical weights on certain price movements based on specific chart indicators, only then can we consider the credibility of the model.


## Data

### *Source*

Pandas Data Reader (Tiingo):

### *Data Dictionary*

|Feature|Type|Dataset|Description|
|---|---|---|---|
|close|float|df|Closing stock price for the day| 
|high|float|df|Highest price reached for the day|
|low|float|df|Lowest price reached for the day|
|open|float|df|Price that the stock started with for the day|
|volume|int|df|Number of transactions for the day|
|adjClose|float|df|Rounding of closing price for the day|

|Feature|Type|Dataset|Description|
|---|---|---|---|
|close|float|pct_c_df|Scaled Valeus of closing stock price for the day| 
|high|float|pct_c_df|Scaled Valeus of highest price reached for the day|
|low|float|pct_c_df|Scaled Valeus of lowest price reached for the day|
|open|float|pct_c_df|Scaled Valeus of price that the stock started with for the day|
|volume|int|pct_c_df|Scaled Valeus of number of transactions for the day|
|adjClose|float|pct_c_df|Scaled Valeus of rounding of closing price for the day|
