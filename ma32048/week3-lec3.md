---
layout: default
title: "Lecture 3 — Branching Processes & Cliques"
---

<a href="{{ '/ma32048/' | relative_url }}" class="back-link">← MA32048 Discrete Probability</a>

# Lecture 3 — Branching Processes & Cliques

---

## Branching Processes

Let $\mathbb{N} = \{1, 2, 3, \ldots\}$ and $\mathbb{N}_0 = \{0, 1, 2, 3, \ldots\}$.

- $[0,1]^{\mathbb{N}}$ is the space of sequences $\mathbf{p} = (p_n)_{n \geq 1}$, $p_n \in [0,1]$.
- $[0,1]^{\mathbb{N}_0}$ is the space of sequences $\mathbf{p} = (p_n)_{n \geq 0}$, $p_n \in [0,1]$.

> **Definition 1.16.** Given $q \in [0,1]^{\mathbb{N}_0}$ with $\sum_{i=0}^\infty q_i = 1$, a **branching process** with offspring distribution $q$ is a sequence of RVs where
>
> $$Z_0 = 1 \qquad \text{and} \qquad Z_n = \sum_{i=1}^{Z_{n-1}} X_i^{(n)},$$
>
> where $(X_i^{(n)})_{i \geq 1,\, n \geq 1}$ are iid RVs with distribution $q$, i.e.
>
> $$\mathbb{P}\!\left[X_i^{(n)} = k\right] = q_k, \quad k \geq 0.$$

**Remarks:**
- If $Z_{n-1} = 0$ then $Z_n = 0$.
- The R.V. $T = \sum_{n=0}^\infty Z_n$ is the **total size** of the branching process.
- The process **survives** if $T = \infty$ and **dies out** if $T < \infty$.
- Set $\mu(q) = \mathbb{E}\!\left[X_i^{(1)}\right] = \sum_{k=0}^\infty k\, q_k$ and

$$g_q(s) = \sum_{k=0}^\infty q_k\, s^k, \quad 0 \leq s \leq 1.$$

---

> **Lemma 1.17.** Assume $q_1 < 1$. Then $x := \mathbb{P}[T < \infty]$ is the smallest non-negative solution to $x = g_q(x)$.
>
> - If $\mu(q) \leq 1$ then $\mathbb{P}[T < \infty] = 1$.
> - If $\mu(q) > 1$ then $\mathbb{P}[T < \infty] < 1$.

**Proof (Sketch):**

$$x = \mathbb{P}[T < \infty] = \sum_{k=0}^\infty \mathbb{P}[T < \infty \mid Z_1 = k]\,\mathbb{P}[Z_1 = k] = \sum_{k=0}^\infty x^k q_k = g_q(x). \quad \square$$

---

> **Lemma 1.18.** For $x \in \mathbb{R}$:
>
> $$e^x \geq 1 + x \quad \Longleftrightarrow \quad 1 - x \leq e^{-x}, \qquad \text{and} \qquad \log(1+x) = x\bigl(1 + o(1)\bigr) \text{ as } x \to 0.$$
>
> **Proof:** Non-examinable.

---

## 2. Cliques and Threshold Functions

**Recall:** $G(n,p)$ is the random graph on $[n] = \{1, \ldots, n\}$ with $\mathbb{P}[\{i,j\} \in E(G(n,p))] = p$ for all $i \neq j$, independently.

**Question:** Is there a sequence $f(n)$ such that if $p_n \ll f(n)$ then $G(n,p_n)$ does not contain a triangle w.h.p., but if $p_n \gg f(n)$ then $G(n,p_n)$ does contain a triangle w.h.p.? (A **triangle** is a copy of $K_3$.)

> **Definition 2.1.** Graphs $G(V,E)$ and $G'(V',E')$ are **isomorphic** if there exists a bijection $\phi: V \to V'$ such that $\{x,y\} \in E$ if and only if $\{\phi(x), \phi(y)\} \in E'$.

> **Definition 2.2.** A **clique** of $G$ is a subgraph isomorphic to $K_k$ for some $k \in \mathbb{N}$. $k$ is called the **order** of the clique. The **clique number** of $G$ is the largest $k \in \mathbb{N}$ such that $G$ has a $k$-clique.
>
> - A 2-clique $\cong$ single edge.
> - A 3-clique $\cong$ triangle.

Let $N_n(k) = \#$ $k$-cliques in $G(n, p_n)$. We are interested in whether $N_n(k) > 0$ w.h.p.

---

> **Theorem 2.3.** If $p_n \ll 1/n^2$ then $G(n, p_n)$ has no edge w.h.p., and if $p_n \gg 1/n^2$ then $G(n, p_n)$ has at least one edge w.h.p.

**Proof:** Let $N_n = N_n(2) = \#$ edges. Then $N_n \sim B\!\left(\binom{n}{2}, p_n\right)$. In particular:

$$\mathbb{E}[N_n] = \binom{n}{2} p_n = \frac{n(n-1)p_n}{2} = \Theta(n^2 p_n).$$

If $p_n \ll 1/n^2$, then $\mathbb{E}[N_n] \to 0$. By Markov's inequality:

$$\mathbb{P}[N_n > 0] = \mathbb{P}[N_n \geq 1] \leq \frac{\mathbb{E}[N_n]}{1} \xrightarrow{n \to \infty} 0.$$

Hence $N_n = 0$ w.h.p. (**first moment method**.)

If $p_n \gg 1/n^2$, then $\mathbb{E}[N_n] \to \infty$ as $n \to \infty$, and

$$\mathbb{P}[N_n = 0] = (1-p_n)^{\binom{n}{2}} \leq \left(e^{-p_n}\right)^{\binom{n}{2}} \xrightarrow{n \to \infty} 0. \quad \square$$
