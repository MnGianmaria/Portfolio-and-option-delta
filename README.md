# Portfolio Optimization and Option Delta Estimation

An empirical study of portfolio allocation and option delta estimation using Python.

## Overview

This project investigates two problems in quantitative finance: portfolio construction using absolute-deviation risk measures, and option delta estimation using machine learning.

Both analyses use chronological training and test samples to evaluate performance on subsequent observations.

## 1. Portfolio Optimization

How do portfolios constructed to minimize absolute-deviation risk perform outside the estimation sample?

Using daily equity returns over 2022–2023, the analysis explores the relationship between portfolio risk, return targets, and asset allocation.

The workflow includes:

- Collecting adjusted stock prices and computing simple returns.
- Examining return distributions through descriptive statistics.
- Constructing fully invested, long-only portfolios across different target levels.
- Comparing portfolio risk and median returns in the training and test samples.

The interpretation distinguishes the median of portfolio returns from the weighted average of individual stock medians.

## 2. Option Delta Estimation

How accurately can machine learning models approximate option delta relative to an analytical benchmark?

The analysis uses call and put options on the December 2023 S&P 500 futures contract, across five strikes.

A Random Forest regressor and a feed-forward neural network estimate delta using:

- Futures price.
- Strike price.
- Time to maturity.
- Rolling historical volatility.
- Option type: call or put.

Predictions are compared with a Black-model benchmark using mean squared error, R², and residual diagnostics.

## Methods and Tools

- **Data preparation:** pandas and NumPy.
- **Portfolio optimization:** SciPy.
- **Machine learning:** scikit-learn.
- **Neural networks:** TensorFlow and Keras.
- **Visualization:** Matplotlib.
- **Market data collection:** yfinance.

## Data and Limitations

The equity analysis downloads historical prices for the S&P 500 constituents available at the time of retrieval. This universe does not reconstruct historical index membership and is subject to selection and survivorship bias.

The options analysis uses a course-provided dataset. Historical volatility is used as an input rather than option-implied volatility. The interpretation of the analytical benchmark depends on the delta conventions used by the data provider.

The analysis concerns portfolio risk and option sensitivity estimation; it does not establish the profitability of a trading strategy.

## Project Status

The original coursework is being revised for reproducibility and clearer methodological documentation. Notebooks, execution instructions, and verified results will be added as the revision is completed.

## Authors

Gianmaria Monaco and Leandro Arzilli.

Originally developed for **21046 — Data Science and Machine Learning for Finance**, class 31, Bocconi University, academic year 2025–2026.
