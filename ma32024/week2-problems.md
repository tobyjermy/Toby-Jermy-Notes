---
layout: default
title: "Problem Class 2 — Finite Differences & Weak Stationarity"
---

<a href="{{ '/ma32024/' | relative_url }}" class="back-link">← MA32024 Time Series</a>

# Problem Class 2 — Finite Differences & Weak Stationarity

---

## Question 1: Third Difference at Lag 2

Write $\nabla_2^3 X_t$ as a function of $X_t, X_{t-2}, X_{t-4}, X_{t-6}$.

$$\nabla_2^3 X_t = \nabla_2\!\left(\nabla_2\!\left(\nabla_2 X_t\right)\right) = \nabla_2\!\left(\nabla_2(X_t - X_{t-2})\right)$$

$$= \nabla_2\!\left(X_t - X_{t-2} - (X_{t-2} - X_{t-4})\right) = \nabla_2\!\left(X_t - 2X_{t-2} + X_{t-4}\right)$$

$$= X_t - X_{t-2} - 2(X_{t-2} - X_{t-4}) + X_{t-4} - X_{t-6}$$

$$= X_t - 3X_{t-2} + 3X_{t-4} - X_{t-6}$$

---

## Question 2: Alternating Process

Consider the stochastic process:

$$X_0 = 0, \qquad X_t = -X_{t-1} + Z_t, \quad t \in \mathbb{Z}_+$$

where $Z_t \overset{\text{iid}}{\sim} N(0, \sigma^2)$.

### Part (a): Is $X_t$ weakly stationary?

Computing the first few terms: $X_0 = 0$, $X_1 = Z_1$, $X_2 = -Z_1 + Z_2$, $X_3 = Z_1 - Z_2 + Z_3, \ldots$

In general:

$$X_t = \sum_{i=1}^{t} (-1)^{t+i} Z_i \tag{1}$$

**Mean:**

$$\mathbb{E}[X_t] = \sum_{i=1}^{t}(-1)^{t+i}\mathbb{E}[Z_i] = 0$$

**Variance:**

$$\mathbb{E}[X_t^2] = \text{Var}(X_t) = \text{Var}\!\left(\sum_{i=1}^{t}(-1)^{t+i} Z_i\right) \overset{\text{iid}}{=} \sum_{i=1}^{t}\text{Var}(Z_i) = t\sigma^2$$

As $\mathbb{E}[X_t^2]$ depends on $t$, the process is **not weakly stationary**.

### Part (b): Is $\nabla X_t$ weakly stationary?

$\nabla X_t = X_t - X_{t-1}$. Writing out:

$$X_t = (-1)^{t+1}Z_1 + (-1)^{t+2}Z_2 + \cdots + (-1)^{2t-1}Z_{t-1} + (-1)^{2t}Z_t$$

$$X_{t-1} = (-1)^t Z_1 + (-1)^{t+1}Z_2 + \cdots + (-1)^{2t-3}Z_{t-2} + (-1)^{2t-2}Z_{t-1}$$

Then:

$$\nabla X_t = Z_t - 2\sum_{i=1}^{t-1}(-1)^{t+i-1} Z_i$$

In the same way as (1), the variance depends on $t$, so $\nabla X_t$ is **not weakly stationary**.

### Part (c): Is $Y_t = X_t + X_{t-1}$ weakly stationary?

From the definition $X_t = -X_{t-1} + Z_t$, we get:

$$X_t + X_{t-1} = Z_t = Y_t$$

$Y_t$ is **white noise**, which is **weakly stationary**. $\checkmark$

---

## Question 5: Not Strictly Stationary but Weakly Stationary

Consider the stochastic process:

$$X_t = \begin{cases} U(-c, c) & \text{if } t \text{ odd}, \quad c \in \mathbb{R}_+ \\ N(0, 3) & \text{if } t \text{ even} \end{cases}$$

Show $X_t$ is **not strictly stationary** but is **weakly stationary** for some values of $c$.

**Not strictly stationary:** The PDF of $X_t$ for $t$ odd (uniform) is different from the PDF for $t$ even (normal). So the marginal distributions change with $t$.

**Weakly stationary:** Need constant mean and variance.

$$\mathbb{E}[X_t] = \begin{cases} \frac{-c + c}{2} = 0 & t \text{ odd} \\ 0 & t \text{ even} \end{cases}$$

$$\text{Var}(X_t) = \begin{cases} \frac{(2c)^2}{12} = \frac{c^2}{3} & t \text{ odd} \\ 3 & t \text{ even} \end{cases}$$

For constant variance we need $\frac{c^2}{3} = 3$, giving $c^2 = 9$, so $\boxed{c = 3}$.

Also, the only covariance different from 0 is at lag $\ell = 0$ (since all RVs are independent):

$$\gamma(\ell) = \begin{cases} 3 & \text{if } \ell = 0 \\ 0 & \text{otherwise} \end{cases}$$

This is like white noise, so if $c = 3$, $X_t$ is W.S.
