
#### This project comes from a competition on Kaggle. 
#### The goal is to predict sales for the 15 days after the last date in the training data for the thousands of product 
####  families sold at Favorita stores located in Ecuador.
#### The data shared by the host are training data, testing data, and other complementary meta data such as the store information, 
####  the oil price information, and the holiday events information, and special events like wage paying and earthquake information.



#### There are a lot of time series forecasting techniques. Generally, the techniques can be divided into two categories, 
#### i.e. Classical statistical methods and machine learning methods. Based on the researches listed below:
* The M3-Competition: Results, Conclusions and Implications, 2000.
* The M4 Competition: Results, findings, conclusion and way forward, 2018.
* Statistical and Machine Learning forecasting methods: Concerns and ways forward, 2018.
* An Empirical Comparison of Machine Learning Models for Time Series Forecasting, 2010.

The results of these papers suggest that:
* Classical methods like ETS and ARIMA out-perform machine learning and deep learning methods for one-step  
  forecasting on univariate datasets.
* Classical methods like Theta and ARIMA out-perform machine learning and deep learning methods for multi-step 
  forecasting on univariate datasets.
* Machine learning and deep learning methods do not yet deliver on their promise for univariate time series 
  forecasting, and there is much work to do.

Hence, this project will focus on exploring classicial statistical methods.

#### Why choose ARIMA model?
The classicial statistical techniques for time series forecasting:
1. Autoregression (AR)
2. Moving Average (MA)
3. Autoregressive Moving Average (ARMA)
4. Autoregressive Integrated Moving Average (ARIMA)
5. Seasonal Autoregressive Integrated Moving-Average (SARIMA)
6. Seasonal Autoregressive Integrated Moving-Average with Exogenous Regressors (SARIMAX)
7. Vector Autoregression (VAR)
8. Vector Autoregression Moving-Average (VARMA)
9. Vector Autoregression Moving-Average with Exogenous Regressors (VARMAX)
10. Simple Exponential Smoothing (SES)
11. Holt Winter’s Exponential Smoothing (HWES)

To use these techniques, basically there is an assumption about the property of the time series, the time series should be stationary, 
which means the mean and variance of the time series aren't changing over time. Also, When we apply these techniques, we are rquired 
to provide non-seasonal auto-regression model parameter (p), non-seasonal moving average parameter(q), sometimes seasonal auto-regressiona 
parameter(P) and seasonal moving average parameter(Q), and seasonal pattern (S).
Normally, we plot ACF and PACF to determine those parameters. However, this is not realistic for thousands families.

The lucky thing is there is an algorithm with Python called pmdarima which search multiple combinations of p,d,q parameters and chooses the 
best model that has the least AIC.

#### To speed up the computation of thousand families, we will apply data preprocessing techniques before we use pmdarima. 
Here are preprocessing techniques being applied:

* delete those time series with the number of data points less than 16 (refering to this paper: MINIMUM SAMPLE SIZE REQUIREMENTS 
  BY Rob J. Hyndman and Andrey V. Kostenko)
* test stationary for each time series using Augmented Dickey-Fuller test
* Apply differencing techniques to non-stationary time series to detrend the data and desensonalize the data
* Acquire the "d"s and "D"s for the non-stationary time series

#### For this kaggle competition, the host doesn't provide actual sales data for test data. The model performance or your score in the 
#### competition is provided after submitting your forecasting data for those time period in testing data via Kaggle website. For this project, 
#### to test our model performance, the "train.csv" provided by host is going to be split into two part: training data and testing data. We use 
#### training data to build our model and test our model performance on testing data.
