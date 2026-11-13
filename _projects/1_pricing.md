---
layout: page
title: Option Pricing Library
description: Black–Scholes, Monte Carlo, Greeks and exotic options.
importance: 1
category: work
github: https://github.com/LancelotWA/Pricing
---

## Problem

Price European and exotic options (Asian, barrier) consistently, and compute their sensitivities (Greeks) for risk management. Closed-form solutions only exist for vanilla payoffs, so a numerical engine is needed for path-dependent products.

## Method

**Black–Scholes (European options).** Under the risk-neutral measure, $dS_t = rS_t\,dt + \sigma S_t\,dW_t$, and

$$
C = S_0\,N(d_1) - K e^{-rT} N(d_2), \qquad
d_{1,2} = \frac{\ln(S_0/K) + (r \pm \tfrac12\sigma^2)T}{\sigma\sqrt{T}} .
$$

**Monte Carlo (path-dependent payoffs).** Paths are simulated exactly on a grid $t_0<\dots<t_n$:

$$
S_{t_{i+1}} = S_{t_i}\exp\!\Big(\big(r-\tfrac12\sigma^2\big)\Delta t + \sigma\sqrt{\Delta t}\,Z_i\Big), \quad Z_i \sim \mathcal N(0,1),
$$

and the price is the discounted mean $\hat V = e^{-rT}\frac1M\sum_{j=1}^M \text{payoff}(S^{(j)})$, with standard error $\hat\sigma/\sqrt M$.
Asian payoff: $\big(\frac1n\sum_i S_{t_i} - K\big)^+$; up-and-out barrier: $(S_T-K)^+\,\mathbf 1_{\{\max_i S_{t_i} < B\}}$.
<!-- TODO: mention variance reduction (antithetic / control variates) if implemented -->

**Greeks.** Analytical for Black–Scholes (e.g. $\Delta = N(d_1)$, $\Gamma = \frac{N'(d_1)}{S_0\sigma\sqrt T}$, $\mathcal V = S_0 N'(d_1)\sqrt T$), finite differences for Monte Carlo prices.

## Results

<!-- TODO: add a convergence plot (MC price vs. number of paths, with BS reference) in assets/img/projects/pricing_convergence.png -->
<!-- {% include figure.liquid path="assets/img/projects/pricing_convergence.png" class="img-fluid rounded" caption="Monte Carlo convergence to the Black–Scholes price." %} -->

| Metric                                        | Value |
| :-------------------------------------------- | :---- |
| MC vs. BS absolute error (European call, M=?) | TODO  |
| Asian call price (parameters?)                | TODO  |
| Runtime for 10⁶ paths                         | TODO  |

## Code

[github.com/LancelotWA/Pricing](https://github.com/LancelotWA/Pricing) — TODO: language / stack (Python? C#?)
