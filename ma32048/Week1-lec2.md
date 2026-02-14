---
layout: default
title: "Lecture 2 — Trees, Cayley's Formula & Asymptotics"
---

<a href="{{ '/ma32048/' | relative_url }}" class="back-link">← MA32048 Discrete Probability</a>

# Lecture 2 — Trees, Cayley's Formula & Asymptotics

> **Definition 1.7: Cycle.** A **cycle** in a graph $(V, E)$ is a sequence of distinct vertices $(v_1, \ldots, v_m)$ with $m \geq 3$ s.t. $\{v_i, v_{i+1}\} \in E$ for $1 \leq i \leq m-1$ and $\{v_m, v_1\} \in E$.

A **tree** is a connected graph with no cycles. A **component** of a graph $G$ is a maximal connected subgraph.

---

> **Lemma 1.8.** Any connected finite graph $G$ has a spanning subgraph which is a tree ("a spanning tree").
>
> **Proof:** If $G$ is a tree, done. Otherwise delete edges from cycles until no cycles remain. $\square$

> **Lemma 1.9.** A connected graph on $n$ vertices is a tree if and only if it has $n-1$ edges.
>
> **Proof ($\Rightarrow$):** Add edges $e_1, \ldots, e_K$ one by one. Components decrease: $n, n-1, \ldots, 1$. Thus $K = n-1$. $\square$

---

## Theorem 1.1 (Cayley's Formula)

> For $n \in \mathbb{N}$, let $\mathcal{T}_n$ denote the number of trees on vertex set $\{1, \ldots, n\}$. Then $\mathcal{T}_n = n^{n-2}$.

**Proof:** Count $A_n$ = number of ways to add directed edges to obtain a rooted tree, in two ways.

**1st way:** Choose tree, then root, then order: $A_n = \mathcal{T}_n \times n \times (n-1)!$

**2nd way:** Add directed edges one by one. Ways to pick $k$-th edge = $n(n-k)$.

$$A_n = n(n-1) \cdot n(n-2) \cdots n \cdot 1 = n^{n-1}(n-1)!$$

$$\Rightarrow \mathcal{T}_n = n^{n-2} \quad \square$$

---

> **Definition 1.12: With High Probability (w.h.p).** $(A_n)_{n \geq 1}$ occurs **w.h.p** if $\lim_{n \to \infty} \mathbb{P}(A_n) = 1$.

## Recall

**Union bound:** $\mathbb{P}\left[\bigcup_{i=1}^n A_i\right] \leq \sum_{i=1}^n \mathbb{P}(A_i)$

**Markov's Inequality:** If $X \geq 0$, then $\mathbb{P}(X \geq \varepsilon) \leq \frac{\mathbb{E}[X]}{\varepsilon}$

---

## Asymptotic Notation

- **Little-o:** $a_n = o(b_n)$ if $\frac{a_n}{b_n} \to 0$
- **Big-O:** $a_n = O(b_n)$ if $\limsup \frac{a_n}{b_n} < \infty$
- **Asymptotic to:** $a_n \sim b_n$ if $\frac{a_n}{b_n} \to 1$
- **Asymptotically equal:** $a_n = \Theta(b_n)$ if $a_n = O(b_n)$ and $b_n = O(a_n)$

**Warning:** $n^{n-2} = \frac{n^n}{n^2} \not\sim n^n$

---

> **Definition 1.13: Convergence in Probability.** $X_n \xrightarrow{\mathbb{P}} x$ if $\forall \varepsilon > 0$: $\lim_{n \to \infty} \mathbb{P}[|X_n - x| > \varepsilon] = 0$.

> **Lemma 1.14.** If $\mathbb{E}[X_n] = x$ $\forall n$ and $\text{Var}(X_n) \to 0$, then $X_n \xrightarrow{\mathbb{P}} x$.
>
> **Proof:** $\mathbb{P}[|X_n - x| > \varepsilon] \leq \frac{\text{Var}(X_n)}{\varepsilon^2} \to 0$ by Markov's inequality. $\square$

> **Lemma 1.15.** If $\mathbb{E}[X_n] \to x$ and $\text{Var}(X_n) \to 0$, then $X_n \xrightarrow{\mathbb{P}} x$. (Proof non-examinable.)
