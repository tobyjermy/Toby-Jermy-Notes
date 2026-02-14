---
layout: default
title: "Lecture 1 — Bayesian Foundations"
---

<a href="{{ '/ma32023/' | relative_url }}" class="back-link">← MA32023 Bayesian Statistics</a>

# Lecture 1 — Bayesian Foundations

## 1. Bayesian Foundations

**Philosophy for reasoning about uncertainty** — how we update that uncertainty given data:

- Begin with **beliefs** about unknown quantities.
- Observe some **data**.
- **Update** our beliefs.

**Bayesian Statistics:** At every step, use probability distributions to represent uncertainty.
→ **All unknown quantities are treated as random variables**, including data and parameters.

---

## Example 2.1 — The Puddle Problem

Leaving the house, you observe a puddle of water. It's a sunny day. We ask: *What caused the puddle?*

**Beliefs (possible causes):** Rain, neighbour watering flowers, leaky pipe, spilled drink, something else.

**Plausibility of each cause (Priors):** Rain is pretty likely; the others are unlikely.

**Plausibility of observing a puddle (Conditionals):** Rain → extremely plausible; the others → low chance.

**Given we see a puddle, what happened?**

---

## Notation and Definitions

**Random Variables:** $X$, with realisations $x$.

**Parameters:** $\theta$, in some parameter space $\Theta$.

**Parametric Model:** $\{f_X(x \mid \theta) : \theta \in \Theta\}$ — the PDF/PMF of our distributions.

**Prior Distribution:** Beliefs about the parameter $\theta$ *before* we see any data, stated as a probability distribution $\pi(\theta)$. This distribution may depend on its own parameters $\pi(\theta \mid \alpha)$ where $\alpha$ is called a **hyperparameter**.

**Likelihood:** Statistical model for the data $f(x \mid \theta)$.

---

## Definition 2.1 — The Posterior Distribution

> Given a prior distribution $\pi(\theta)$ and a likelihood for the observed data, the **posterior distribution** is:
>
> $$\pi(\theta \mid x) = \frac{f(x \mid \theta)\pi(\theta)}{f(x)}$$

**Analogous to Bayes' Theorem:** For events $A, B$:

$$\mathbb{P}(B \mid A) = \frac{\mathbb{P}(A \cap B)}{\mathbb{P}(A)} = \frac{\mathbb{P}(A \mid B)\mathbb{P}(B)}{\mathbb{P}(A)}$$

---

**Important Remarks:**

$$\pi(\theta \mid x) \propto f(x \mid \theta)\pi(\theta)$$

> **"Posterior is proportional to Prior × Likelihood"**
