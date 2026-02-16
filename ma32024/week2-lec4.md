---
layout: default
title: "Lecture 4 — Estimation, Linear Filters & Trend Removal"
---

<a href="{{ '/ma32024/' | relative_url }}" class="back-link">← MA32024 Time Series</a>

# Lecture 4 — Estimation, Linear Filters & Trend Removal

## Estimation

**Estimator of the mean** (sample mean):

$$\bar{X} = \frac{1}{n}\sum_{t=1}^{n} X_t$$

This is an unbiased estimator:

$$\mathbb{E}[\bar{X}] = \mathbb{E}\left[\frac{1}{n}\sum_{t=1}^{n} X_t\right] = \frac{1}{n}\sum_{t=1}^{n}\mathbb{E}[X_t] = \mu$$

**Estimator for the autocovariance function** $\gamma(\ell)$:

$$C_K = \frac{1}{n}\sum_{t=1}^{n-K}(X_t - \bar{X})(X_{t+K} - \bar{X})$$

This estimator is **not unbiased**, but $\mathbb{E}[C_K] \to \gamma(K)$ as $n \to \infty$ — i.e. $C_K$ is **asymptotically unbiased**.

**Estimator for the ACF:**

$$r_K = \frac{C_K}{C_0} = \frac{\displaystyle\sum_{t=1}^{n-K}(X_t - \bar{X})(X_{t+K} - \bar{X})}{\displaystyle\sum_{t=1}^{n}(X_t - \bar{X})^2}$$

---

## 2.2.4: Linear Filters

Given a W.S. stochastic process $\{X_t\}$, we can define another stochastic process $\{Y_t\}$ called a **linear filter**:

$$Y_t = \sum_{k=-\infty}^{\infty} a_k \, X_{t-k}$$

If $\{X_t\}$ is W.S., then $\{Y_t\}$ is also W.S. provided that:

$$\sum_{k=-\infty}^{\infty} |a_k| < \infty$$

**Example 1:** $X_t = Z_t + \beta Z_{t-1}$ (MA(1)). Indeed, $a_0 = 1$, $a_1 = \beta$, $a_k = 0$ $\forall k \notin \{0, 1\}$.

**Example 2:** The first difference at lag $d$: $\nabla_d X_t = X_t - X_{t-d}$. Here $a_0 = 1$, $a_d = -1$, $a_k = 0$ $\forall k \notin \{0, d\}$.

Further, we can generalise the order of finite differences. The **$j$th difference at lag $d$** is:

$$\nabla_d^j X_t = \nabla_d\!\left(\nabla_d^{j-1} X_t\right)$$

**Example:** Second difference, lag 1.

$$\nabla^2 X_t = \nabla(\nabla X_t) = \nabla(X_t - X_{t-1}) = \nabla X_t - \nabla X_{t-1}$$

$$= X_t - X_{t-1} - X_{t-1} + X_{t-2} = X_t - 2X_{t-1} + X_{t-2}$$

This is also a linear filter: $a_0 = 1$, $a_1 = -2$, $a_2 = 1$, $a_k = 0$ $\forall k \notin \{0, 1, 2\}$.

---

## Proposition 1.1

> If $\{X_t\}$ is a W.S. process with a (constant) mean $\mu$ (not necessarily 0) and ACVF $\gamma(\ell)$, then its first difference at lag $d$, $\nabla_d X_t$, is also a W.S. process with **0 mean** and ACVF:
>
> $$\tilde{\gamma}(\ell) = 2\gamma(\ell) - \gamma(\ell + d) - \gamma(\ell - d)$$

**Proof:** Let $Y_t = X_t - X_{t-d}$.

$$\mathbb{E}[Y_t] = \mathbb{E}[X_t] - \mathbb{E}[X_{t-d}] = \mu - \mu = 0$$

$$\tilde{\gamma}(\ell) = \text{Cov}(Y_t, Y_{t+\ell}) = \text{Cov}(X_t - X_{t-d},\; X_{t+\ell} - X_{t-d+\ell})$$

$$= \text{Cov}(X_t, X_{t+\ell}) - \text{Cov}(X_t, X_{t-d+\ell}) - \text{Cov}(X_{t-d}, X_{t+\ell}) + \text{Cov}(X_{t-d}, X_{t-d+\ell})$$

$$= \gamma(\ell) - \gamma(\ell - d) - \gamma(\ell + d) + \gamma(\ell) = 2\gamma(\ell) - \gamma(\ell+d) - \gamma(\ell-d) \quad \square$$

This depends only on $\ell$, so $\nabla_d X_t$ is W.S.

---

## 2.3: Removal of Trend and Seasonal Components

A stochastic process can be added to a trend or a periodic pattern.

**Polynomial trend of order $k$:**

$$M_t(k) := a_0 + a_1 t + a_2 t^2 + \cdots + a_k t^k$$

This is deterministic (not random/stochastic).

> **Proposition 1.2.** If $M_t(k)$ is a polynomial trend, then $\nabla^k M_t(k) = k! \, a_k$.

**Proof:** Induction — exercise.

*Intuition:* Differences eliminate trends. The number of differences needed depends on the order of the polynomial.

> **Corollary 2.1.** If $\{Y_t\}$, $t \in \mathbb{Z}$, is a stationary process, and $X_t = M_t(k) + Y_t$, $t \in \mathbb{Z}$, $k \geq 1$, then
>
> $$\nabla^k X_t = k! \, a_k + \nabla^k Y_t$$
>
> is a stationary process with mean $k! \, a_k$.
