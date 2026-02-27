---
layout: default
title: "Problem Class 3 — ARMA(1,1) ACVF & MA(1) Invertibility"
---

<a href="{{ '/ma32024/' | relative_url }}" class="back-link">← MA32024 Time Series &amp; Spatial Statistics</a>

# Problem Class 3 — ARMA(1,1) ACVF & MA(1) Invertibility

---

## Question 1: ARMA(1,1) — Causality, Invertibility & ACVF

Consider the ARMA(1,1) process:

$$X_t = 0.5X_{t-1} + Z_t - 0.3Z_{t-1}$$

### Part (a): Is the process causal and invertible?

Writing in operator form $\phi(B)X_t = \theta(B)Z_t$:

$$(1 - 0.5B)X_t = (1 - 0.3B)Z_t$$

So $\phi(\lambda) = 1 - 0.5\lambda$ and $\theta(\lambda) = 1 - 0.3\lambda$.

**Causality:** $\phi(\lambda) = 0 \Leftrightarrow \lambda = 2 > 1$. So the process is **causal**.

**Invertibility:** $\theta(\lambda) = 0 \Leftrightarrow \lambda = \tfrac{10}{3} > 1$. So the process is **invertible**.

> **Remark.** The roots of $\phi$ and $\theta$ must not be common (otherwise the model is reducible).

### Part (b): ACVF for the generic ARMA(1,1) process

Write the generic ARMA(1,1) as:

$$X_t = \alpha X_{t-1} + Z_t + \beta Z_{t-1} \tag{1}$$

**MA($\infty$) representation.** Applying $(1-\alpha B)^{-1}$:

$$X_t = (1-\alpha B)^{-1}(1+\beta B)Z_t = (1 + \alpha B + \alpha^2 B^2 + \cdots)(1+\beta B)Z_t$$

$$= \left(1 + \sum_{i=1}^{\infty}(\alpha+\beta)\alpha^{i-1}B^i\right)Z_t = Z_t + \sum_{i=1}^{\infty}(\alpha+\beta)\alpha^{i-1}Z_{t-i} \tag{2}$$

**Key expectations** (from (2), using $Z_t \sim \text{WN}(0,\sigma^2)$):

$$\mathbb{E}[Z_t X_t] = \mathbb{E}[Z_t^2] + \sum_{i=1}^{\infty}(\alpha+\beta)\alpha^{i-1}\mathbb{E}[Z_{t-i}Z_t] = \sigma^2$$

$$\mathbb{E}[Z_{t-1}X_t] = \mathbb{E}[Z_{t-1}Z_t] + \sum_{i=1}^{\infty}(\alpha+\beta)\alpha^{i-1}\mathbb{E}[Z_{t-i}Z_{t-1}] = (\alpha+\beta)\sigma^2$$

**Yule–Walker equations.** Multiplying (1) through by $X_t$ and taking expectations:

$$\gamma(0) = \alpha\,\mathbb{E}[X_{t-1}X_t] + \mathbb{E}[Z_t X_t] + \beta\,\mathbb{E}[Z_{t-1}X_t] = \alpha\gamma(1) + \sigma^2 + \beta(\alpha+\beta)\sigma^2$$

$$\boxed{\gamma(0) = \alpha\gamma(1) + \bigl(1+\beta(\alpha+\beta)\bigr)\sigma^2} \tag{5}$$

Multiplying (1) through by $X_{t-1}$ and taking expectations ($\mathbb{E}[Z_t X_{t-1}] = 0$ since $Z_t$ is independent of the past):

$$\gamma(1) = \alpha\,\mathbb{E}[X_{t-1}^2] + \mathbb{E}[Z_t X_{t-1}] + \beta\,\mathbb{E}[Z_{t-1}X_{t-1}] = \alpha\gamma(0) + \beta\sigma^2$$

$$\boxed{\gamma(1) = \alpha\gamma(0) + \beta\sigma^2} \tag{6}$$

**Solving (5) and (6) simultaneously:**

$$\gamma(0) = \sigma^2\,\frac{1+\beta^2+2\alpha\beta}{1-\alpha^2}, \qquad \gamma(1) = \sigma^2\,\frac{(1+\alpha\beta)(\alpha+\beta)}{1-\alpha^2} \tag{7}$$

**For $\ell \geq 2$.** Multiplying (1) by $X_{t-\ell}$ (with $\ell \geq 2$), both $Z_t$ and $Z_{t-1}$ are uncorrelated with $X_{t-\ell}$, so:

$$\gamma(2) = \alpha\,\mathbb{E}[X_{t-1}X_{t-2}] = \alpha\gamma(1)$$

and in general:

$$\gamma(\ell) = \alpha\,\gamma(\ell-1), \quad \ell \geq 2 \tag{8}$$

**Applied to our ARMA(1,1)** with $\alpha = 0.5$, $\beta = -0.3$, and using $\gamma(\ell) = \gamma(-\ell)$ for $\ell < 0$:

$$\gamma(\ell) = \begin{cases} \dfrac{79}{75}\,\sigma^2 & \ell = 0 \\[8pt] \dfrac{17}{75}\,\sigma^2 & \ell = 1 \\[8pt] 0.5\,\gamma(\ell-1) & \ell \geq 2 \end{cases}$$

---

## Question 2: MA(1) — Non-Invertibility

Consider:

$$X_t = Z_t - 7Z_{t-1}, \quad \text{MA(1) with } \beta = -7$$

**Invertibility:** $\theta(\lambda) = 1 - 7\lambda = 0 \Leftrightarrow \lambda = \tfrac{1}{7} < 1$. So the process is **not invertible**.

**ACVF** (cutoff property of MA($q$)):

$$\gamma(\ell) = \begin{cases} \sigma^2(1+\beta^2) & \ell = 0 \\ \sigma^2\beta & \ell = 1 \\ 0 & \ell \geq 2 \end{cases} \qquad \gamma(\ell) = \gamma(-\ell) \text{ for } \ell < 0$$

Substituting $\beta = -7$:

$$\gamma(\ell) = \begin{cases} 50\sigma^2 & \ell = 0 \\ -7\sigma^2 & \ell = 1 \\ 0 & \ell \geq 2 \end{cases}$$

**ACF:**

$$\rho(\ell) = \frac{\gamma(\ell)}{\gamma(0)} = \begin{cases} 1 & \ell = 0 \\[4pt] -\dfrac{7}{50} & \ell = 1 \\[4pt] 0 & \ell \geq 2 \end{cases}$$
