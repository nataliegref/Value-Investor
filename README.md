
# Value Imvestor

## Problem statement:

We are a portfolio investment company and we make investments in the emerging markets around the world. Our company profits by investing in profitable companies, buying, holding and selling company stocks based on value investing principles.


Our goal is to establish a robust intelligent system to aid our value investing efforts using stock market data. We make investment decisions and based on intrinsic value of companies and do not trade on the basis of daily market volatility. Our profit realization strategy typically involves weekly, monthly and quarterly performance of stocks we buy or hold.


## Data Description:


You are given a set of portfolio companies trading data from emerging markets including 2020 Q1-Q2-Q3-Q4 2021 Q1 stock prices. Each company stock is provided in different sheets. Each market's operating days varies based on the country of the company and the market the stocks are exchanged. Use only 2020 data and predict with 2021 Q1 data.


## Download Data:


https://docs.google.com/spreadsheets/d/1MiunF_O8eNWIcfaOA4PVm668RN7FgLNA0a6U4LWf5Bk/edit?usp=sharing


## Goal(s):


Predict stock price valuations on a daily, weekly and monthly basis. Recommend BUY, HOLD, SELL decisions. Maximize capital returns, minimize losses. Ideally a loss should never happen. Minimize HOLD period.


## Success Metrics:


Evaluate on the basis of capital returns. Use Bollinger Bands to measure your systems effectiveness.


# Method and Results
## Exploratory data analysis and cleaning data
I noticed the last row of each sheets had text to I removed those rows. I also cleaned up text in the volume column, made the date into datetime format, along with making other columns numeric. I then did some simple data exploration to gain insights.

## Feature engineeing
The exercise calls for looking at daily (original data), weekly and monthy trends so I made two new datasets derives from the original data that were rexampled to be weekly and monthly respectively.

## Models
I then built several models: moving average, exponential smoothing, LSTM (normal, sequential and binary), Auto-ARIMA and Propher. I trained each model for daily, weekly and monthyl, and with different lookback windows. I then gathered test scores for each (mean squared error, and mean absolute error) in order to compare models.
I did this for the first 3 sheets with the idea of then selecting the best type of model to run on all 8 sheets (each sheet is for a portfolio company).

## Initital Results
### Sheet 0
#### DAILY: 
I discounted auto-ARIMA and exponential smoothing results as they are just a flat line.
The best daily forecasting models for data sheet 0 in MSE are:
moving average look back 30, sequential LSTM with lookback 30, and standard LSTM with lookback 20 
and in MAP are:
the same

#### WEEKLY:
The best weekly forecasting models for data sheet 0 in MSE are: moving average with lookback 6, exponential smoothing with smoothing .5 , and moving average with lookback 2 
and in MAP are: the same

#### MONTHLY:
The best monthly forecasting models for data sheet 0 in MSE are: sequential LSTM with lookback 3 , bidirectional LSTM with lookback 3 , and moving average with lookback 3 
and in MAP are: the same

### Sheet 1
#### DAILY: 
I discounted exponential smoothing and autoarima results as they are just a flat line.

The best daily forecasting models for data sheet 1 in MSE are:
prophet, moving average lookback 30 and standard lstm lookback 10
and in MAP are: prophet, standard lstm lookback 10 and moving average lookback 30


#### WEEKLY:
I discounted exponential smoothing results as they are just a flat line.

The best weekly forecasting models for data sheet 1 in MSE are: moving average lookback 2, bidirectional lstm lookback 2 and standard lstm lookback 2.
and in MAP are: the same

#### MONTHLY:
I discounted moving average 1 and exponential smoothing results as they are just a flat line.

The best monthly forecasting models for data sheet 1 in MSE are: standard LSTM lookback 3, moving average lookack 3 and bidirectional lstm lookback 3
and in MAP are: the same

### Sheet 2
#### DAILY: 
I discounted exponential smoothing and auto-ARIMA results as they are just a flat line.
The best daily forecasting models for data sheet 2 in MSE are: moving average lookback 60, sequential LSTM lookback 10, and sequential LSTM lookback 60
and for MAP are: the same


#### WEEKLY:
I discounted moving average lookback 2 and exponential smoothing results as they are just a flat line.
The best weekly forecasting models for data sheet 2 in MSE are: moving average lookback 6, bidirectional LSTM lookback 6 and auto arima.
and in MAP are: the same

#### MONTHLY:
I discounted moving average lookback 1 and exponential smoothing results as they are just a flat line.
The best monthly forecasting models for data sheet 2 in MSE are: standard LSTM lookback 3, moving average lookback 3, and bidirectional lstm lookack 3
and for MAP are: the same

Based on these results I used sequential LSTM lookback 30 for dialy forecasts, moving average with lookback 6 for weekly and standard LSTM with lookack 3 for monthly.
However I noted that the LSTM model results fluctate in their accuracy more than the simplest models here (moving average) and so might not be the best overall. This could be improved by running multiple for each instantiation of the models and looking at precision, accuracy and their distribution. For the sake of this exercise I will however used the identified 'best' models.

## Investments
Based on these trained models, I then built an investment function wherein I first made the Bollinger bands for the predictions, and then defined buy and sell strategies based whether the actual data was above (sell), within (hold) or below (buy) the bollinger bands.

## Conclusion

Results show that the investment strategy is not particularly strong. It would be better to use models that work best for each data set rather than pick a general model for all datasets. Furthemore the positive results (profit) that I saw in some cases seemed to be more due to change than the models themselves.
The models have a lot of built-in stochasticity, and stock markets are notoriously difficult to predict. 


