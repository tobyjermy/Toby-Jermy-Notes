---
layout: default
title: "Lecture 1 — σ-Algebras and Measurable Spaces"
---

<a href="{{ '/ma32061/' | relative_url }}" class="back-link">← MA32061 Measure Theory & Integration</a>

# Lecture 1 — σ-Algebras and Measurable Spaces

## σ-Algebras

> **Definition.** Let $\Omega$ be a non-empty set. A collection $\mathcal{F} \subseteq \mathcal{P}(\Omega)$ is a **σ-algebra** if:
> 1. $\Omega \in \mathcal{F}$,
> 2. $A \in \mathcal{F} \implies A^c \in \mathcal{F}$,
> 3. $A_1, A_2, \ldots \in \mathcal{F} \implies \bigcup_{n=1}^{\infty} A_n \in \mathcal{F}$.

The pair $(\Omega, \mathcal{F})$ is called a **measurable space**.

### The Borel σ-Algebra

The **Borel σ-algebra** $\mathcal{B}(\mathbb{R})$ is the smallest σ-algebra on $\mathbb{R}$ containing all open sets. Equivalently:

$$
\mathcal{B}(\mathbb{R}) = \sigma\bigl(\{(a, b) : a < b, \; a, b \in \mathbb{R}\}\bigr)
$$

## Measures

> **Definition.** A function $\mu : \mathcal{F} \to [0, \infty]$ is a **measure** on $(\Omega, \mathcal{F})$ if:
> 1. $\mu(\emptyset) = 0$,
> 2. For any countable collection of pairwise disjoint sets $\{A_n\} \subseteq \mathcal{F}$:
>
> $$\mu\left(\bigsqcup_{n=1}^{\infty} A_n\right) = \sum_{n=1}^{\infty} \mu(A_n).$$

The triple $(\Omega, \mathcal{F}, \mu)$ is a **measure space**. If $\mu(\Omega) = 1$, it is a **probability space**.

### Lebesgue Measure

The **Lebesgue measure** $\lambda$ on $(\mathbb{R}, \mathcal{B}(\mathbb{R}))$ is the unique measure satisfying:

$$
\lambda\bigl((a, b]\bigr) = b - a \quad \text{for all } a < b.
$$

## Monotone Convergence (Preview)

> **Theorem (Monotone Convergence).** Let $(\Omega, \mathcal{F}, \mu)$ be a measure space and let $0 \leq f_1 \leq f_2 \leq \cdots$ be measurable functions with $f_n \uparrow f$ pointwise. Then:
>
> $$\lim_{n \to \infty} \int f_n \, d\mu = \int f \, d\mu.$$

---

*These are example notes — replace with your own lecture content.*
