---
layout: page
title: Pair Trading on the S&P 500
description: Cointegration-based statistical arbitrage with 3-year backtests.
importance: 2
category: work
github: https://github.com/LancelotWA/PairTrading
---

## Problem

Can a market-neutral strategy exploit temporary mispricings between economically linked S&P 500 stocks, with a stable risk-adjusted return out-of-sample?

## Method

**Pair selection.** For candidate pairs $(A,B)$, estimate the hedge ratio by OLS on log-prices

$$
\log P^A_t = \alpha + \beta \log P^B_t + \varepsilon_t ,
$$

and test the residual $\varepsilon_t$ for stationarity (Engle–Granger, ADF test). Pairs are ranked dynamically using p-values and quantile analysis.

**Signal.** The spread $s_t = \log P^A_t - \beta \log P^B_t$ is standardised on a rolling window:

$$
z_t = \frac{s_t - \mu_t}{\sigma_t}.
$$

Enter short spread when $z_t > z_{\text{in}}$, long spread when $z_t < -z_{\text{in}}$, exit when $|z_t| < z_{\text{out}}$. <!-- TODO: thresholds, window length, stop-loss, transaction costs -->

Mean reversion speed can be read from an Ornstein–Uhlenbeck fit $ds_t = \theta(\mu - s_t)\,dt + \sigma\,dW_t$ (half-life $\ln 2/\theta$).

## Results

Averages over 3-year backtests:

| Metric                      | Value       |
| :-------------------------- | :---------- |
| Sharpe ratio                | **1.35**    |
| Annualised return           | **23.76 %** |
| Maximum drawdown            | **−3.43 %** |

<!-- TODO: add equity curve + z-score plot in assets/img/projects/ and include with figure.liquid -->

Full methodology and results: [report (PDF, French)](/assets/pdf/Rapport_Pair_Trading_FRANCAIS.pdf).

## Code

[github.com/LancelotWA/PairTrading](https://github.com/LancelotWA/PairTrading)
