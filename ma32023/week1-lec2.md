---
layout: default
title: "Lecture 2 — Posteriors, Credible Intervals & HDR"
---

<a href="{{ '/ma32023/' | relative_url }}" class="back-link">← MA32023 Bayesian Statistics</a>

# Lecture 2 — Posteriors, Credible Intervals & HDR

## Example 2.2: The Puddle Problem (Detailed)

|  | Rained | Flowers | Leak | Spillage | Something Else |
|---|---|---|---|---|---|
| **Priors ("Beliefs")** | 0.45 | 0.1 | 0.02 | 0.05 | 0.38 |
| **Likelihood ($P_c$)** | 0.7 | 0.3 | 0.05 | 0.02 | 0.05 |
| **Likelihood × Prior** | 0.315 | 0.03 | 0.001 | 0.001 | 0.019 |
| **Posterior** | 0.861 | 0.082 | 0.003 | 0.003 | 0.052 |

$X \sim \text{Bernoulli}(P_c)$

For the likelihoods, we mean $\mathbb{P}(X = 1 \mid \text{Cause})$ ("Conditional beliefs").

**Posterior:** Normalize to 1 for a valid PDF. (In this case — divide everything by 0.366)

---

## Example 2.3: Fair Coin?

Flip a coin three times and get three heads.

$X \mid \theta \sim \text{Bernoulli}(\theta)$, $\theta$ = probability of tails.

$$f(x_1 = H, x_2 = H, x_3 = H \mid \theta) = (1 - \theta)^3$$

$$\mathbb{E}[X] = \bar{x} \Rightarrow \hat{\theta} = \bar{x} = 0$$

Should be $\approx 0.5$!

---

## Example 2.4: Germinating Seeds

Plant 3 seeds from an old packet. None of them grow.

$X \mid \theta \sim \text{Bernoulli}(\theta)$ where $\theta$ = probability of germination. Assume trials are independent.

$$f(x_1 = 0, x_2 = 0, x_3 = 0 \mid \theta) = (1 - \theta)^3$$

$$\hat{\theta} = \bar{x} = 0$$

**Coins:** Posterior peaks around $\theta = 0.5$ (prior is flatter).

**Seeds:** Posterior peaks near $\theta = 0$ (prior decreases from left, posterior more concentrated near 0).

---

## §2.4: Using the Posterior

**Measures of location:** Posterior mean, mode, median.

**Measures of dispersion:** Variance, IQR.

**Regions that capture most values / bulk of distribution.**

**Tail probabilities:** $\mathbb{P}(\theta < \theta^* \mid x)$

---

## Definition 2.2: Credible Interval (CRI)

> A **credible interval (CRI)** for a parameter $\theta$ is an interval $[L, U]$ such that, given the observed data and the prior, the posterior probability that $\theta$ lies in the interval is at $100(1 - \alpha)\%$:
>
> $$\mathbb{P}(L \leq \theta \leq U \mid x) = 1 - \alpha$$

**Equitailed:** $\mathbb{P}(\theta < L) = \mathbb{P}(\theta > U) = \frac{\alpha}{2}$

**Shortest interval.**

---

## Definition 2.3: Highest Density Region (HDR)

> The **highest density region (HDR)** is a region $C$ that contains $100(1 - \alpha)\%$ of the posterior distribution and has the property that:
>
> $$\forall \theta_1 \in C, \, \theta_2 \notin C \text{ then } \pi(\theta_1 \mid x) > \pi(\theta_2 \mid x)$$

The HDR captures the regions of highest posterior density, which may be disjoint for multimodal distributions.
