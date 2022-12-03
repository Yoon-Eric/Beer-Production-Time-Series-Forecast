# Australian Beer Production Forecast

This was the final project for my time series class at UCSB (PSTAT 174)

## Abstract
In business, it is very important to know how much goods need to be produced in certain time of the year. In this project, I've implemented a mathematical model (Seasonal ARIMA) to predict monthly beer production using the past data. To be specific, in order to predict 24 months of future Australian beer production, data from 20 past years was used to formulate a mathematical model that considers both the production values from the same time of the year from the past and the production values from the past months. In conclusion, the model provides quite accurate forecast that closely resembles the actual beer production values.

## Introduction

The goal of this project is to implement time series model with parameters tuned on 20 years worth data from 1956 to 1976 to make a 2 year forecast on the monthly beer production (from 1976~1978). The dataset from Kaggle consists of two columns: date and beer production in million liters.

It is crucial for the businesses, not only for just the beer companies but the suppliers for beer companies, to predict how much production of the product is needed for each month/time of the year, and having a good, accurate model will provide forecasts that will be beneficial insights for businesses to prepare resources to produce the appropriate amount of product needed each month. Inaccurate forecast would result in over or under producing the goods and result in financial losses for the businesses. The Australian beer industry produced about 1.6 billion liters (about 422 million gallons) of beer in 2018, and the beer industry contributed 4.6 billion Australian dollars to the Australian economy. In an industry of this size, it's crucial to have an accurate forecast of the production.

In order to make an accurate forecast, first, the non-seasonality of the data was confirmed by plotting it as a time series. Box-cox transformation was used to transform the data and stabilize the variance. Decomposition of the time series and the graph was utilized to identify where to difference the time series. ACF and PACF graphs of transformed and differenced data were analyzed to identify potential parameters for seasonal ARIMA models. Then, to find the optimal model that fits the data well, several SARIMA models with all the combination of parameters were fitted and their AIC values were compared (to pick models with lower AIC values). Two candidate models were then tested for stationarity and invertibility by checking if the roots of characteristic functions of MA, AR, SMA and SAR parts of SARIMA models lie outside of unit circle. Since Model i had $\phi_2=-1$, the model was concluded to fail the stationary test. Model ii had all the roots outside of unit circle, so its stationarity and invertibility were checked. Then, for diagnostics, the normality of residuals was first assessed using histogram, qqPlot, and Shapiro Wilk test. Then, to check for independence of residuals (residuals should resemble Gaussian WN(0,1)), the ACF and PACF plot of residuals was assessed (should be within the C.I.), and linear and non linear dependence of residuals were tested using Box-Pierce test, Ljung-Box test, and McLeod-Li test. In the process, unfortunately, the model didn't pass the Box-Pierce and Ljung-Box test at confidence level 95%. Then, residuals were tested using yule-walker method, if the order selected is 0, which means that the residuals resemble AR(0) process, white noise. Although the model didn't pass the box tests, the histogram, qqPlot, ACF plot, and PACF plot all looked decent and it passed other diagnostic tests, the model SARIMA (p=1,d=1,q=3)x(P=0,D=1,Q=5)$_{s=12}$ was used for the forecast. Finally, the generated forecast of monthly beer production from 1976~1978  was compared to the actual production values from the test set. The result was quite successful with actual data aligning with the forecast values closely.

For all the visualization and calculation, R was used.
Dataset Source: https://www.kaggle.com/datasets/sergiomora823/monthly-beer-production
