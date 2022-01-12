# Udacity's Artificial Intelligence for Trading Nanodegree

## Project: Trading with Momentum

### Summary of What I Learned

I learned a few basic but essential concepts about implementing a trading strategy from this project. For instance, we can convert daily close prices to other frequencies and utilise them (via converting them to log returns) to construct momentum indicators. Then, these indicators can be used to generate trading signals, and through backtesting, we can project our annualised rate of return. However, it is of crucial importance to do statistical tests on these results since the results alone could be misleading. Hence, I also learned how to carry out a one-sample, one-sided t-test on the observed mean return, leading to a conclusion that the null hypotheses (H<sub>0</sub>) cannot be rejected. Thus, I became aware of the importance of statistical tests and that even though we used many data points, we must consider the possibility that a positive return is deceptive and may not represent the actual future returns.

## Table of content

1. [Project Overview](#overview)
2. [Data Description](#data)
3. [Trading Strategy](#strategy)
4. [Results](#results)
5. [Evaluation](#evaluation)
6. [Conclusions](#conclusions)
7. [Packages and Files](#packages)

***

<a id='overview'></a>
### Project Overview

This project teaches how to implement a trading strategy and evaluate its potential profitability. To that end, a universe of stocks (with a time range) and a textual description of how we can generate a trading signal (based on a momentum indicator) are provided for us by Udacity. These allow us to construct a particular trading signal for the given time range and apply it to our dataset, which produces the portfolio's expected returns. Then, using a statistical test on these returns, we determine whether our investment strategy contains alpha (i.e., the ability to beat the market).

<a id='data'></a>
### Data Description
For this project, we use end of day stock data provided by [Quotemedia](https://www.quotemedia.com/). Although this dataset contains many stocks, we limit our stock universe to those in the S&P 500 and restrict our time range. Moreover, we only plot Apple's stock (AAPL) to display partial results purely for illustrative purposes during the project.

Unfortunately, Udacity does not have a [licence](https://github.com/udacity/artificial-intelligence-for-trading) to redistribute these data; however, they are working on alternatives to this problem.

<a id='strategy'></a>
### Trading Strategy
We aim to use the following trading strategy:

> For each month-end observation period, rank the stocks by previous returns, from the highest to the lowest. Select the top-performing stocks for the long portfolio and the bottom-performing ones for the short one.

Since daily adjusted close prices are given, we first need to resample them into monthly buckets and select the last observation of each month. Then, we can compute the log-returns from these resampled prices as our primary momentum indicator, which we can use to generate trading signals. Finally, according to the strategy description above, we need to select the top and bottom-performing stocks and construct the long and short portfolios accordingly.

> A trading signal is a sequence of trading actions or results that can be used to take trading actions. A common form is to produce a "long" and "short" portfolio of stocks on each date (e.g. end of each month, or any other frequency you desire to trade at). This signal can be interpreted as rebalancing the portfolio on each of those dates, entering long ("buy") and short ("sell") positions as indicated.

<a id='results'></a>
### Results
Although we have generated a trading signal, we have no idea whether it can become profitable. So first, we assume every stock gets an equal investment amount for simplicity. Then, this enables us to compute the net returns for this portfolio, which is the simple arithmetic average of the individual stock returns. Let's see how the portfolio did:

![Portfolio Returns](/images/Result.png)

<a id='evaluation'></a>
### Evaluation

#### Annualised Rate of Return
It is helpful to calculate the annualised rate of return since this allows us to compare the rate of return from this strategy to other quoted rates of return (usually quoted on an annual basis).

#### T-Test
Another test we can do is the so-called t-test. Here, first, we need to decide upon our null hypothesis (H<sub>0</sub>), which in our case is that the actual mean return from the signal is zero. To that end, we perform a one-sample, one-sided t-test on the observed mean return to see if we can reject (H<sub>0</sub>).

Hence, we first compute the t-statistic and then find its corresponding p-value, which will indicate the probability of observing a t-statistic equally or more extreme than the one we observed if the null hypothesis were true.

> A small p-value means that the chance of observing the t-statistic we observed under the null hypothesis is slight and thus casts doubt on the null hypothesis. Therefore, it is good practice to set a desired level of significance or alpha (&alpha;) before computing the p-value, and then reject the null hypothesis if p<&alpha;. A typical value for &alpha; is 0.05 that we also used in the current project.

<a id='conclusion'></a>
### Conclusions

We observed a p-value of 0.071916, which is greater than the &alpha; = 0.05 defied earlier. Since p>&alpha;, we cannot reject the null hypothesis that the actual mean return from the signal is zero, so the 4.02% Annualized Rate of Return may not reflect the future performance of our trading signal. Hence, this trading strategy does not contain alpha.

<a id='packages'></a>
### Packages and Files

Custom packages:
- `helper` and `project_helper` packages contain utility and graph functions.
- `project_tests` include all unit tests for this project
- `tests` generates various test cases for the unit tests

The necessary libraries defined in `requirements.txt` are the followings:
- [colour==0.1.5](https://github.com/vaab/colour)
- [cvxpy==1.0.3](https://github.com/cvxgrp/cvxpy/)
- [cycler==0.10.0](https://matplotlib.org/cycler/)
- [numpy==1.13.3](http://www.numpy.org/)
- [pandas==0.21.1](https://github.com/pandas-dev/pandas)
- [plotly==2.2.3](https://plot.ly/python/)
- [pyparsing==2.2.0](https://github.com/pyparsing/pyparsing/)
- [python-dateutil==2.6.1](https://dateutil.readthedocs.io/en/stable/)
- [pytz==2017.3](https://pythonhosted.org/pytz/)
- [requests==2.18.4](http://docs.python-requests.org/en/master/)
- [scipy==1.0.0](https://www.scipy.org/)
- [scikit-learn==0.19.1](https://scikit-learn.org/stable/)
- [six==1.11.0](https://github.com/benjaminp/six)
- [tqdm==4.19.5](https://tqdm.github.io/)