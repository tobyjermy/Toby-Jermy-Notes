---
layout: default
title: "Lecture 8 — The ARIMA Model & Partial Autocorrelation"
---

<a href="{{ '/ma32024/' | relative_url }}" class="back-link">← MA32024 Time Series</a>

# Lecture 8 — The ARIMA Model & Partial Autocorrelation

---

## The ARIMA Model

The ARMA($p$,$q$) model $\Phi(B)X_t = \Theta(B)z_t$ is **stationary**. Using powers of $(I - B)$, we can extend this to non-stationary processes.

Recall the difference operators:

$$(I - B)X_t = X_t - X_{t-1} = \nabla X_t$$

$$(I - B)^2 X_t = (I-B)\nabla X_t = \nabla X_t - \nabla X_{t-1} = \nabla^2 X_t$$

For a **non-stationary** process $X_t$: apply the difference operator $d$ times until the result is stationary:

$$(I - B)^d X_t = W_t \qquad \text{($W_t$ stationary, $X_t$ non-stationary)}$$

The ARIMA process comes from treating $W_t$ as an ARMA process.

> **Definition.** **ARIMA($p$, $d$, $q$)** is the process $X_t$ satisfying:
>
> $$\Phi(B)(I - B)^d X_t = \Theta(B)\,z_t \quad \Longleftrightarrow \quad \Phi(B)W_t = \Theta(B)\,z_t$$

---

## Examples

**Example 5.1:** $W_t = z_t$ $\Leftrightarrow$ ARMA(0,0), and $W_t = (I-B)X_t$ $\Leftrightarrow$ ARIMA(0,1,0).

$$(I - B)X_t = z_t \Rightarrow X_t - X_{t-1} = z_t \Rightarrow X_t = X_{t-1} + z_t \quad \text{"Random Walk"}$$

---

**Example 5.2:** ARIMA(1,1,0): $(1 - \alpha B)(1-B)X_t = z_t$

$$(1 - (1+\alpha)B + \alpha B^2)X_t = z_t \Rightarrow X_t - (1+\alpha)X_{t-1} + \alpha X_{t-2} = z_t$$

$$\Rightarrow X_t = (\alpha+1)X_{t-1} - \alpha X_{t-2} + z_t \quad \Leftrightarrow \text{ARMA(2,0)}$$

---

**Example (apparent AR(2)):** Consider

$$X_t = 1.7\,X_{t-1} - 0.7\,X_{t-2} + z_t$$

$$\Phi(\lambda) = 1 - 1.7\lambda + 0.7\lambda^2, \qquad \Phi(1) = 1 - 1.7 + 0.7 = 0$$

There is a **unit root**: $\Phi(\lambda) = (1 - \lambda)(1 - 0.7\lambda)$. Thus $X_t$ is ARIMA(1,1,0):

$$(1 - 0.7B)(1 - B)X_t = z_t$$

---

## Partial Autocorrelation Function (PACF)

The PACF is a function equal to $\rho(1)$ when $k = 1$, and to a (yet to be defined) $\alpha(k)$ for $k \geq 2$. It is **truncated** for $k > p$ when $X_t$ is AR($p$).

| | AR($p$) | MA($q$) | ARMA($p$,$q$) |
|---|---|---|---|
| **ACF** | tails off | cuts off at $k > q$ | tails off |
| **PACF** | cuts off at $k > p$ | tails off | tails off |

> **Rule of thumb:** Use the ACF and PACF to identify the model order. A clear cutoff in the ACF suggests a pure MA process; a clear cutoff in the PACF suggests a pure AR process; if both tail off, try ARMA.
