---
layout: default
title: "Lab 2 — Stationarity in R"
---

<a href="{{ '/ma32024/' | relative_url }}" class="back-link">← MA32024 Time Series</a>

# Lab 2 — Stationarity in R

## Aims

- Import or simulate time series data
- Check data are in the right form (a `ts` object)
- Check whether a time series is stationary
- Transform a non-stationary time series into a stationary one (where possible)

---

## Part 1: Data from Packages

Load the `astsa` package and access the five datasets: `flu`, `sales`, `AirPassengers`, `co2`, `EQ5`.

```r
library(astsa)
str(flu)
str(sales)
```

Import external data from CSV and convert to a `ts` object:

```r
recife <- read.csv(file = "Recife.csv", header = FALSE)
recife <- ts(recife$V1, start = c(1953, 1), frequency = 12)
plot(recife)
```

---

## Part 2: Simulating Time Series

### 1. Random Walk ($\sigma^2 = 9$)

```r
z <- rnorm(1000, sd = 3)
simu1 <- cumsum(z)
simu1 <- ts(simu1)
plot(simu1)
```

### 2. Engineered Series (Uniform/Normal)

$$X_t = \begin{cases} N\!\left(0, \frac{1}{3}\right) & \text{if } t \text{ odd} \\ U(-1, 1) & \text{if } t \text{ even} \end{cases}$$

All RVs sampled independently.

```r
tmp <- rep(0, times = 1000)
to <- seq(1, 999, by = 2)
te <- seq(2, 1000, by = 2)
tmp[to] <- rnorm(500, mean = 0, sd = 1/sqrt(3))
tmp[te] <- runif(500, -1, 1)
simu2 <- ts(tmp)
plot(simu2)
```

### 3. MA(1) with $\beta = 0.9$, $\sigma = 1$

Set seed to 6118 before simulating.

### 4. Engineered Series ($X_t \sim N(0, t/100)$)

Variance grows with $t$ — expect non-stationarity.

---

## Part 3: Assessing Stationarity

### Flu

1. Plot the series. Does it appear stationary? Look for trend and seasonality.
2. Use `stl()` to decompose — confirm the presence of trend/seasonal components.

### Sales

1. Reformat as monthly data starting January 1950:

```r
sales12 <- ts(sales, start = c(1950, 1), frequency = 12)
plot(sales12)
```

2. Decompose with `stl()` — clear trend present, no obvious seasonality:

```r
plot(stl(sales12, s.window = "periodic"))
```

3. First difference to remove trend:

```r
dsales12 <- diff(sales12)
plot(dsales12)
plot(stl(dsales12, s.window = "periodic"))
```

Note: differencing reduces length by 1. After differencing, strong seasonality appears.

4. **Kolmogorov–Smirnov test** for constant variance — split series in half and test whether both halves come from the same distribution:

```r
# Original series — likely non-stationary
x <- sales12[1:75]
y <- sales12[76:150]
ks.test(x, y)

# Differenced series — less conclusive
xd <- dsales12[1:75]
yd <- dsales12[76:149]
ks.test(xd, yd)
```

5. Second difference — appears more stationary:

```r
ddsales12 <- diff(dsales12)
plot(ddsales12)

xdd <- ddsales12[1:74]
ydd <- ddsales12[75:148]
ks.test(xdd, ydd)
```

Large p-value confirms same distribution — conclude weak stationarity.

### Air Passengers

1. Plot data — observe increasing trend and seasonality with growing amplitude.
2. For a **multiplicative model** $Y_t = X_t \cdot m_t \cdot s_t$, apply $\log$ to make it additive:

$$\log Y_t = \log X_t + \log m_t + \log s_t$$

3. Difference the log-transformed series to achieve stationarity.

### CO₂ and EQ5

Follow the same workflow: plot, decompose with `stl()`, assess stationarity, difference as needed.

### Simulated Series

- **simu1** (random walk): Not stationary, but first difference is. Verify with plot and KS test.
- **simu2** (uniform/normal): W.S. but not strictly stationary (different marginal distributions at odd/even times).
- **simu3** (MA(1)): Check stationarity using KS test only.
- **simu4** ($\sigma^2 = t/100$): Non-stationary due to time-dependent variance. Verify with KS test.
