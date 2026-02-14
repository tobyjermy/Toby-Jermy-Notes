---
layout: default
title: "Lecture 2 — σ-Algebras, Borel Sets & Measures"
---

<a href="{{ '/ma32061/' | relative_url }}" class="back-link">← MA32061 Measure Theory & Integration</a>

# Lecture 2 — σ-Algebras, Borel Sets & Measures

## §4: σ-Algebras

> **Definition 4.1: Algebra.** A collection $\mathcal{A} \subseteq \mathcal{P}(X)$ is an **algebra** if:
> 1. $\emptyset \in \mathcal{A}$
> 2. $A \in \mathcal{A} \Rightarrow A^c \in \mathcal{A}$
> 3. $\{A_j\}_{j=1}^n \subseteq \mathcal{A} \Rightarrow \bigcup_{j=1}^n A_j \in \mathcal{A}$

> **Definition 4.2: σ-Algebra.** $\mathcal{A}$ is a **σ-algebra** if also whenever $\{A_j\}_{j=1}^\infty \subseteq \mathcal{A}$, then $\bigcup_{j=1}^\infty A_j \in \mathcal{A}$.

**Examples:**

1. **Trivial σ-algebra:** $\{\emptyset, X\}$
2. $\mathcal{P}(X)$ is a σ-algebra.
3. If $X$ is uncountable: $\{E \subseteq X \mid E \text{ or } E^c \text{ is at most countable}\}$ is a σ-algebra.
4. If $X$ is countable: $\{E \subseteq X \mid E \text{ or } E^c \text{ is finite}\}$ is an algebra but **not** a σ-algebra.

---

> **Lemma 4.2.** Let $\mathcal{A}$ be a σ-algebra. Then:
> 1. $\mathcal{A}$ is an algebra.
> 2. $\{A_j\}_{j=1}^\infty \subseteq \mathcal{A} \Rightarrow \bigcap_{j=1}^\infty A_j \in \mathcal{A}$
>
> **Proof of (ii):** By De Morgan: $\bigcap_{j=1}^\infty A_j = \left(\bigcup_{j=1}^\infty A_j^c\right)^c \in \mathcal{A}$. $\square$

---

> **Lemma 4.5.** If $\{\mathcal{A}_j\}_{j \in J}$ is a (possibly uncountable) collection of σ-algebras, then $\bigcap_{j \in J} \mathcal{A}_j$ is a σ-algebra.
>
> **Proof:** (i) $\emptyset \in \mathcal{A}_j$ $\forall j$. (ii) $A \in \mathcal{L} \Rightarrow A^c \in \mathcal{A}_j$ $\forall j$. (iii) $\{A_n\} \subseteq \mathcal{L} \Rightarrow \bigcup A_n \in \mathcal{A}_j$ $\forall j$. $\square$

> **Definition 4.6: Generated σ-Algebra.** $\sigma(\mathcal{G})$ is the **smallest σ-algebra containing** $\mathcal{G}$.

**Example:** $\sigma(\{B\}) = \{\emptyset, B, B^c, X\}$

---

> **Definition 4.8: Borel σ-Algebra.** Let $(M, d)$ be a metric space. The **Borel σ-algebra** $\mathcal{B}_M = \sigma(\{U \subseteq M \mid U \text{ is open}\})$.

> **Lemma 4.9:**
> 1. $\mathcal{B}_M = \sigma(\{C \subseteq M \mid C \text{ is closed}\})$
> 2. For $X = \mathbb{R}$: $\sigma(\{(a, b] \mid -\infty < a < b < \infty\}) = \mathcal{B}_{\mathbb{R}}$

---

## §5. Measures

> **Definition 5.1: Measure.** A function $\mu : \mathcal{A} \to [0, \infty]$ is a **measure** if:
> 1. $\mu(\emptyset) = 0$
> 2. For pairwise disjoint $\{A_n\}$: $\mu\left(\bigcup_{n=1}^\infty A_n\right) = \sum_{n=1}^\infty \mu(A_n)$

> **Definition 5.2.** A **measurable space** is $(X, \mathcal{A})$. A **measure space** is $(X, \mathcal{A}, \mu)$. If $\mu(X) = 1$, it is a **probability space**.

---

### Examples of Measures

**1. Counting Measure:**

$$\mu(A) = \begin{cases} \#A & \text{if } A \text{ is finite} \\ \infty & \text{otherwise} \end{cases}$$

**2. Dirac Measure** at $x$:

$$\delta_x(A) = \begin{cases} 1 & x \in A \\ 0 & x \notin A \end{cases}$$

**3. General Weighted Measure:** For $f : X \to [0, \infty]$:

$$\mu_f(A) = \sum_{x \in A} f(x)$$

If $f \equiv 1$: counting measure. If $f(x) = 1$, $f(y) = 0$ $\forall y \neq x$: $\mu_f = \delta_x$.

**Non-Example:** $\mu(A) = 0$ if $A$ finite, $\infty$ if $A$ infinite — this is **not** a measure.
