---
layout: default
title: "Lecture 6 — The Autoregressive Process AR(p)"
---

<a href="{{ '/ma32024/' | relative_url }}" class="back-link">← MA32024 Time Series</a>

# Lecture 6 — The Autoregressive Process AR($p$)

---

## The AR($p$) Process

$$\text{AR}(p): \quad X_t = \alpha_1 X_{t-1} + \alpha_2 X_{t-2} + \cdots + \alpha_p X_{t-p} + z_t$$

Or equivalently: $X_t - \alpha_1 X_{t-1} - \cdots - \alpha_p X_{t-p} = z_t$, which gives:

$$(I - \alpha_1 B - \alpha_2 B^2 - \cdots - \alpha_p B^p)\,X_t = z_t$$

Associated **characteristic polynomial**:

$$\Phi(\lambda) = 1 - \alpha_1 \lambda - \alpha_2 \lambda^2 - \cdots - \alpha_p \lambda^p \quad \Longleftrightarrow \quad \Phi(B)\,X_t = z_t$$

---

## Properties of AR(1)

$(I - \alpha B)X_t = z_t$ or $X_t = \alpha X_{t-1} + z_t$.

Substituting repeatedly:

$$X_t = \alpha(\alpha X_{t-2} + z_{t-1}) + z_t = \alpha^2 X_{t-2} + \alpha z_{t-1} + z_t$$

$$X_t = \alpha^3 X_{t-3} + \alpha^2 z_{t-2} + \alpha z_{t-1} + z_t$$

After $k$ iterations:

$$X_t = \alpha^{k+1} X_{t-k-1} + \alpha^k z_{t-k} + \alpha^{k-1} z_{t-k+1} + \cdots + \alpha z_{t-1} + z_t$$

**Claim:** $\alpha^{k+1} X_{t-k-1} \to 0$ as $k \to \infty$ when $|\alpha| < 1$.

Using $\mathbb{E}[X_t^2] = \omega^2$ (constant) and $\mathbb{E}[X_t] = 0$ for a weakly stationary process:

$$\lim_{k \to \infty} \mathbb{E}\!\left[\left(\alpha^{k+1} X_{t-k-1}\right)^2\right] = \lim_{k \to \infty} \alpha^{2(k+1)} \mathbb{E}[X_{t-k-1}^2] = \omega^2 \lim_{k \to \infty} \alpha^{2(k+1)} = 0 \quad \text{when } |\alpha| < 1$$

When $|\alpha| < 1$:

$$X_t = \sum_{j=0}^\infty \alpha^j z_{t-j} = z_t + \sum_{j=1}^\infty \alpha^j z_{t-j}$$

This is called the **MA($\infty$) representation** of AR(1).

**Recall:** $\sum_{j=0}^\infty a\pi^j = \dfrac{a}{1-\pi}$, $|\pi| < 1$ (geometric series).

---

## Formal Derivation via Operator Inversion

$(I - \alpha B)X_t = z_t \Rightarrow X_t = (I - \alpha B)^{-1} z_t$

Rewriting $(I - \alpha B)^{-1} = \delta_0 I + \delta_1 B + \delta_2 B^2 + \cdots$ and using $(I - \alpha B)^{-1}(I - \alpha B) = I$:

$$(\delta_0 I + \delta_1 B + \delta_2 B^2 + \cdots)(I - \alpha B) = I$$

$$\delta_0 I + (\delta_1 - \alpha\delta_0)B + (\delta_2 - \alpha\delta_1)B^2 + \cdots = I$$

Thus $\delta_0 = 1$, $\delta_1 = \alpha$, $\delta_2 = \alpha^2$, ..., in general:

$$\boxed{(I - \alpha B)^{-1} = \sum_{j=0}^\infty \alpha^j B^j}$$

---

## Moments and ACVF of AR(1)

**Mean:**

$$\mathbb{E}[X_t] = \mathbb{E}\!\left[\sum_{j=0}^\infty \alpha^j z_{t-j}\right] = 0$$

**Variance** (also $\gamma(0)$):

$$\mathbb{E}[X_t^2] = \mathbb{E}\!\left[\left(\sum_{j=0}^\infty \alpha^j z_{t-j}\right)^2\right] = \sum_{j=0}^\infty (\alpha^2)^j \mathbb{E}[z_{t-j}^2] = \sigma^2 \sum_{j=0}^\infty (\alpha^2)^j = \frac{\sigma^2}{1 - \alpha^2} < \infty$$

**ACVF** (with $\ell > 0$):

$$\gamma(-\ell) = \operatorname{Cov}(X_t, X_{t-\ell}) = \operatorname{Cov}(\alpha X_{t-1} + z_t,\; X_{t-\ell})$$

$$= \underbrace{\alpha\operatorname{Cov}(X_{t-1}, X_{t-\ell})}_{\text{(1) } = \alpha\gamma(\ell-1)} + \underbrace{\operatorname{Cov}(z_t, X_{t-\ell})}_{\text{(2)} = 0}$$

For (2): $X_{t-\ell} = \sum_{j=0}^\infty \alpha^j z_{t-\ell-j}$ involves only $z_s$ with $s \leq t - \ell < t$, so $z_t$ is uncorrelated with $X_{t-\ell}$ for $\ell > 0$.

$$\Rightarrow \gamma(\ell) = \alpha\,\gamma(\ell - 1) \qquad \text{(recurrence relation)}$$

**Solving:** $\gamma(1) = \alpha\,\gamma(0) = \dfrac{\sigma^2 \alpha}{1 - \alpha^2}$, $\;\gamma(2) = \alpha\,\gamma(1) = \dfrac{\sigma^2 \alpha^2}{1 - \alpha^2}$, ..., $\gamma(\ell) = \dfrac{\sigma^2 \alpha^\ell}{1 - \alpha^2}$.

For $\ell < 0$: since $\gamma(\ell) = \gamma(-\ell)$, we get $\gamma(\ell) = \dfrac{\sigma^2 \alpha^{-\ell}}{1-\alpha^2}$.

In general:

$$\gamma(\ell) = \frac{\sigma^2 \alpha^{|\ell|}}{1 - \alpha^2}$$

**ACF:**

$$\rho(\ell) = \alpha^{|\ell|}$$

> **Key property:** The ACF of AR(1) **decays** geometrically (tails off) with lag $\ell$.
