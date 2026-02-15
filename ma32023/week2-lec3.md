---
layout: default
title: "Lecture 3 — Posterior Predictive Distribution & Sequential Updating"
---

<a href="{{ '/ma32023/' | relative_url }}" class="back-link">← MA32023 Bayesian Statistics</a>

# Lecture 3 — Posterior Predictive Distribution & Sequential Updating

## Definition 2.4: Posterior Predictive Distribution

> The **posterior predictive distribution** is the distribution of new data $z$ given observed data $X = x$:
>
> $$f(z \mid x) = \int_{\Theta} f(z \mid \theta, x) \, \pi(\theta \mid x) \, d\theta$$

If we judge $z$ and $X$ are **conditionally independent** given $\theta$, this simplifies to:

$$f(z \mid x) = \int_{\Theta} f(z \mid \theta) \, \pi(\theta \mid x) \, d\theta$$

In Stat 3A/ML: $f(z \mid x, \hat{\theta})$.

---

## Sequential Updating

Once we observe $z$, the posterior for $\theta$ is:

$$\pi(\theta \mid x, z) \propto f(x, z \mid \theta) \, \pi(\theta)$$

Expanding the joint likelihood:

$$f(x, z \mid \theta) \pi(\theta) = f(x, z, \theta) = f(z \mid x, \theta) f(x, \theta)$$

$$= f(z \mid x, \theta) \, \pi(\theta \mid x) \, f(x)$$

$$\propto f(z \mid x, \theta) \, \pi(\theta \mid x)$$

Therefore:

$$\pi(\theta \mid x, z) \propto f(z \mid x, \theta) \, \pi(\theta \mid x)$$

If $z$ and $X$ are conditionally independent given $\theta$:

$$\pi(\theta \mid x, z) \propto f(z \mid \theta) \, \pi(\theta \mid x)$$

> **"Yesterday's posterior is today's prior."**
