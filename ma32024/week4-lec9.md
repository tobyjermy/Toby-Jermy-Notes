---
layout: default
title: "Lecture 9 — Box-Jenkins Methodology & Parameter Estimation"
---

<a href="{{ '/ma32024/' | relative_url }}" class="back-link">← MA32024 Time Series</a>

# Lecture 9 — Box-Jenkins Methodology & Parameter Estimation

---

## Box-Jenkins Methodology

Given a realisation of a stochastic process (time series), we find the model that best fits the data as follows:

---

### Step 1: Preliminary Transformation

Apply log transformation, remove trend/seasonality, etc. We want this to lead to a **weakly stationary** series. If needed, apply differencing:

$$W_t = (I - B)^d X_t$$

---

### Step 2: Stationarity Tests

Tests include the KS test and autocovariance tests. In R: `adf()` (Augmented Dickey-Fuller test). This step determines $d$.

---

### Step 3: Discover Orders $p$, $q$

Analyse the ACF and PACF (recall the table from Lecture 8):

- If there is a clear cutoff in the **ACF** → pure **MA** process.
- If there is a clear cutoff in the **PACF** → pure **AR** process.
- Otherwise, try **ARMA(1,1)** as a first attempt.

The decision on whether a "spike" is meaningful or noise is based on the (not proved here) result that the noise can be modelled as Gaussian. This means:

$$a_k \text{ (ACF) or } \pi_k \text{ (PACF)} \sim N\!\left(0, \frac{1}{n}\right)$$

where $n$ is the number of observations. The 95% significance bounds are $\pm 1.96/\sqrt{n}$.

---

### Example 9.1

| $k$ | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|---|---|
| **ACF** | 1 | −0.52 | −0.04 | 0.13 | −0.09 | −0.01 | 0.1 |
| **PACF** | 1 | −0.52 | −0.43 | −0.21 | −0.09 | −0.20 | −0.1 |

$n = 120$ observations. The variance of the Gaussian is $\frac{1}{n} = \frac{1}{120}$, so $\sigma = \frac{1}{\sqrt{120}} \approx 0.091$.

Significance bounds:

$$-\frac{1.96}{\sqrt{120}} < a_k, \pi_k < \frac{1.96}{\sqrt{120}} \quad \Longleftrightarrow \quad -0.179 < a_k, \pi_k < 0.179$$

Since $a_k = 0$ for $k > 1$ (ACF cuts off after lag 1) $\Rightarrow$ **MA(1) model:**

$$X_t = z_t + \beta z_{t-1}$$

---

### Step 4: Estimate the Parameters

Fit the general ARMA model (with mean $\mu$):

$$X_t - \mu = \sum_{i=1}^p \alpha_i(X_{t-i} - \mu) + z_t + \sum_{i=1}^q \beta_i z_{t-i} \tag{1}$$

Also need to estimate the variance of the **innovation** $z_t$. Methods:

- **(a) Method of Moments** — match sample moments to theoretical ones.
- **(b) Least Squares** — minimise the sum of squared residuals.
- **(c) Maximum Likelihood** — maximise the likelihood function.

In R these are implemented via `arima()`. We use **AIC (Akaike's Information Criterion)** to compare candidate models.

---

### Step 5: Residual Diagnostics

Substitute estimated parameters back into (1) to obtain estimated residuals $\hat{z}_t$. These should be **white noise**. Complete diagnostics (e.g. Ljung-Box test) to verify.

---

### Step 6: Iterate

If unhappy with the residuals, change $p$, $d$, $q$ and return to Step 2.
