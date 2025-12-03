# Overview

In this project, I will demonstrate data preparation and aggregation methods, together with data analysis, on the example of wheat futures data. I will use Power BI charts, as well as Python and R visuals, for a more in-depth analysis. Data was used from these sources:



# Goal(Business question)
Our **goal** is to model factors that influence commercials' net positioning in futures and options. The data sets that we will use are Commitment of Traders Reports, WASDE reports, Export Sales reports, OHLC data, and Cooling/Heating Degree days. Our main task is to determine how extreme the positioning is compared to previous years. We will achieve that by calculating a z-score with a rolling average with a look-back window of five years. We will do the same for our explanatory variables. Before we proceed with transformations, we will take a quick glance at correlation tables that will give us a hint of potential relationships.(1.4) 


# Data Preparation and linkage
First, we aggregate WASDE reports into one (PY 2.Aggregation Script); the rest of the data came aggregated from the download source. Since our data has different granularity and was collected on different days of the week, we need to prepare the data for Python and R so that the regression scripts run properly. 

We create a calendar table and merge a copy of it with each weekly fact table. As an output, we get a daily fact table that has some null values, which we fill down to complete the data. (3. Weekly to Daily transformation) Now we have data that is ready to be linked. We use a star schema to link our calendar with multiple fact tables. The only thing that unites them is the date. 

# Variable preparation
We have already measured correlations of raw variables with the Net Commercial position. One of the problems of using raw data is the potential non-stationarity of the time series. We will transform variables of interest into z-scores that will be calculated taking a five-year rolling average. After the transformation, the relationship still exists. We will proceed with our analysis. (1.4 correlation summary z-score) 

# Modeling
We will run OLS, including the Newey-West estimator with five lags, so our standard errors are more reliable.(5. OLS) The model will fit our values, and the residuals that deviate more than one sigma (adjustable threshold) will indicate unusually high or low positioning, which will serve as a potential indicator that the Net Commercial position is about to reach its peak. 

Our standard errors are most likely overly “optimistic” due to potential autocorrelation; however, R-squared and coefficients are still meaningful. 


# Results
If we plot our residuals, we can see points in time where the positioning was very extreme. The bigger the deviation, the stronger the signal. (5. Residuals and Signal)
