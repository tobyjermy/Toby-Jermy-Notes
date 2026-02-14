---
layout: default
title: "Problem Class 1"
---

<a href="{{ '/ma32024/' | relative_url }}" class="back-link">← MA32024 Time Series & Spatial Statistics</a>

# Problem Class 1

$Z_t$ is a Gaussian RV with mean 0, variance $\sigma^2$. Which process is weakly stationary?

---

## Problem 1a: $X_t = c + tZ_t$, $c \in \mathbb{R}$

- $\mathbb{E}[X_t] = c$
- $\mathbb{E}[X_t^2] = c^2 + t^2\sigma^2$ (depends on $t$)

$\Rightarrow \gamma(t, \ell)$ depends on $t$. **Not weakly stationary.**

---

## Problem 1b: $Y_t = \nabla X_t = X_t - X_{t-1}$

$$\nabla X_t = tZ_t - (t-1)Z_{t-1}$$

- $\mathbb{E}[Y_t] = 0$
- $\mathbb{E}[Y_t^2] = t^2\sigma^2 + (t-1)^2\sigma^2$ (depends on $t$)

**Not weakly stationary.**

ACVF:

$$\gamma(t, \ell) = \begin{cases} t^2\sigma^2 + (t-1)^2\sigma^2 & \text{if } \ell = 0 \\ -t^2\sigma^2 & \text{if } \ell = 1 \\ -(t-1)^2\sigma^2 & \text{if } \ell = -1 \end{cases}$$

---

## Problem 1c: $W_t = Z_t Z_{t-1}$

- $\mathbb{E}[W_t] = 0$ (constant)
- $\mathbb{E}[W_t^2] = \sigma^4$

$$\gamma(t, \ell) = \begin{cases} \sigma^4 & \text{if } \ell = 0 \\ 0 & \text{if } \ell \neq 0 \end{cases}$$

Does not depend on $t$ — **it's weakly stationary.**

---

## Problem 2

$$X_t = \begin{cases} Z_t & \text{if } t \text{ is odd} \\ \frac{Z_t^2 - 1}{\sqrt{2}} & \text{if } t \text{ is even} \end{cases}$$

$Z_t \sim N(0, 1)$. Distribution is not always the same, so **not strictly stationary**.

- $\mathbb{E}[X_t] = 0$ for all $t$.
- $\text{Var}(X_t) = 1$ for odd $t$.
- For even $t$: $\text{Var}\left(\frac{Z_t^2 - 1}{\sqrt{2}}\right) = \frac{1}{2}\mathbb{E}[Z_t^4] - \frac{1}{2}$

**Hint:** $\mathbb{E}[Z_t^4] = 3$ (fourth moment of standard normal), thus $\text{Var}(X_t) = 1$ when $t$ is even.

As all variables are independent for two different indices, $\text{Cov}(X_t, X_{t+\ell}) \neq 0$ only when $\ell = 0$.

$\Rightarrow X_t$ is **weakly stationary**.
