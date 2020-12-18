---
layout: post
title: Predicting the Present with Google Trends and News Headlines
subtitle: 
cover-img: /assets/img/stocks.jpg
thumbnail-img: /assets/img/trends.png
share-img: /assets/img/google-trends.png
tags: [trends, google]
---


## Predicting the Present with Google Trends and News Headlines


Who wouldn’t like to be able to predict the stock market? Certainly everyone would, however, doing so is an extremely hard process.

But, can we make it even harder? Fortunately, yes! If we consider periods of high economic uncertainty, when the market is more volatile and unpredictable than ever.

In this blog post, we show how we can utilise Google Trends data along with news headlines to try and predict the prices of the S&P 500 market index and Bitcoin.

{% include scatter.html %}



### How do trends relate to stocks?
First, let’s see how trends in Google searches and news headlines relate to the movements of the stock market.

A naive person (not us!) may think that if someone is searching for stocks, then they must be feeling confident about the economy and the stock market, so they are looking to invest. But, if let’s take a moment to think about this a bit further. What would an investor do when the economy seems on the verge of crashing? Check the stock prices! So, even if stock prices are bound to take a dive in the immediate future, Google searches may still be rapidly increasing.

Let’s look at specific examples. The next figure shows the price of the S&P 500 market index for the time period between 01 January 2019 until 31 May 2020. We see that in the period between , which corresponds to the peak of the coronavirus pandemic worldwide, there is an inverse correlation between the S&P price and the Google Trends for the term “S&P 500”.

## How do trends relate to stocks?



{% include scatter_snp-2.html %}

### Insert Figures for S&P

Let’s also take a look at the same data for the case of Bitcoin.

### Insert Figures for Bitcoin
{% include lines_snp.html %}



Autoregressive Models

Now. it’s time to get a bit more technical.

Autoregressive models are frequently used in finance for predictions in time series. In short, an autoregressive model which uses values from previous time steps (lags) as an input to a regression equation in order to predict the values at the current time step. For example, in the case of daily stock prices a lag-1 corresponds to the price of the previous day.

Let’s plot the autocorrelation between the S&P price at time t and the prices at various days before that, such as the previous day, 5, 10, and 14 days before. We see that prices of a given day are highly correlated with the prices of previous days. The further back we are looking at the looser the correlation becomes.

### Insert Autocorrelation Figures for S&P
