---
layout: post
title:  "Time Series Forecasting"
date:   2020-01-26 00:04:58 +0530
categories: general
summary: Time series forecasting problems can be approached using various methods, including statistical and machine learning methods. This article focuses primarily on machine learning. Statistical methods may be covered in upcoming articles.
---


This article is divided into two parts. The first part explains the basic concepts of time series forecasting, and the second part implements these concepts in a real-world problem.

## Content

1. What can be forecast?
2. Determining what to forecast?
3. Forecasting data and methods
4. Time Series Forecasting
5. Predictor variables and time series forecasting

### 1. What can be forecast?

Some things are easier to forecast than others. For example, we can forecast the electricity demand of a city because we know the factors affecting it, such as temperature, holidays, and economic conditions. On the other hand, forecasting stock values is more challenging because the factors affecting them are less predictable.

The predictability of an event or quantity depends on several factors:
- How well we understand the contributing factors.
- The amount of available data.
- Whether the forecasts can impact the subject being forecasted.

### 2. Determining What to Forecast?

Before jumping directly into forecasting, it's necessary to understand what needs to be forecasted. Considerations include:
- Product lines or groups of products.
- Sales outlets, grouped by region or only for total sales.
- Frequency of forecasts (weekly, monthly, or annually).
- Forecast horizon (one month, six months, ten years).

### 3. Forecasting Data and Methods

The appropriate forecasting methods depend largely on the available data.

- **Qualitative forecasting methods (guesswork):** Used when no relevant data are available.
  
- **Quantitative forecasting methods:** Used when numerical information about the past is available, and some aspects of past patterns are expected to continue into the future.

### 4. Time Series Forecasting

Anything observed sequentially over time is a time series. In this article, we'll consider time series observed at regular intervals (e.g., hourly, daily, weekly, monthly).

### 5. Predictor Variables and Time Series Forecasting

Predictor variables are often useful in time series forecasting. For example, a model forecasting hourly electricity demand during the summer might include predictor variables like current temperature, strength of the economy, population, time of day, day of the week, and an error term.

Time series forecasting models can take different forms:
- **Explanatory model:** \(ED = f(\text{current temperature, strength of economy, population, time of day, day of week, error})\).
  
- **Time series model:** \(ED_{t+1} = f(ED_t, ED_{t-1}, ED_{t-2}, ED_{t-3}, \ldots, \text{error})\).
  
- **Mixed models:** \(ED_{t+1} = f(ED_t, \text{current temperature, time of day, day of the week, error})\).

### Conclusion

An explanatory model is useful for incorporating information about other variables. However, a forecaster might choose a time series model for various reasons, including a lack of understanding of the system, difficulty in measuring relationships, the need to forecast future values of predictors, and a focus on predicting outcomes rather than understanding the underlying reasons.

The choice of the forecasting model depends on available resources and data, the accuracy of competing models, and the intended use of the forecasting model.

*Next Part: The basic steps in a forecasting task (coming soon)*

*The End!*

