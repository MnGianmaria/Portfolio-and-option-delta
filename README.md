# Portfolio Optimization and Option Delta Estimation

An empirical study of portfolio allocation and option delta estimation using Python.

## Overview

This project examines two problems in quantitative finance: portfolio construction using absolute-deviation risk and option delta estimation using machine learning.

Both analyses use chronological training and test samples. The notebooks include executed results, visualizations, and methodological limitations.

## Notebooks

| Notebook | Focus |
| --- | --- |
| [Portfolio Optimization](01_portfolio_optimization.ipynb) | Long-only allocation using absolute-deviation risk |
| [Option Delta Estimation](02_option_delta_estimation.ipynb) | Random Forest, neural network, and Black-model comparison |

## 1. Portfolio Optimization

How do portfolios constructed to minimize absolute-deviation risk perform outside the estimation sample?

Using daily adjusted equity prices for 2022–2023, the analysis:

- Computes simple returns and descriptive statistics.
- Splits observations chronologically and selects eligible assets using training data.
- Constructs ten fully invested, long-only portfolios using linear programming.
- Compares median daily returns, absolute-deviation risk, and portfolio composition.

Risk is measured as mean absolute deviation around the portfolio median. Allocation targets constrain a weighted average of individual asset medians, which differs from the median of portfolio returns. The resulting portfolios are not all points on an efficient frontier.

## 2. Option Delta Estimation

How accurately can machine learning models approximate recorded option deltas relative to an analytical benchmark?

The analysis uses December 2023 S&P 500 futures and call and put options across five strikes. Features include futures price, strike, time to maturity, rolling historical volatility, and option type.

A Random Forest and a neural network are compared with an undiscounted Black-model delta benchmark. Neural network development uses a chronological validation subset within the training sample; the final network is retrained on the full training sample.

### Test-Sample Results

| Model | MSE | R² |
| --- | ---: | ---: |
| Random Forest | 0.022081 | 0.9364 |
| Neural Network | 0.008819 | 0.9746 |
| Black benchmark | 0.004243 | 0.9878 |

Black has the lowest estimation error on this test sample. Diagnostics examine errors over time, across strikes, and by option type. These results do not establish a general ranking across other contracts or periods.

## Running the Notebooks

### Google Colab

Open a notebook using the links below, connect to a runtime, and run the cells in order.

- [Open Portfolio Optimization in Colab](https://colab.research.google.com/github/MnGianmaria/Portfolio-and-option-delta/blob/main/01_portfolio_optimization.ipynb)
- [Open Option Delta Estimation in Colab](https://colab.research.google.com/github/MnGianmaria/Portfolio-and-option-delta/blob/main/02_option_delta_estimation.ipynb)

The portfolio notebook downloads equity data from Yahoo Finance. The option notebook loads the Excel dataset directly from this repository. Internet access is required.

### Local Execution

Download or clone the repository and install the dependencies:

```bash
pip install -r requirements.txt
```

Open the notebooks in Jupyter or another compatible environment and run all cells in order.

## Data and Limitations

**Equity data.** The constituent list comes from the version of the [S&P 500 companies dataset](https://github.com/datasets/s-and-p-500-companies) accessed during retrieval. It does not reconstruct index membership during 2022–2023. This introduces retrospective selection and survivorship bias: evaluation is out-of-sample with respect to weight estimation, but not universe selection. Subsequent downloads may produce different results because of constituent changes, data revisions, or download availability.

**Option data.** The course-provided dataset is stored in [data/sp500_futures_options.xlsx](data/sp500_futures_options.xlsx). Historical volatility is used instead of implied volatility. Time to maturity uses an approximate weekday count, and the provider's delta convention has not been independently verified.

**Scope.** Both analyses use a single chronological split. Portfolio evaluation assumes daily rebalancing and excludes transaction costs. Option analysis estimates contemporaneous recorded deltas and does not evaluate hedging effectiveness. Neither analysis establishes trading profitability.

## Methods and Tools

- **Data preparation:** pandas and NumPy.
- **Portfolio optimization and analytical benchmark:** SciPy.
- **Machine learning:** scikit-learn.
- **Neural networks:** TensorFlow and Keras.
- **Visualization:** Matplotlib.
- **Equity data collection:** yfinance.

## Reproducibility

Both notebooks include saved outputs. Equity inputs are downloaded live, while the option dataset is included in the repository.

Random seeds are set for the machine learning models. Neural network results may still vary across software versions and computing environments. Reported metrics correspond to the saved notebook outputs.

## Authors

Gianmaria Monaco and Leandro Arzilli.

Originally developed for **21046 — Data Science and Machine Learning for Finance**, class 31, Bocconi University, academic year 2025–2026.
