---
layout: default
title: "Lecture 5 — Seasonality, Backward-Shift Operator & the MA(q) Process"
---

<a href="{{ '/ma32024/' | relative_url }}" class="back-link">← MA32024 Time Series</a>

# Lecture 5 — Seasonality, Backward-Shift Operator & the MA(q) Process

---

## Seasonality

The additive model with a seasonal component:

$$X_t = Y_t + m_t + S_t, \qquad S_t = S_{t-d},\; d > 0$$

where $Y_t$ is random, $m_t$ is trend, $S_t$ is seasonality, and $d$ is called the **period**.

Seasonality can be approximately removed via a first-order difference at lag $d$:

$$\nabla_d X_t = (Y_t + m_t + S_t) - (Y_{t-d} + m_{t-d} + S_{t-d}) = \nabla_d Y_t + m_t - m_{t-d}$$

where $m_t - m_{t-d}$ is approximately polynomial.

Beside additive models, we can have **multiplicative models**:

$$X_t = Y_t \cdot m_t \cdot S_t \quad \Longleftrightarrow \quad \log(X_t) = \log(Y_t) + \log(m_t) + \log(S_t)$$

---

## The Backward-Shift Operator $B$

$$BX_t = X_{t-1}$$

The $B$ operator can acquire powers: $B^2 X_t = X_{t-2}$, ..., $B^q X_t = X_{t-q}$.

With this notation, MA(1) becomes:

$$X_t = z_t + \beta B z_t = (1 + \beta B) z_t$$

We associate a characteristic polynomial to this operator:

$$\theta(\lambda) = 1 + \beta\lambda \qquad \text{"characteristic polynomial of MA(1)"}$$

---

## The MA($q$) Process

The general MA($q$) process is:

$$X_t = (1 + \beta_1 B + \beta_2 B^2 + \cdots + \beta_q B^q)\,z_t = z_t + \beta_1 z_{t-1} + \beta_2 z_{t-2} + \cdots + \beta_q z_{t-q}$$

This process has an associated **characteristic polynomial**:

$$\theta(\lambda) = 1 + \beta_1 \lambda + \beta_2 \lambda^2 + \cdots + \beta_q \lambda^q$$

Redefine MA($q$) formally as: $X_t = \theta(B)\,z_t$.

---

## Exercise 2.1: Show MA($q$) is a W.S. Process

**Mean:**

$$\mathbb{E}[X_t] = \mathbb{E}[z_t + \beta_1 z_{t-1} + \cdots + \beta_q z_{t-q}] = 0 + \beta_1 \cdot 0 + \cdots + \beta_q \cdot 0 = 0$$

**Variance** (using $\beta_0 := 1$):

$$\operatorname{Var}[X_t] = \mathbb{E}[X_t^2] = \operatorname{Var}(z_t) + \beta_1^2 \operatorname{Var}(z_{t-1}) + \cdots + \beta_q^2 \operatorname{Var}(z_{t-q}) = \left(1 + \beta_1^2 + \cdots + \beta_q^2\right)\sigma^2 \quad \text{(constant)}$$

**ACVF:** Computing $\gamma(t, \ell) = \operatorname{Cov}(X_t, X_{t+\ell})$, terms of the form $\beta_i \beta_j \operatorname{Cov}(Z_{t-i}, Z_{t+\ell-j})$ are nonzero only when $\ell + i - j = 0$. Fixing $\ell > 0$, all terms with $\ell > q$ vanish. Thus:

$$\gamma(t, \ell) = \sigma^2 \sum_{i=0}^{q-\ell} \beta_i \beta_{i+\ell} \qquad \text{(only depends on } \ell\text{)}$$

so MA($q$) is **weakly stationary**, with ACVF:

$$\gamma(\ell) = \begin{cases} \sigma^2 \displaystyle\sum_{i=0}^{q} \beta_i^2 & \text{if } \ell = 0 \\[6pt] \sigma^2 \displaystyle\sum_{i=0}^{q-\ell} \beta_i \beta_{i+\ell} & \text{if } 0 < \ell \leq q \\[4pt] 0 & \text{otherwise} \end{cases}$$

where $\beta_0 := 1$.

**ACF:**

$$\rho(\ell) = \begin{cases} 1 & \text{if } \ell = 0 \\[4pt] \displaystyle\frac{\displaystyle\sum_{i=0}^{q-\ell} \beta_i \beta_{i+\ell}}{\displaystyle\sum_{i=0}^{q} \beta_i^2} & \text{if } 0 < \ell \leq q \\[8pt] 0 & \text{if } \ell > q \end{cases}$$

> **Key property:** The ACF of an MA($q$) process **cuts off** at lag $q$ — it is exactly zero for $\ell > q$.
