---
layout: default
title: "Lecture 3 — ACVF, ACF & Properties of WS Processes"
---

<a href="{{ '/ma32024/' | relative_url }}" class="back-link">← MA32024 Time Series & Spatial Statistics</a>

# Lecture 3 — ACVF, ACF & Properties of WS Processes

## Recall: Random Walk

$X_t = \sum_{j=1}^t Z_j$ and for $\ell > 0$:

$$\gamma(t, \ell) = \sum_{j=1}^t \sum_{i=1}^{t+\ell} \mathbb{E}[Z_j Z_i] = t\sigma^2$$

If $\ell < 0$: $\gamma(t, \ell) = (t + \ell)\sigma^2$. In any case, the random walk is **not weakly stationary**.

How about its **first difference**?

$$\nabla X_t = X_t - X_{t-1} = Z_t$$

White noise, which is **weakly stationary**.

---

## Example 1.8: The Cauchy Distribution

$X_t \sim \text{Cauchy}(\gamma, x_0)$ (scale, location)

**CDF:** $F(x) = \frac{1}{\pi} \arctan\left(\frac{x - x_0}{\gamma}\right) + \frac{1}{2}$

**PDF:** $f(x) = \frac{1}{\pi \gamma \left(1 + \left(\frac{x - x_0}{\gamma}\right)^2\right)}$

There exist some **strictly stationary** processes which are **not weakly stationary**, because their 1st and/or 2nd moments are infinite or not well defined.

---

The **autocorrelation function** (ACF):

$$\rho(\ell) = \frac{\gamma(\ell)}{\gamma(0)}$$

## Example 1.9: ACVF and ACF of MA(1)

$X_t = Z_t + \beta Z_{t-1}$

$$\gamma(t, \ell) = \text{Cov}(Z_t + \beta Z_{t-1}, Z_{t+\ell} + \beta Z_{t+\ell-1})$$

$$= \gamma_Z(\ell) + \beta \gamma_Z(\ell-1) + \beta \gamma_Z(\ell+1) + \beta^2 \gamma_Z(\ell)$$

$$\gamma(\ell) = \begin{cases} (1 + \beta^2)\sigma^2 & \text{if } \ell = 0 \\ \beta\sigma^2 & \text{if } \ell \in \{-1, 1\} \\ 0 & \text{otherwise} \end{cases}$$

The ACVF of MA(1) is **truncated** for $|\ell| \geq 1$.

$$\rho(\ell) = \begin{cases} 1 & \text{if } \ell = 0 \\ \frac{\beta}{1 + \beta^2} & \text{if } \ell \in \{-1, 1\} \\ 0 & \text{otherwise} \end{cases}$$

---

## Theorem 1.1: Weakly Stationary ACVFs and ACFs

**1. The ACVF of a WS process is a non-negative definite function.** For any real $a_i$ and any $t_1, \ldots, t_n$:

$$\sum_{i=1}^n \sum_{j=1}^n a_i a_j \gamma(t_i - t_j) \geq 0$$

> **Proof:** $\text{Var}(a_1 X_{t_1} + \ldots + a_n X_{t_n}) = \sum_{i=1}^n \sum_{j=1}^n a_i a_j \gamma(t_i - t_j) \geq 0$, as variances are non-negative. $\square$

**2. The ACVF is an even function of $\ell$.**

> **Proof:** $\gamma(-\ell) = \text{Cov}(X_t, X_{t-\ell})$. Use $t' = t - \ell$; $= \text{Cov}(X_{t'}, X_{t'+\ell}) = \gamma(\ell)$. $\square$

**3.** $|\rho(\ell)| \leq 1 \Leftrightarrow -1 \leq \rho(\ell) \leq 1$

> **Proof:** Consider $\lambda_1 X_t + \lambda_2 X_{t+\ell}$:
>
> $$\text{Var}(\lambda_1 X_t + \lambda_2 X_{t+\ell}) = \lambda_1^2 \gamma(0) + \lambda_2^2 \gamma(0) + 2\lambda_1\lambda_2 \gamma(\ell) \geq 0 \quad (*)$$
>
> With $\lambda_1 = 1$, $\lambda_2 = -1$: $2\gamma(0) - 2\gamma(\ell) \geq 0 \Rightarrow \rho(\ell) \leq 1$.
>
> With $\lambda_1 = \lambda_2 = 1$: $2\gamma(0) + 2\gamma(\ell) \geq 0 \Rightarrow \rho(\ell) \geq -1$. $\square$

**4. The ACF does not uniquely identify the underlying stochastic process.**
