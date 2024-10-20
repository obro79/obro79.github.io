---
layout: post
author: Owen Fisher
permalink: https://obro79.github.io/portfolio-optimizer/
---
<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/3.2.0/es5/tex-mml-chtml.js">
</script>
---

# Portfolio Optimization Project

In this project, I applied several advanced mathematical models to construct and optimize a portfolio, including **Classic Portfolio Optimization**, the **Black-Litterman Model**, and several **Objective Functions** and **Risk Measures**. Below is an explanation of the mathematical theory behind each component.

## Classic Portfolio Optimization (Mean-Variance Optimization)

**Mean-Variance Optimization** (MVO), introduced by Harry Markowitz, focuses on optimizing a portfolio’s expected return and risk (variance). The objective is to find a set of asset weights that either maximize return for a given level of risk or minimize risk for a given expected return.

### 1. **Expected Return:**
The **expected return** of a portfolio is a weighted average of the expected returns of the individual assets:

$$
\mu_p = \sum_{i=1}^{N} w_i r_i = \mathbf{w}^T \mathbf{r}
$$

Where:
- $\( \mu_p \)$ is the expected return of the portfolio.
- $\( w_i \)$ is the weight of asset \( i \) in the portfolio.
- $\( r_i \)$ is the expected return of asset \( i \).
- $\( \mathbf{w} \)$ is the vector of asset weights.
- \( \mathbf{r} \) is the vector of expected returns.

### 2. **Portfolio Variance (Risk):**
The **variance** of a portfolio measures the portfolio’s risk, accounting for how the returns of the assets move together (covariance):

$$
\sigma_p^2 = \mathbf{w}^T \Sigma \mathbf{w}
$$

Where:
- \( \sigma_p^2 \) is the portfolio variance.
- \( \Sigma \) is the covariance matrix of asset returns.

### 3. **Optimization Problem:**
The optimization can be set up as:

- **Minimizing Risk:**

$$
\min_{\mathbf{w}} \ \mathbf{w}^T \Sigma \mathbf{w}
$$

  Subject to:

$$
\mathbf{w}^T \mathbf{r} = \mu_p, \quad \sum_{i=1}^{N} w_i = 1, \quad w_i \geq 0 \ (\text{for long-only portfolios})
$$

In this equation:
- The goal is to minimize portfolio variance while achieving a certain expected return \( \mu_p \).
- The sum of weights equals 1 to ensure full investment.
- The weights \( w_i \geq 0 \) for long-only portfolios (no short selling).

## Black-Litterman Model

The **Black-Litterman Model** adjusts the traditional Markowitz optimization by blending market equilibrium returns with investor views. This model allows for incorporating subjective insights into the optimization process, mitigating the sensitivity of inputs in the classic approach.

### 1. **Market Equilibrium Returns:**
In equilibrium, the implied returns \( \Pi \) are reverse-engineered from the market weights \( w_m \) using the following equation:

$$
\Pi = \delta \Sigma w_m
$$

Where:
- \( \delta \) is the risk-aversion coefficient.
- \( \Sigma \) is the covariance matrix of returns.
- \( w_m \) are the market capitalization weights.

### 2. **Investor Views:**
The investor has views on certain assets, which are represented by the matrix \( P \) (linking assets to views) and the expected return vector \( Q \). The uncertainty in the investor’s views is captured by the matrix \( \Omega \).

### 3. **Blended Expected Returns:**
The expected returns \( \Pi_{\text{BL}} \) under the Black-Litterman model are a weighted combination of the market equilibrium returns and the investor views:

$$
\Pi_{\text{BL}} = \left[ (\tau \Sigma)^{-1} + P^T \Omega^{-1} P \right]^{-1} \left[ (\tau \Sigma)^{-1} \Pi + P^T \Omega^{-1} Q \right]
$$

Where:
- \( \tau \) is a scalar reflecting the uncertainty of the equilibrium returns.
- \( P \) is the matrix defining investor views.
- \( Q \) is the vector of expected returns for the views.
- \( \Omega \) is the covariance matrix of the views.

## Objective Functions

Objective functions define what we aim to optimize in the portfolio. I used the following:

### 1. **Maximizing the Sharpe Ratio:**
The **Sharpe Ratio** is a measure of risk-adjusted return. We maximize it to get the highest possible return for each unit of risk:

$$
\text{Sharpe Ratio} = \frac{R_p - R_f}{\sigma_p}
$$

Where:
- \( R_p \) is the expected portfolio return.
- \( R_f \) is the risk-free rate.
- \( \sigma_p \) is the standard deviation of portfolio returns (portfolio risk).

The optimization problem becomes:

$$
\max_{\mathbf{w}} \ \frac{\mathbf{w}^T \mathbf{r} - R_f}{\sqrt{\mathbf{w}^T \Sigma \mathbf{w}}}
$$

### 2. **Minimizing Risk (Variance):**
In this case, the goal is to minimize the portfolio's risk for a given return:

$$
\min_{\mathbf{w}} \ \mathbf{w}^T \Sigma \mathbf{w}
$$

This leads to a low-risk portfolio but doesn't necessarily maximize returns.

### 3. **Maximizing Return:**
This objective maximizes the portfolio’s expected return:

$$
\max_{\mathbf{w}} \ \mathbf{w}^T \mathbf{r}
$$

This aims to maximize profit, but the risk level may be high.

## Risk Measures

To assess and manage risk, I used the following measures:

### 1. **Value-at-Risk (VaR):**
**Value-at-Risk (VaR)** estimates the maximum loss over a specified period for a given confidence level \( \alpha \):

$$
\text{VaR}_{\alpha} = \inf \{ x \in \mathbb{R} : P(L > x) \leq 1 - \alpha \}
$$

Where \( L \) is the loss over the specified time period. For example, a 95% VaR might indicate the portfolio will lose no more than \$1,000 with 95% confidence.

### 2. **Conditional Value-at-Risk (CVaR):**
**CVaR** (also called Expected Shortfall) is the average loss that exceeds the VaR. It is used to capture the risk of extreme losses:

$$
\text{CVaR}_{\alpha} = \mathbb{E}[L \ | \ L > \text{VaR}_{\alpha}]
$$

This is a more conservative risk measure, focusing on tail risk.

### 3. **Maximum Drawdown (MDD):**
**Maximum Drawdown** measures the maximum observed loss from the peak to the trough of the portfolio’s value during a given period:

$$
\text{MDD} = \max_{t \in [0,T]} \left( \frac{\text{peak}_t - \text{trough}_t}{\text{peak}_t} \right)
$$

This gives an idea of the worst-case scenario for potential losses.

---

By using these mathematical models, it enables users to construct portfolios that balance risk and return effectively. The combination of **Classic Portfolio Optimization**, the **Black-Litterman Model**, and these **Objective Functions** and **Risk Measures** allows for a highly customizable and sophisticated approach to portfolio management.