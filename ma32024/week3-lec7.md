---
layout: default
title: "Lecture 7 — The ARMA Process: Invertibility & Causality"
---

<a href="{{ '/ma32024/' | relative_url }}" class="back-link">← MA32024 Time Series</a>

# Lecture 7 — The ARMA Process: Invertibility & Causality

---

## The ARMA Process

ARMA combines AR and MA components into one useful weakly stationary process.

**ARMA($p$,$q$):**

$$X_t = \alpha_1 X_{t-1} + \cdots + \alpha_p X_{t-p} + z_t + \beta_1 z_{t-1} + \cdots + \beta_q z_{t-q}$$

Using the backward-shift operator $B$:

$$\Phi(B)\,X_t = \Theta(B)\,z_t$$

where $\Phi(\lambda) = 1 - \alpha_1\lambda - \cdots - \alpha_p\lambda^p$ and $\Theta(\lambda) = 1 + \beta_1\lambda + \cdots + \beta_q\lambda^q$.

---

> **Definition 2.2 (Invertible).** An ARMA($p$,$q$) process is **invertible** if there exists a sequence of constants $\{a_i,\, i \in \mathbb{Z}\}$ such that:
>
> - $\sum_i |a_i| < \infty$
> - $z_t = X_t - \sum_{i=1}^\infty a_i X_{t-i}$ &emsp; **(AR($\infty$) representation)** &emsp; (3)
>
> Written as $X_t = \sum_{i=1}^\infty a_i X_{t-i} + z_t$. &emsp; (4)

> **Definition 2.3 (Causal).** An ARMA process is **causal** if there exists a sequence of constants $\{c_i,\, i \in \mathbb{Z}_+\}$ such that:
>
> - $\sum_i |c_i| < \infty$
> - $X_t = \sum_{i=1}^\infty c_i z_{t-i} + z_t$ &emsp; **(MA($\infty$) representation)** &emsp; (5)

---

> **Theorem 3.1.** Assume that the characteristic polynomials $\Theta(\lambda)$ and $\Phi(\lambda)$, $\lambda \in \mathbb{C}$, have no common roots. Then:
>
> - ARMA($p$,$q$) is **invertible** iff all roots of $\Theta(\lambda)$ lie **outside** the complex unit disc: $\{z \in \mathbb{C} : |z| \leq 1\}$.
> - ARMA($p$,$q$) is **causal** iff all roots of $\Phi(\lambda)$ lie outside the complex unit disc.

---

## Exercise 3.2: Condition on $\beta$ for MA(1) to be Invertible

MA(1): $X_t = z_t + \beta z_{t-1}$ $\Leftrightarrow$ ARMA(0,1) with $\Phi(\lambda) = 1$, $\Theta(\lambda) = 1 + \beta\lambda$.

Roots of $\Theta(\lambda)$: $\Theta(\lambda) = 0 \Leftrightarrow 1 + \beta\lambda = 0 \Rightarrow \lambda = -\dfrac{1}{\beta}$.

$$|\lambda| = \frac{1}{|\beta|} > 1 \iff |\beta| < 1$$

$\Rightarrow$ **MA(1) is invertible if and only if $|\beta| < 1$.**

Similarly, **AR(1) is causal if and only if $|\alpha| < 1$.**

---

## Example 3.1: ARMA(1,1) Process

$$X_t = 0.6\,X_{t-1} + z_t - 0.2\,z_{t-1}$$

**Characteristic polynomials:** $\Phi(\lambda) = 1 - 0.6\lambda$, $\Theta(\lambda) = 1 - 0.2\lambda$.

**Causality:** $\Phi(\lambda) = 0 \Rightarrow \lambda = \dfrac{5}{3} > 1$ $\Rightarrow$ **Causal** → admits MA($\infty$) representation.

**Invertibility:** $\Theta(\lambda) = 0 \Rightarrow \lambda = 5 > 1$ $\Rightarrow$ **Invertible** → admits AR($\infty$) representation.

**Finding the MA($\infty$) representation** (since the process is causal):

$$X_t = (1 - 0.6B)^{-1}(1 - 0.2B)\,z_t = \left(\sum_{i=0}^\infty 0.6^i B^i\right)(1 - 0.2B)\,z_t$$

$$= (1 + 0.6B + 0.6^2 B^2 + \cdots)(1 - 0.2B)\,z_t$$

$$= (1 + 0.4B + 0.4(0.6)B^2 + 0.4(0.6^2)B^3 + \cdots)\,z_t$$

$$\boxed{X_t = z_t + \sum_{i=1}^\infty 0.4\,(0.6^{i-1})\,z_{t-i}}$$

(MA($\infty$) representation)
