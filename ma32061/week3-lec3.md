---
layout: default
title: "Lecture 3 — Properties of Measures, Null Sets & Completion"
---

<a href="{{ '/ma32061/' | relative_url }}" class="back-link">← MA32061 Measure Theory & Integration</a>

# Lecture 3 — Properties of Measures, Null Sets & Completion

---

## §5 (continued): Properties of Measures

> **Theorem 5.3.** Let $(X, \mathcal{A}, \mu)$ be a measure space.
>
> **(i) Monotonicity:** If $A, B \in \mathcal{A}$ and $A \subseteq B$, then $\mu(A) \leq \mu(B)$.
>
> **(ii) Sub-additivity:** If $\{A_j\}_{j=1}^\infty \subseteq \mathcal{A}$, then
> $$\mu\!\left(\bigcup_{j=1}^\infty A_j\right) \leq \sum_{j=1}^\infty \mu(A_j).$$
>
> **(iii) Continuity from below:** Let $\{A_j\}_{j=1}^\infty \subseteq \mathcal{A}$ with $A_1 \subseteq A_2 \subseteq \cdots$. Then
> $$\mu\!\left(\bigcup_{j=1}^\infty A_j\right) = \lim_{j \to \infty} \mu(A_j).$$
>
> **(iv) Continuity from above:** Let $\{A_j\}_{j=1}^\infty \subseteq \mathcal{A}$ with $A_1 \supseteq A_2 \supseteq \cdots$ and $\exists N \in \mathbb{N}$ s.t. $\mu(A_N) < \infty$. Then
> $$\mu\!\left(\bigcap_{j=1}^\infty A_j\right) = \lim_{j \to \infty} \mu(A_j).$$

**Proof.**

**(i)** Note $B = A \cup (B \setminus A)$ and $A \cap (B \setminus A) = \emptyset$. So

$$\mu(B) = \mu(A \cup (B \setminus A)) = \mu(A) + \mu(B \setminus A) \geq \mu(A). \quad \square$$

**(ii)** Let $B_1 = A_1$ and $B_n = A_n \setminus \bigl(\bigcup_{j=1}^{n-1} A_j\bigr)$ for $n \geq 2$.

Then $\bigcup_{j=1}^\infty A_j = \bigcup_{j=1}^\infty B_j$ and $\{B_j\}$ are pairwise disjoint. So

$$\mu\!\left(\bigcup_{j=1}^\infty A_j\right) = \mu\!\left(\bigcup_{j=1}^\infty B_j\right) = \sum_{j=1}^\infty \mu(B_j) \leq \sum_{j=1}^\infty \mu(A_j) \quad \text{by (i).} \quad \square$$

**(iii)** Set $B_1 = A_1$ and $B_n = A_n \setminus A_{n-1}$ for $n \geq 2$. Then

$$\bigcup_{j=1}^\infty A_j = \bigcup_{j=1}^\infty B_j \qquad \text{and} \qquad \bigcup_{j=1}^n A_j = \bigcup_{j=1}^n B_j = A_n.$$

So

$$\mu\!\left(\bigcup_{j=1}^\infty A_j\right) = \mu\!\left(\bigcup_{j=1}^\infty B_j\right) = \sum_{j=1}^\infty \mu(B_j) = \lim_{j \to \infty} \sum_{n=1}^j \mu(B_n) = \lim_{j \to \infty} \mu\!\left(\bigcup_{n=1}^j B_n\right) = \lim_{j \to \infty} \mu(A_j). \quad \square$$

**(iv)** WLOG $\mu(A_1) < \infty$. Let $B_1 = \emptyset$ and $B_n = A_1 \setminus A_n$. Then $\mu(B_n) \leq \mu(A_1) < \infty$ for all $n$, and $B_n \subseteq B_{n+1}$ for all $n$.

By (iii): $\mu\!\left(\bigcup_{n=1}^\infty B_n\right) = \lim_{n \to \infty} \mu(B_n)$.

Now $\mu(A_1) = \mu(A_n) + \mu(B_n)$ for all $n$, and

$$\bigcup_{n=1}^\infty B_n = \bigcup_{n=1}^\infty (A_1 \setminus A_n) = \bigcup_{n=1}^\infty (A_1 \cap A_n^c) = A_1 \setminus \bigcap_{n=1}^\infty A_n.$$

So

$$\mu\!\left(\bigcup_{n=1}^\infty B_n\right) = \mu\!\left(A_1 \setminus \bigcap_{n=1}^\infty A_n\right) = \mu(A_1) - \mu\!\left(\bigcap_{n=1}^\infty A_n\right).$$

But also

$$\lim_{n \to \infty} \mu(B_n) = \lim_{n \to \infty}\bigl(\mu(A_1) - \mu(A_n)\bigr) = \mu(A_1) - \lim_{n \to \infty} \mu(A_n).$$

We are done since $\mu(A_1) < \infty$. $\square$

---

## §5 (continued): Null Sets and Completeness

> **Definition 5.4.** Let $(X, \mathcal{A}, \mu)$ be a measure space. $N \in \mathcal{A}$ is **null** (or **measure zero**) if $\mu(N) = 0$.
>
> A property $P$ holds **almost everywhere (a.e.)** if
> $$\mu\bigl(\{x \mid P \text{ does not hold at } x\}\bigr) = 0.$$

**Example:** $f, g : X \to \mathbb{R}$ are equal a.e. if $\mu(\{x \mid f(x) \neq g(x)\}) = 0$.

---

> **Definition 5.5.** A measure space $(X, \mathcal{A}, \mu)$ is **complete** if for every $B \subseteq X$ such that there exists a null set $A$ with $B \subseteq A$, we have $B \in \mathcal{A}$.

---

> **Theorem 5.6 (Completing a measure).** Let $(X, \mathcal{A}, \mu)$ be a measure space. Define
>
> $$\mathcal{N} = \{N \in \mathcal{A} \mid \mu(N) = 0\},$$
> $$\bar{\mathcal{A}} = \{A \cup B \mid A \in \mathcal{A},\, B \subseteq N,\, N \in \mathcal{N}\}.$$
>
> Then $\bar{\mathcal{A}}$ is a $\sigma$-algebra and there exists a measure $\bar{\mu} : \bar{\mathcal{A}} \to [0, \infty]$ such that $\bar{\mu}(A) = \mu(A)$ for all $A \in \mathcal{A}$.

**Proof Sketch (Non-Examinable).**

Clearly $\emptyset \in \mathcal{N}$, so $\mathcal{A} \subseteq \bar{\mathcal{A}}$.

**Closure under complement:** Take $A \in \mathcal{A}$, $B \subseteq N \in \mathcal{N}$. We need $(A \cup B)^c = \tilde{A} \cup \tilde{B}$ where $\tilde{A} \in \mathcal{A}$ and $\tilde{B} \subseteq \tilde{N} \in \mathcal{N}$.

Take $N' = N \setminus A \in \mathcal{N}$ and $B' = B \cap N'^c \subseteq N'$; then $A \cup B = A \cup B'$.

WLOG assume $A \cap B = \emptyset$ and $A \cap N = \emptyset$. Then $(A \cup B)^c = A^c \cap B^c$. Write

$$(A \cup B)^c = (A^c \cap N^c) \cup \tilde{B},$$

where $A^c \cap N^c \in \mathcal{A}$ and $\tilde{B} \in \bar{\mathcal{A}}$.

**Closure under unions** follows easily from sub-additivity.

**Extension of $\mu$:** For $A \in \mathcal{A}$, $B \subseteq N \in \mathcal{N}$:

$$\mu(A) = \bar{\mu}(A) \leq \bar{\mu}(A \cup B) \leq \bar{\mu}(A \cup N) = \mu(A \cup N) \leq \mu(A) + \mu(N) = \mu(A).$$

Thus $\bar{\mu}(A \cup B) = \mu(A)$.

**Well-definedness:** It remains to show $\bar{\mu}(A_1 \cup B_1) = \bar{\mu}(A_2 \cup B_2)$ whenever $A_1 \cup B_1 = A_2 \cup B_2$. $\square$
