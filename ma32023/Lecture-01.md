---
layout: default
title: "Lecture 1 — Introduction to Bayesian Inference"
---

<a href="{{ '/ma32023/' | relative_url }}" class="back-link">← MA32023 Bayesian Statistics</a>

# Lecture 1 — Introduction to Bayesian Inference

## Bayes' Theorem

The foundation of Bayesian statistics is Bayes' theorem. For a parameter $\theta$ and observed data $\mathbf{x}$:

$$
p(\theta \mid \mathbf{x}) = \frac{p(\mathbf{x} \mid \theta) \, p(\theta)}{p(\mathbf{x})}
$$

where:

- $p(\theta)$ is the **prior** distribution,
- $p(\mathbf{x} \mid \theta)$ is the **likelihood**,
- $p(\theta \mid \mathbf{x})$ is the **posterior** distribution,
- $p(\mathbf{x}) = \int p(\mathbf{x} \mid \theta) \, p(\theta) \, d\theta$ is the **marginal likelihood** (evidence).

## Conjugate Priors

> **Definition.** A prior $p(\theta)$ is said to be *conjugate* for a likelihood $p(\mathbf{x} \mid \theta)$ if the posterior $p(\theta \mid \mathbf{x})$ belongs to the same family as the prior.

### Example: Beta–Binomial Model

Suppose $X \mid \theta \sim \text{Bin}(n, \theta)$ and $\theta \sim \text{Beta}(\alpha, \beta)$. Then:

$$
p(\theta \mid x) \propto \theta^{x + \alpha - 1}(1 - \theta)^{n - x + \beta - 1}
$$

so the posterior is $\theta \mid x \sim \text{Beta}(\alpha + x, \; \beta + n - x)$.

## Posterior Summaries

The **posterior mean** under the Beta–Binomial model is:

$$
\mathbb{E}[\theta \mid x] = \frac{\alpha + x}{\alpha + \beta + n}
$$

This can be written as a weighted average of the prior mean and the MLE:

$$
\mathbb{E}[\theta \mid x] = w \cdot \frac{\alpha}{\alpha + \beta} + (1 - w) \cdot \frac{x}{n}, \qquad w = \frac{\alpha + \beta}{\alpha + \beta + n}.
$$

## Code: Plotting the Posterior

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.stats import beta

# Prior parameters
alpha_prior, beta_prior = 2, 5

# Observed data
n, x = 20, 12

# Posterior parameters
alpha_post = alpha_prior + x
beta_post = beta_prior + n - x

theta = np.linspace(0, 1, 500)

fig, ax = plt.subplots(figsize=(8, 4))
ax.plot(theta, beta.pdf(theta, alpha_prior, beta_prior), '--', label='Prior')
ax.plot(theta, beta.pdf(theta, alpha_post, beta_post), label='Posterior')
ax.axvline(x / n, color='gray', linestyle=':', label=f'MLE = {x/n:.2f}')
ax.set_xlabel(r'$\theta$')
ax.set_ylabel('Density')
ax.legend()
ax.set_title('Beta–Binomial Conjugate Update')
plt.tight_layout()
plt.show()
```

---

*These are example notes — replace with your own lecture content.*
