---
layout: post
title: Predicting the Present with Google Trends and News Headlines
subtitle: 
cover-img: /assets/img/stocks.jpg
thumbnail-img: /assets/img/trends.png
share-img: /assets/img/google-trends.png
tags: [trends, google]
---


## Predicting the stock market

Who wouldn’t like to be able to predict the stock market? Certainly everyone would, however, doing so is an extremely hard process.

But, can we make it even harder? Fortunately, yes! If we consider periods of high economic uncertainty, when the market is more volatile and unpredictable than ever.

In this blog post, we show how we can utilise Google Trends data along with news headlines to try and predict the prices of the S&P 500 market index and Bitcoin.




## How do Google Trends relate to stocks? 
First, let’s see how trends in Google searches relate to the movements of the stock market.

A naive person (not us!) may think that if someone is searching for stocks, then they must be feeling confident about the economy and the stock market, so they are looking to invest. But, if let’s take a moment to think about this a bit further. What would an investor do when the economy seems on the verge of crashing? Check the stock prices! So, even if stock prices are bound to take a dive in the immediate future, Google searches may still be rapidly increasing.

Let’s look at specific examples. The next figure shows the price of the S&P 500 market index for the time period between 01 January 2019 until 31 May 2020. We see that in the period between , which corresponds to the peak of the coronavirus pandemic worldwide, there is an inverse correlation between the S&P price and the Google Trends for the term “S&P 500”.



{% include lines_snp_pts.html %}



Let’s also take a look at the same data for the case of Bitcoin.

{% include lines_btc_pts.html %}



## Autoregressive Models

Now, it’s time to get a bit more technical.

Autoregressive models are frequently used in finance for predictions in time series. In short, an autoregressive model which uses values from previous time steps (lags) as an input to a regression equation in order to predict the values at the current time step. For example, in the case of daily stock prices a lag-1 corresponds to the price of the previous day.

Let’s plot the autocorrelation between the S&P price at time t and the prices at various days before that, such as the previous day, 5, 10, and 14 days before. We see that prices of a given day are highly correlated with the prices of previous days. The further back we are looking at the looser the correlation becomes.


{% include scatter_snp.html %}

## Predicting with Autoregressive Models and Google Trends

Now we are ready to predict some S&P 500 and Bitcoin prices using autoregression. We will showcase the performance of two such models; one that uses only the prices of the five previous days to predict the current one and one that also utilizes the Google Trends of the day whose price we are trying to predict.

The next figure shows the results of the predictions.


{% include snp_preds_no_news.html %}


Let’s focus on a smaller time frame, specifically the one when coronavirus peaked. The  figure below shows the prediction results for that period. We see that the model guided by the **trends performs worse**. 

![image](/assets/img/table_covid_simple.png)



How can we explain that? As we mentioned earlier, the Google searches for “S&P 500” during those days were at their peak. However, they do not provide the model with any _sense_ about the motive behind those searches. Are people confident or uncertain? We will try to provide a solution to the problem in the next paragraph.


## Sentimental Analysis of News

Sentimental analysis is the process of analyzing a natural language phrase and assigning a value to it that measures how positive (value greater than zero) or negative (value less than zero) that phrase is.

## Embedding Sentiments in Predictions

We analyzed news headlines for the mentioned time periods and performed sentimental analysis on them. For this purpose we use  [TextBlob](https://textblob.readthedocs.io/en/dev/).

Our intuition is that positive news drive stock prices up, while negative news have the opposite effect. We factor in the news in our model by multiplying the trends coefficient with -1 or 1 depending on the aggregated news' sentimental value of that day. The idea is that if Trends are high for a day because of some bad news, multiplying them with a negative value will have the desired effect.



The predictions of the model that utilizes the news are indeed better than the one that only utilizes the trends. To provide some numbers, from 15 February 2020 to 15 April 2020 the former model has a mean absolute error of 91.68 while, the former has error equal to 92.18.

{% include lines_snp_covid.html %}

We see that our intuition is indeed correct!

### What about a more volatile price?

We also attempt to predict bitcoin price changes. The news' addition slightly improves predictions in this case too.

{% include btc_preds.html %}



## Conclusion


So, are we going to get rich? Probably not! 

But overall, by adding sentimental analysis of news, we slightly improved the trends model in both datasets. In the table below we can see the mae improvement which is marginal.

![image](/assets/img/tables.png)

In this blog post we have highlighted the useful resources that can be combined to create a reasonable short term prediction. We only use a weak model, but all techniques are appliable to stronger models (deep neural networks etc.).

