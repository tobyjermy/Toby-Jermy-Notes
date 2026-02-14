---
layout: default
title: "Lecture 1 — Motivation, Vitali Set & Outer Measure"
---

<a href="{{ '/ma32061/' | relative_url }}" class="back-link">← MA32061 Measure Theory & Integration</a>

# Lecture 1 — Motivation, Vitali Set & Outer Measure

## 1. Motivation — Assigning "Size" to Subsets

Given a set $X$, how do we assign a notion of "size" to subsets $A \subseteq X$? Integration is one type of size. Probability of events is another.

**Example: Dirichlet Function.** Define $f: [0,1] \to \mathbb{R}$ by

$$f(x) = \begin{cases} 1 & x \in \mathbb{Q} \\ 0 & x \in [0,1] \setminus \mathbb{Q} \end{cases}$$

This is **not** Riemann integrable. **Intuition:** $\int_0^1 f\,dx$ should equal $\text{length}(\mathbb{Q} \cap [0,1])$.

Since $\mathbb{Q}$ is countable, enumerate $\mathbb{Q} \cap [0,1] = \{q_j\}_{j=1}^{\infty}$. For each $j$, take $I_j = \left(q_j - \frac{\varepsilon}{2^j}, q_j + \frac{\varepsilon}{2^j}\right)$, so $|I_j| = \frac{\varepsilon}{2^{j-1}}$ and $\text{length}(\mathbb{Q} \cap [0,1]) \leq 2\varepsilon$. Since $\varepsilon$ is arbitrary:

$$\text{length}(\mathbb{Q} \cap [0,1]) = 0$$

---

## 2. Desired Properties of a Length Function

We want $\mu: \mathcal{P}(\mathbb{R}) \to [0,\infty)$ such that:

1. **Normalisation:** $\mu((a,b]) = b - a$
2. **Non-negativity:** $\mu(A) \geq 0$
3. **Monotonicity:** $A \subseteq B \Rightarrow \mu(A) \leq \mu(B)$
4. **Countable additivity:** $\mu\left(\bigcup_{j=1}^\infty A_j\right) = \sum_{j=1}^\infty \mu(A_j)$ for pairwise disjoint sets
5. **Translation Invariance:** $\mu(A + a) = \mu(A)$

---

## Theorem 2.1 — Vitali Set

> **Statement.** There exists $E \subseteq (0,1]$ such that, setting $E_q := E + q$ for $q \in \mathbb{Q}$:
>
> $$(0,1] \subseteq \bigcup_{n=1}^\infty E_{q_n} \quad \text{and} \quad E_{q_i} \cap E_{q_j} = \emptyset \text{ if } i \neq j$$

**Proof (Non-examinable).** Define equivalence: $x \sim y$ if $x - y \in \mathbb{Q}$. Construct $E$ by choosing one element from each equivalence class (Axiom of Choice). Disjointness and covering follow from the construction. $\square$

## Corollary 2.2

> There is no $\mu$ satisfying all the conditions listed above.

> **Proof.** $(0,1] \subseteq \bigcup_{j=1}^\infty E_{q_j} \subseteq (-1,2]$. By monotonicity: $1 \leq \mu\left(\bigcup E_{q_j}\right) \leq 3$. By additivity + translation invariance: $\sum_{j=1}^\infty \mu(E) = 0$ or $\infty$. Contradiction. $\square$

---

## 3. The Lebesgue Outer Measure

> **Definition 3.1.** The **outer measure** of $A \subseteq \mathbb{R}$:
>
> $$\mu^*(A) = \inf\left\{\sum_{j=1}^\infty |I_j| \;\Big|\; \{I_j\}_{j=1}^\infty \text{ is an open cover of } A\right\}$$

**Examples:**

- $\mu^*((a,b)) = b - a$
- $\mu^*([a,b]) = b - a$ (proven via compactness argument)
- $\mu^*(\mathbb{Q}) = 0$

> **Any countable $A \subseteq \mathbb{R}$ has $\mu^*(A) = 0$.**

**Example: Middle-Third Cantor Set.** $C = \bigcap_{n=0}^\infty C_n$ where each $C_n$ consists of $2^n$ intervals of length $3^{-n}$:

$$\mu^*(C) \leq \mu^*(C_n) = \left(\frac{2}{3}\right)^n \to 0$$

$C$ is uncountable yet has $\mu^*(C) = 0$.

---

## Proposition 3.3 — Properties of $\mu^*$

1. $0 \leq \mu^*(A) \leq \infty$
2. $A \subseteq B \Rightarrow \mu^*(A) \leq \mu^*(B)$ **(monotonicity)**
3. $\mu^*\left(\bigcup_{j=1}^\infty A_j\right) \leq \sum_{j=1}^\infty \mu^*(A_j)$ **(countable sub-additivity)**
4. For all intervals $I$: $\mu^*(I) = |I|$
5. $\mu^*(A+h) = \mu^*(A)$ **(translation invariance)**

> **Proof of (iii).** For each $A_j$, take cover $\{I_{j,n}\}$ with $\sum_n |I_{j,n}| \leq \mu^*(A_j) + \varepsilon/2^j$. Then $\{I_{j,n}\}_{j,n}$ covers $\bigcup A_j$:
>
> $$\mu^*\left(\bigcup A_j\right) \leq \sum_j \sum_n |I_{j,n}| \leq \sum_j \mu^*(A_j) + \varepsilon \quad \square$$
