# Object-Oriented Equity Option Pricing Library (C++)

A compact, extensible C++ library for pricing equity options with two core engines:

1) **Black–Scholes–Merton (BSM)**: closed-form pricing and Delta for European vanilla and digital options.  
2) **Cox–Ross–Rubinstein (CRR)**: binomial tree with backward induction, optional closed-form at the root, and natural support for early exercise.

The codebase is structured with clear abstraction layers to make it easy to add new products or pricers.

---

## Features

- **Products**
  - European **Vanilla**: `Call`, `Put`
  - **Digital**: `DigitalCall`, `DigitalPut`
  - (Optional extensions) **American** and **Asian** scaffolding if you choose to include them
- **Pricers**
  - `BlackScholesPricer` for European Vanilla & Digitals, with Delta
  - `CRRPricer` for European options on a recombining binomial tree
- **Data Structures**
  - `BinaryTree<T>` for storing node data and visualizing trees
- **Model Checks**
  - CRR no-arbitrage guard: `D < R < U`

---

## Mathematical Overview

### Black–Scholes–Merton (European)
Let \(S\) be spot, \(K\) strike, \(r\) risk-free rate, \(\sigma\) volatility, \(T\) time to expiry.

\[
d_1 = \frac{\ln(S/K) + \left(r + \frac{1}{2}\sigma^2\right)T}{\sigma \sqrt{T}}, \quad
d_2 = d_1 - \sigma \sqrt{T}
\]

- **Call price**: \(C = S\,N(d_1) - K e^{-rT} N(d_2)\)  
- **Put price**: \(P = K e^{-rT} N(-d_2) - S\,N(-d_1)\)  
- **Delta (Call)**: \(\Delta = N(d_1)\), **Delta (Put)**: \(\Delta = N(d_1) - 1\)

> Implementation uses `std::erfc` to evaluate the standard normal CDF.

### CRR Binomial Tree
At time step \(n\) and node \(i\):
\[
S(n,i) = S_0 (1+U)^i (1+D)^{n-i}, \quad q = \frac{R - D}{U - D}, \quad R = \text{per-step risk-free growth}
\]

Backward induction:
\[
H(n,i) = \frac{q\,H(n+1,i+1) + (1-q)\,H(n+1,i)}{1+R}
\]

Closed-form at the root (optional):
\[
H(0,0) = \frac{1}{(1+R)^N}\sum_{i=0}^{N} \binom{N}{i} q^i (1-q)^{N-i}\, h\!\big(S(N,i)\big)
\]
