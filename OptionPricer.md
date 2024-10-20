---
layout: default
title: "Language Tests"
permalink: "/option-pricer/"

---
layout: default
title: Options Pricing and Monte Carlo Methods Project
---

<!-- Include MathJax Script -->
<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/3.2.0/es5/tex-mml-chtml.js">
</script>

# Options Pricing and Monte Carlo Methods Project

In this project, I explored the pricing of **European** and **American options**, examined the **Greeks** (sensitivities of option prices to various factors), and employed **Monte Carlo Methods** for asset pricing. Below is an in-depth explanation of these concepts along with the associated mathematical models.

## European Options

A **European option** is a financial derivative that gives the holder the right (but not the obligation) to buy or sell an asset at a specific price (the strike price) on a specific date (the expiration date).

### 1. **Call Option Pricing Formula:**
The price of a European call option can be determined using the **Black-Scholes Formula**:

$$
C = S_0 N(d_1) - K e^{-rT} N(d_2)
$$

Where:
- \( C \) is the price of the call option.
- \( S_0 \) is the current price of the underlying asset.
- \( K \) is the strike price.
- \( r \) is the risk-free interest rate.
- \( T \) is the time to maturity.
- \( N(\cdot) \) is the cumulative distribution function of the standard normal distribution.
- \( d_1 \) and \( d_2 \) are calculated as:

$$
d_1 = \frac{\ln\left(\frac{S_0}{K}\right) + \left(r + \frac{\sigma^2}{2}\right)T}{\sigma \sqrt{T}}
$$

$$
d_2 = d_1 - \sigma \sqrt{T}
$$

Where \( \sigma \) is the volatility of the underlying asset.

### 2. **Put Option Pricing Formula:**
The price of a European put option can be derived from the put-call parity or directly from the Black-Scholes equation:

$$
P = K e^{-rT} N(-d_2) - S_0 N(-d_1)
$$

Where:
- \( P \) is the price of the put option.
- The other terms are defined similarly to the call option formula.

## American Options

An **American option** differs from a European option in that it can be exercised at any point up to the expiration date. This flexibility makes pricing American options more complex.

### 1. **Pricing American Options:**
American options cannot be priced exactly with the Black-Scholes formula due to their early exercise feature. Instead, they are typically priced using numerical methods like the **Binomial Tree Method** or **Monte Carlo simulations** (for approximations).

#### **Binomial Tree Model:**
The Binomial Tree Model breaks the time to expiration into small steps and calculates the price at each node, working backwards from the expiration date.

At each node:
- The asset price can either move up or down by specific factors \( u \) and \( d \).
- At the terminal nodes (expiration), the payoff is calculated, and the option price is determined by discounting backwards through the tree, considering the possibility of early exercise.

### 2. **Binomial Tree Equations:**
The price of an American call or put option at each node is:

$$
C = \max(S_t - K, e^{-r\Delta t} [pC_u + (1 - p)C_d])
$$

Where:
- \( C \) is the option price.
- \( S_t \) is the asset price at time \( t \).
- \( K \) is the strike price.
- \( C_u \) and \( C_d \) are the option prices at the up and down nodes, respectively.
- \( p \) is the probability of an upward movement, calculated as:

$$
p = \frac{e^{r\Delta t} - d}{u - d}
$$

- \( \Delta t \) is the length of each time step.

## The Greeks

The **Greeks** measure the sensitivity of the option price to various factors like the underlying asset price, time, and volatility. These are key risk management tools in options trading.

### 1. **Delta (\( \Delta \)):**
Delta measures the sensitivity of the option price to changes in the underlying asset price:

$$
\Delta = \frac{\partial C}{\partial S}
$$

For a call option:

$$
\Delta_{\text{call}} = N(d_1)
$$

For a put option:

$$
\Delta_{\text{put}} = N(d_1) - 1
$$

### 2. **Gamma (\( \Gamma \)):**
Gamma measures the rate of change of Delta with respect to changes in the underlying asset price:

$$
\Gamma = \frac{\partial^2 C}{\partial S^2}
$$

For both calls and puts:

$$
\Gamma = \frac{N'(d_1)}{S_0 \sigma \sqrt{T}}
$$

### 3. **Vega (\( \nu \)):**
Vega measures the sensitivity of the option price to changes in the volatility of the underlying asset:

$$
\nu = \frac{\partial C}{\partial \sigma} = S_0 \sqrt{T} N'(d_1)
$$

### 4. **Theta (\( \Theta \)):**
Theta measures the sensitivity of the option price to the passage of time (time decay):

For a call option:

$$
\Theta_{\text{call}} = -\frac{S_0 N'(d_1) \sigma}{2 \sqrt{T}} - rK e^{-rT} N(d_2)
$$

For a put option:

$$
\Theta_{\text{put}} = -\frac{S_0 N'(d_1) \sigma}{2 \sqrt{T}} + rK e^{-rT} N(-d_2)
$$

### 5. **Rho (\( \rho \)):**
Rho measures the sensitivity of the option price to changes in the risk-free interest rate:

For a call option:

$$
\rho_{\text{call}} = K T e^{-rT} N(d_2)
$$

For a put option:

$$
\rho_{\text{put}} = -K T e^{-rT} N(-d_2)
$$

## Monte Carlo Methods for Asset Pricing

**Monte Carlo Methods** are used for pricing derivatives, particularly when closed-form solutions (like the Black-Scholes formula) are not available. Monte Carlo simulations rely on the generation of random paths for the underlying asset price to estimate the option price.

### 1. **Monte Carlo Simulation for European Options:**
The general approach to pricing European options using Monte Carlo simulations involves simulating a large number of possible future asset price paths and then calculating the option payoff for each path.

#### **Step 1: Simulating Asset Prices**
The underlying asset prices are modeled using a **Geometric Brownian Motion** (GBM):

$$
S_T = S_0 \exp\left[\left(r - \frac{\sigma^2}{2}\right)T + \sigma \sqrt{T} Z\right]
$$

Where:
- \( S_T \) is the simulated price at time \( T \).
- \( S_0 \) is the current asset price.
- \( r \) is the risk-free rate.
- \( \sigma \) is the volatility.
- \( Z \) is a standard normal random variable.

#### **Step 2: Calculating the Payoff**
For a call option, the payoff is:

$$
\text{Payoff} = \max(S_T - K, 0)
$$

For a put option, the payoff is:

$$
\text{Payoff} = \max(K - S_T, 0)
$$

#### **Step 3: Estimating the Option Price**
The option price is estimated as the discounted average of the payoffs:

$$
\text{Option Price} = e^{-rT} \frac{1}{M} \sum_{i=1}^{M} \text{Payoff}_i
$$

Where \( M \) is the number of simulated paths.

---
layout: default
title: Monte Carlo Methods for Option Pricing
---

# Monte Carlo Methods for Option Pricing

Monte Carlo simulation is a powerful technique used to price options by simulating numerous potential future price paths of the underlying asset. This method is particularly useful when there are no closed-form solutions for the option, such as in the case of **American options** or **complex exotic derivatives**.

## 1. General Approach to Monte Carlo Simulation

The basic idea behind Monte Carlo simulations is to generate multiple random paths for the price of the underlying asset and then calculate the expected payoff of the option across these paths. The option price is then estimated as the discounted average of these payoffs.

### Geometric Brownian Motion (GBM)

In Monte Carlo simulations, the underlying asset price is usually modeled as following **Geometric Brownian Motion (GBM)**. This model assumes that the price of the asset evolves over time with a drift (representing the expected return) and a volatility component (representing randomness in the price movements).

The stochastic differential equation for GBM is:

$$
dS_t = \mu S_t dt + \sigma S_t dW_t
$$

Where:
- \( S_t \) is the asset price at time \( t \).
- \( \mu \) is the drift (or expected rate of return).
- \( \sigma \) is the volatility of the asset.
- \( dW_t \) is a Wiener process (standard Brownian motion), representing the random component.

### Simulating Asset Prices Using GBM

To simulate the price of an asset over time, we discretize the time period into small steps and use the following equation to generate asset prices at each step:

$$
S_{t + \Delta t} = S_t \exp\left[\left( \mu - \frac{\sigma^2}{2} \right) \Delta t + \sigma \sqrt{\Delta t} Z_t\right]
$$

Where:
- \( S_{t + \Delta t} \) is the asset price at the next time step.
- \( S_t \) is the current asset price.
- \( \Delta t \) is the time increment.
- \( Z_t \) is a standard normal random variable \( Z \sim N(0,1) \).

This equation is used to simulate price paths of the underlying asset over time. By repeating this simulation for many paths, we can estimate the expected payoff of the option.

## 2. Monte Carlo Simulation for European Options

European options can only be exercised at the expiration date. Therefore, for European options, we simulate the underlying asset price at the expiration date \( T \) and calculate the payoff at that point.

### Simulating Payoffs

For a **European call option**, the payoff at expiration is:

$$
\text{Payoff}_{\text{call}} = \max(S_T - K, 0)
$$

For a **European put option**, the payoff at expiration is:

$$
\text{Payoff}_{\text{put}} = \max(K - S_T, 0)
$$

Where:
- \( S_T \) is the simulated price of the underlying asset at expiration \( T \).
- \( K \) is the strike price of the option.

### Estimating the Option Price

The Monte Carlo estimate of the option price is the discounted average of the payoffs from all simulated paths. For \( M \) simulated paths, the price of the European option is given by:

$$
\text{Option Price} = e^{-rT} \frac{1}{M} \sum_{i=1}^{M} \text{Payoff}_i
$$

Where:
- \( r \) is the risk-free interest rate.
- \( T \) is the time to maturity.
- \( \text{Payoff}_i \) is the payoff for the \( i \)-th simulated path.
- \( M \) is the total number of simulated paths.

## 3. Monte Carlo Simulation for American Options

American options are more complex because they can be exercised at any time up until expiration. This means we need to account for the possibility of early exercise when pricing these options.

### Least-Squares Monte Carlo (LSMC) Method

One method to price American options using Monte Carlo is the **Least-Squares Monte Carlo (LSMC)** approach. This method approximates the value of the option at each time step by considering whether the option holder would exercise the option early.

The general steps are:
1. Simulate multiple price paths for the underlying asset using GBM.
2. At each time step, determine the payoff from exercising the option early.
3. Use regression to estimate the continuation value (i.e., the value of holding the option) as a function of the asset price.
4. If the immediate exercise payoff is greater than the estimated continuation value, the option is exercised; otherwise, it is continued to the next step.

### American Option Payoff

At each time step \( t \), the payoff for an American call option is:

$$
\text{Payoff}_{\text{call}} = \max(S_t - K, 0)
$$

For an American put option, the payoff is:

$$
\text{Payoff}_{\text{put}} = \max(K - S_t, 0)
$$

By simulating multiple paths and using the LSMC approach, we can estimate the value of the American option by comparing the continuation value to the exercise payoff at each step.

## 4. Accuracy and Convergence of Monte Carlo Methods

The accuracy of Monte Carlo simulations depends on the number of simulated paths \( M \). As the number of simulations increases, the accuracy of the option price estimate improves.

The error in Monte Carlo simulations typically decreases at the rate of:

$$
\text{Error} \propto \frac{1}{\sqrt{M}}
$$

This means that to reduce the error by half, we need to quadruple the number of simulations.

---

In this project, I used Monte Carlo methods to simulate both **European** and **American options**. For European options, I applied the Black-Scholes model for validation and compared it with the Monte Carlo results. For American options, I implemented the **Least-Squares Monte Carlo** method to handle the possibility of early exercise. These methods allowed for flexible and accurate pricing of options in complex scenarios where analytical solutions are not feasible.



