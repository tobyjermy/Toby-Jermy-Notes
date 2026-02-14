---
layout: default
title: "Lecture 1 — R Lab: White Noise, Random Walk, MA(1)"
---

<a href="{{ '/ma32024/' | relative_url }}" class="back-link">← MA32024 Time Series & Spatial Statistics</a>

# Lecture 1 — R Lab: White Noise, Random Walk, MA(1)

**Coursework:** Produce PDF from RMD which has both text and code. This will be uploaded through the same system that we hand our problem sheets in.

A specific class (type of data) used in R to represent a time series (`ts`). Thus `x1 <- as.ts(z)` creates a time series object.

## White Noise

The random variable $Z_t$ representing white noise has probability density function equal to a Gaussian with mean zero and variance $\sigma^2$.

$$X_t = Z_t, \quad t \in \mathbb{Z}$$

In R, random values for this distribution are obtained with `rnorm`. The vector produced is transformed into an object of class `ts`.

```r
# Fixed seed for data reproducibility
set.seed(6612)

# Vector of 1000 normal values (mean 0, st. dev. 1)
z <- rnorm(1000)

# White noise (time series)
x1 <- as.ts(z)

# Plot
plot(x1)

# Add the z=0 mean line as reference
abline(h=0, lwd=2, col=2)
```

## The Random Walk

This is defined with the help of $Z_t$ by the following expression:

$$X_0 = 0, \quad X_t = X_{t-1} + Z_t, \quad t \in \mathbb{Z}_+$$

Equivalently: $X_t = \sum_{i=1}^t Z_i$

In R we can reproduce the random walk using `cumsum` (cumulative sum), because $X_t$ is the cumulative sum of the first $t$ values of $Z_i$.

```r
# First five positive integers
v <- 1:5
print(v)

# Cumulative sum
cv <- cumsum(v)
print(cv)
```

```r
# Fixed seed for data reproducibility
set.seed(1932)

z <- rnorm(1000)
x2 <- cumsum(z)
x2 <- as.ts(x2)

plot(x2)
abline(h=0, lwd=2, col=2)
```

**Random Walk:** Steps, frequency the process crosses the mean line is slow which differs to white noise.

## The MA(1) Process (Moving Average)

$$X_t = Z_t + \beta Z_{t-1}, \quad t \in \mathbb{Z}, \ \beta \in \mathbb{R}$$

```r
# Fixed seed for data reproducibility
set.seed(7711)

z <- rnorm(1000)

# Sum with "shifted" vector. Beta=0.8
x3 <- z + 0.8 * c(0, z[-1000])

x3 <- as.ts(x3[2:1000])
plot(x3)
abline(h=0, lwd=2, col=2)
```

The MA(1) with $\beta=0.8$ looks less dense than white noise — adjacent values tend to have the same direction and cross the zero line less frequently. The opposite happens with negative $\beta$.

```r
# Fixed seed for data reproducibility
set.seed(1624)

z <- rnorm(1000)
x4 <- z - 0.8 * c(0, z[-1000])
x4 <- as.ts(x4[2:1000])

# Comparison of three time series
par(mfrow=c(3,1))
par(mar = c(1,2,0.1,1))
plot(x1); legend(950,-2.2,legend="White Noise", fill=TRUE, bg="white", cex=0.5)
abline(h=0, lwd=2, col=2)
par(mar = c(1,2,0.1,1))
plot(x3); legend(930,-3.3,legend="MA(1), beta=0.8", fill=TRUE, bg="white", cex=0.5)
abline(h=0, lwd=2, col=2)
par(mar = c(1,2,0.1,1))
plot(x4); legend(930,-3.2,legend="MA(1), beta=-0.8", fill=TRUE, bg="white", cex=0.5)
abline(h=0, lwd=2, col=2)
```

## Autocorrelation and the `stl` Function

```r
set.seed(6612)
z <- rnorm(1001)
x1 <- as.ts(z[1:1000])
x2 <- z + 0.8 * c(0, z[-1001])
x2 <- as.ts(x2[2:1001])
```

Seasonality is added through a sinusoidal function: $Y_t = X_t + A \sin(2\pi k \cdot t/1000)$ where $A$ determines the amplitude and $k$ determines the number of oscillations.

```r
t <- 0:999
A <- 10; k <- 6
y1 <- x1 + A * sin(2*pi*k*t/1000)
y2 <- x2 + A * sin(2*pi*k*t/1000)

plot(y1)
plot(y2)
```

A **trend** is added: $W_t = X_t + A \sin(2\pi k \cdot t/1000) + Bt + C$

```r
B <- 0.1; C <- 5
w1 <- y1 + B*t + C
w2 <- y2 + B*t + C
plot(w1)
plot(w2)
```

The `stl` function decomposes a time series into trend, seasonality, and remainder. Requires correct frequency setting:

```r
# Redefine with proper frequency (120 obs/year for 6 years)
set.seed(6612)
t <- 0:719
z <- rnorm(721)
x1 <- ts(z[1:720], start=0, end=(6-1/120), frequency=120)
y1 <- x1 + A*sin(2*pi*k*t/720)
w1 <- y1 + B*t + C

# Decomposition
deco <- stl(w1, s.window="periodic")
plot(deco)
```

## Autocovariance and Autocorrelation

For **white noise**: $\gamma(\tau) = \sigma^2$ if $\tau = 0$, and $0$ if $\tau \neq 0$.

For the **MA(1)** process with parameter $\beta$:

$$\gamma(\tau) = \begin{cases} (1 + \beta^2)\sigma^2 & \tau = 0 \\ \beta\sigma^2 & |\tau| = 1 \\ 0 & |\tau| > 1 \end{cases}$$

```r
# Autocovariance for the white noise (spike at tau=0)
acf(x1, type="covariance")

# Autocovariance for the MA(1) (spikes at tau=0 and tau=1)
acf(x2, type="covariance")
```

If the `type` argument is not included (default), `acf` computes the autocorrelation function.
