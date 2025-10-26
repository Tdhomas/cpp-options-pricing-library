# C++ Options Pricing Library  
### Black-Scholes, Cox-Ross-Rubinstein (CRR), Monte-Carlo — Object-Oriented Financial Engineering Project

This project implements a modular pricing library for equity options in modern C++.  
It was developed as part of a university financial engineering course focused on derivative pricing models and quantitative software design.

The objective is to bridge **theory and practice**: taking mathematical pricing frameworks and transforming them into clean, extensible code architectures suitable for production-style research.

---

## 📌 Learning and Project Objectives

### 1️⃣ Introduction to Financial Options  
Fundamentals of European and American options, payoff functions, arbitrage-free valuation, and market usage.

### 2️⃣ C++ Programming Foundations for Quants  
Application of:
- Object-oriented programming  
- Inheritance and polymorphism  
- Abstract base classes for product hierarchies  
- Clean interfaces and encapsulation  

### 3️⃣ Black–Scholes–Merton Pricer  
Analytical pricing for European options including:
- Closed-form price
- Delta (sensitivity to underlying price)
- Support for vanilla and digital payoffs

The model uses the standard normal CDF via `std::erfc`.

### 4️⃣ Cox-Ross-Rubinstein (CRR) Binomial Model  
Backward-induction algorithm over a recombining tree for European options.
- Includes no-arbitrage validation (`D < R < U`)
- Optional explicit closed-form binomial solution at the root
- Tree stored & visualized using a reusable `BinaryTree<T>` template

### 5️⃣ Monte-Carlo Simulations  
Pricing by simulating stochastic asset paths.
- Statistical estimation of fair value
- Convergence testing
- Comparison vs. analytic pricing

### 6️⃣ Advanced Concepts  
Extensions for:
- Path-dependent options (Asian structure in place)
- Early exercise support (American option architecture)
- Computational efficiency considerations

---

## ✅ Features Summary

| Category | Capabilities |
|--------|--------------|
| Products | Call, Put, Digital Calls/Puts (European) |
| Pricing Engines | BSM, CRR Tree, Monte-Carlo |
| Greeks | Delta (BSM) |
| Data Structures | Generic binary tree with printer |
| Model Risk Controls | Arbitrage condition checks |
