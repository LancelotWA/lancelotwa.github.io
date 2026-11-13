---
layout: post
title: "From Itô's lemma to the Black–Scholes PDE"
date: 2026-11-13
description: A short derivation note.
tags: [stochastic-calculus, derivatives]
---

<!-- TODO: example note — rewrite or delete. To hide the blog entirely, set `nav: false` in _pages/blog.md. -->

Let the underlying follow a geometric Brownian motion $dS_t = \mu S_t\,dt + \sigma S_t\,dW_t$.
For a smooth price function $V(t,S)$, Itô's lemma gives

$$
dV = \left(\partial_t V + \mu S\,\partial_S V + \tfrac12\sigma^2 S^2\,\partial_{SS} V\right)dt + \sigma S\,\partial_S V\,dW_t .
$$

Holding $\Delta = \partial_S V$ shares against a short option removes the $dW_t$ term; by no-arbitrage the hedged portfolio earns $r$, which yields

$$
\partial_t V + rS\,\partial_S V + \tfrac12\sigma^2 S^2\,\partial_{SS} V - rV = 0 .
$$
