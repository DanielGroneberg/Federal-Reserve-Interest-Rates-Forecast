# Overview

The goal of this project is to predict how the Federal Reserve will change interest rates using a timeseries forcast and several economic metrics, including:

* GDP
* Potenial GDP
* Inflation
* Core Inflation 
* Unemployment
* Productivity
* Sentiment analysis from the Federal Reserve's Beige Book transcripts


# Problem Statement

Interest rates adjustments are a major component in the Federal Reserve's monetary policy and are intended to have a far-reaching effect on the economy by affecting the cost of borrowing. Increases in interest rates will make expanding a business more expensive, and may lead to slower hiring or layoffs which can show up as higher unemployment. Low interest rates can cause the opposite - expanded production, lower unemployment and GDP expansion. The Federal Reserve attempts to "promote maximum employment, stable prices, and moderate long-term interest rates in the U.S. economy" through its monetary policy, and these metrics are in turn used to guide future rates changes. https://www.federalreserve.gov/aboutthefed.htm I created a timeseries forecast to attempt to model these metrics and predict interest rates changes. I also performed sentiment analysis on Beige Book transcripts which contain a national summary of the Federal Reserve's written report on economic conditions.


# Discussion

I created a Vector Autoregression model for the metrics mentioned above, as well as Beige Book sentiment scores, and it performed with mixed success. Due to some of the metrics having quarterly or even yearly frequency, it is somewhat difficult to accurately score model performance, and difficult to even train a model due to limited data. I picked a forecasting period of five years for my test set, which was intended to provide enough test data to score properly while not making up an unrealistic amount of time to predict, but even this split meant that some metrics contained very little testing data. In particular, the interest rate forecast model did not perform especially well - it has an error of 653%. This is probably a reflection of a Vector Autoregression model not being able to capture the underlying complexity of Federal Reserve interest rates changes, and the difficulty of scoring a model using only 60 observations across a five year window. Unlike the other metrics though, interest rate changes nearly always take place with a low degree of frequency (roughly every six weeks), so this isn't really something which can be improved much further using a vector autoregression model.

A better approach for forecasting interest rates could be a Monte Carlo experiment where I could predict the likelihood of interest rates falling within certain ranges, similar to how these experiments are used to predict the future value of a portfolio: https://www.wallstreetoasis.com/resources/financial-modeling/monte-carlo-simulation

     "The simulation has also been applied in portfolio management. Here it is used to estimate the value of a portfolio and create a distribution of potential future cash flows and price paths."
     
So, rather than predicting exact interest rate values, I could focus on estimating the likelihood that interest rates will be within specific ranges during defined periods in the future. Not only would this be a much more feasible approach, it would probably produce a more usable model, as it would better handle the inherit uncertainty present in any forecast. The model would clearly express the degree of uncertainty present, whereas my Vector Autoregression model can be said to perform well or poorly, but doesn't clearly represent the degree of uncertainty contained in each prediction.


# Conclusion 

A natural problem of a timeseries forecast model is that predictions further into the future will be more difficult to make accurately. I initially tried a train/test split of 80/20, but this amounted to ~40 years of training data and ~10 years of testing data, meaning I would be forecasting GDP, inflation, etc. 10 years into the future which ended up being unrealistic both because it reduced the training data and also because it's just inheritly challenging to forecast economic data that far into the future. I thought that a forecast of two quarters would be more feasible, but the frequency of my data posed a different challenge: it's either on a monthly or quarterly basis. This meant that the test data would contain either six or two observations. As a result, it was difficult to actually assess model performance, as there was not enough granularity. I settled on a testing set of five years to strike a decent balance, but in order to improve this model I will need to find more granular data with a higher frequency. This will allow me to more accurately test my model while giving it more data points and more complexity.

Another approach would be to apply Monte Carlo experiments to predict the probability of future observations falling within certain ranges of values. This could be especially valuable for predicting interest rate adjustments, as these adjustments take place relatively infrequently and these models are designed specifically for scenarios with a high degree of uncertainty.