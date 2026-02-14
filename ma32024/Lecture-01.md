---
layout: default
title: "Lecture 1 — Stationarity and Autocovariance"
---

<a href="{{ '/ma32024/' | relative_url }}" class="back-link">← MA32024 Time Series & Spatial Statistics</a>

# Lecture 1 — Stationarity and Autocovariance

## Weak Stationarity

> **Definition.** A time series $\{X_t\}$ is **weakly stationary** (or second-order stationary) if:
> 1. $\mathbb{E}[X_t] = \mu$ for all $t$,
> 2. $\text{Cov}(X_t, X_{t+h}) = \gamma(h)$ depends only on the lag $h$.

The function $\gamma(h) = \text{Cov}(X_t, X_{t+h})$ is the **autocovariance function** (ACVF).

## The MA(1) Process

Consider the MA(1) process $X_t = Z_t + \beta Z_{t-1}$, where $Z_t \sim \text{WN}(0, \sigma^2)$.

The autocovariance function is:

$$
\gamma(h) = \begin{cases}
(1 + \beta^2)\sigma^2 & h = 0 \\
\beta \sigma^2 & |h| = 1 \\
0 & |h| \geq 2
\end{cases}
$$

and the autocorrelation function:

$$
\rho(h) = \frac{\gamma(h)}{\gamma(0)} = \begin{cases}
1 & h = 0 \\
\frac{\beta}{1 + \beta^2} & |h| = 1 \\
0 & |h| \geq 2
\end{cases}
$$

## Code: Simulating MA(1)

```python
import numpy as np
import matplotlib.pyplot as plt

np.random.seed(42)
n = 200
beta = 0.8
sigma = 1.0

Z = np.random.normal(0, sigma, n + 1)
X = Z[1:] + beta * Z[:-1]

fig, axes = plt.subplots(2, 1, figsize=(10, 5))
axes[0].plot(X)
axes[0].set_title(f'MA(1) with β = {beta}')
axes[0].set_xlabel('t')

# Sample ACF
from statsmodels.graphics.tsaplots import plot_acf
plot_acf(X, lags=20, ax=axes[1])
axes[1].set_title('Sample ACF')
plt.tight_layout()
plt.show()
```

---

*These are example notes — replace with your own lecture content.*
