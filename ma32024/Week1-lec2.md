---
layout: default
title: "Lecture 2 — Mean Function, Weak Stationarity & ACVF"
---

<a href="{{ '/ma32024/' | relative_url }}" class="back-link">← MA32024 Time Series & Spatial Statistics</a>

# Lecture 2 — Mean Function, Weak Stationarity & ACVF

**Recall:** A strictly stationary stochastic process must have RVs $X_t$ all with the same distribution as $F_t(x) = F_{t+\ell}(x)$. Many artificial stochastic processes can be built using the same PDF for each $X_t$, but this is unlikely in practice. We need a less stringent version.

## 1st and 2nd Moment of a Distribution

$\mathbb{E}[\xi^k]$ is the $k$-th moment where $\mathbb{E}[|\xi|^k] < \infty$.

> **Definition 1.5: Mean Function.** The **mean function** $\mu_t$ of a stochastic process is defined as its expectation:
>
> $$\mu_t = \mathbb{E}[X_t], \quad t \in T$$

> **Definition 1.6: Variance Function.** The **variance function** $\sigma_t^2$ of a stochastic process is the variance of each RV:
>
> $$\sigma_t^2 = \mathbb{E}[(X_t - \mu_t)^2], \quad t \in T$$

---

> **Definition 1.7: First Order Stationarity.** A process is **1st moment stationary** if:
> 1. $\mathbb{E}[|X_t|] < \infty$ (1st moment exists)
> 2. $\mathbb{E}[X_t] = \mu_t = \mu$ $\forall t \in T$ (1st moment is constant)

---

> **Definition 1.8: Autocovariance Function (ACVF).** The **autocovariance function** $\gamma(t_i, t_j)$ of a stochastic process is the covariance of $X_{t_i}, X_{t_j}$:
>
> $$\gamma(t_i, t_j) = \mathbb{E}[(X_{t_i} - \mu_{t_i})(X_{t_j} - \mu_{t_j})]$$

Since $t \in T \subseteq \mathbb{Z}$, we consider the integer separation $\ell$ (the **lag**):

$$\gamma(t, \ell) = \text{Cov}(X_t, X_{t+\ell}) = \mathbb{E}[(X_t - \mu_t)(X_{t+\ell} - \mu_{t+\ell})]$$

---

> **Definition 1.9: Weak Stationarity.** A stochastic process $\{X_t, t \in T\}$ is **weakly stationary** if:
> - $\mathbb{E}[|X_t|] < \infty$ and $\mathbb{E}[|X_t|^2] < \infty$
> - $\mathbb{E}[X_t] = \mu_t = \mu$ = constant
> - $\gamma(t, \ell) = \gamma(\ell)$ → Constant variance

---

## Example: White Noise is Weakly Stationary

- $\mathbb{E}[Z_t] = 0$ $\forall t \in \mathbb{Z}$; $\mathbb{E}[Z_t^2] = \sigma^2$
- $\mu_t = 0$ = constant

$$\gamma(t, \ell) = \text{Cov}(Z_t, Z_{t+\ell}) = \mathbb{E}[Z_t Z_{t+\ell}] = \begin{cases} \sigma^2 & \ell = 0 \\ 0 & \ell \neq 0 \end{cases}$$

By independence. As $\gamma(t, \ell)$ only depends on $\ell$, white noise is **weakly stationary**.

---

## Example: Weak Stationarity of the Random Walk

$X_t = \sum_{j=1}^t Z_j$

- $\mathbb{E}[X_t] = 0$
- $\gamma(t, \ell) = \mathbb{E}[X_t X_{t+\ell}] = \sum_{j=1}^t \sum_{i=1}^{t+\ell} \mathbb{E}[Z_j Z_i] = t\sigma^2$

Thus the **random walk is not weakly stationary**.
