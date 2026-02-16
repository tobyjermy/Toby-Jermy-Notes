---
layout: default
title: "Problem Class 1 — Paths, Cycles, Factorial Bounds & Spanning Trees"
---

<a href="{{ '/ma32048/' | relative_url }}" class="back-link">← MA32048 Discrete Probability</a>

# Problem Class 1 — Paths, Cycles, Factorial Bounds & Spanning Trees

---

## Question 3: Paths in $G(n,p)$

Given $k \geq 2$, a **path** of length $k$ is a graph $P_k = (V, E)$ with $V = \{x_0, \ldots, x_k\}$ and $E = \{\{x_0, x_1\}, \{x_1, x_2\}, \ldots, \{x_{k-1}, x_k\}\}$.

Given $n > k$, find $\mathbb{P}(G(n,p)$ contains a single path of length $k$, but no other edges besides those in the path$)$.

Each such path has probability $p^k (1-p)^{\binom{n}{2} - k}$.

The number of such labelled paths on $n$ vertices is:

$$\frac{1}{2} n(n-1) \cdots (n-k) = \frac{1}{2}(n)_{k+1}$$

where $(n)_y := n(n-1)\cdots(n-y+1)$ is the falling factorial, with $(n)_0 = 1$.

Therefore:

$$\mathbb{P}(\ldots) = \frac{1}{2}(n)_{k+1} \cdot p^k (1-p)^{\binom{n}{2} - k}$$

---

## Question 4: Cycles in $G(n,p)$

Given $n, k \geq 3$, find $\mathbb{P}(G(n,p)$ contains a cycle of length $k$ and no other edges$)$.

The number of directed cycles of length $k$ with a fixed starting vertex is $n(n-1)\cdots(n-k+1)$. To get undirected cycles, divide by $2k$ (each cycle is traversed in 2 directions, and has $k$ choices of starting vertex):

$$\text{\\# cycles of length } k = \frac{n(n-1)\cdots(n-k+1)}{2k} = \frac{(n)_k}{2k}$$

Each cycle has probability $p^k(1-p)^{\binom{n}{2}-k}$.

Hence:

$$\mathbb{P}(\ldots) = \frac{(n)_k}{2k} \cdot p^k (1-p)^{\binom{n}{2} - k}$$

---

## Question 5: Useful Inequalities

### Part (a): Prove $k! \geq \dfrac{k^k}{e^k}$ for all $k \in \mathbb{N}$

We need $e^k \geq \dfrac{k^k}{k!}$. Using the Taylor series:

$$e^k = \sum_{n=0}^{\infty} \frac{k^n}{n!} \geq \frac{k^k}{k!}$$

since all terms are positive and $n = k$ is one of them. $\square$

**Remark (Stirling's formula):** $k! \sim \left(\frac{k}{e}\right)^k \sqrt{2\pi k}$ as $k \to \infty$.

**Probabilistic interpretation:** A $\text{Poisson}(k)$ RV has PMF $e^{-k}\frac{k^n}{n!}$, $n = 0, 1, 2, \ldots$ If $X \sim \text{Poisson}(k)$, write $X = Y_1 + \cdots + Y_k$ where $Y_1, \ldots, Y_k$ are iid $\text{Pois}(1)$ RVs. Then:

$$e^{-k}\frac{k^k}{k!} = \mathbb{P}(X = k) = \mathbb{P}\!\left(k - \tfrac{1}{2} \leq X \leq k + \tfrac{1}{2}\right) = \mathbb{P}\!\left(-\frac{1}{2\sqrt{k}} \leq \frac{X - k}{\sqrt{k}} \leq \frac{1}{2\sqrt{k}}\right)$$

By CLT this is approximately $\mathbb{P}\!\left(-\frac{1}{\sqrt{2k}} \leq Z \leq \frac{1}{\sqrt{2k}}\right) \approx \frac{1}{\sqrt{2\pi}} \cdot \frac{1}{\sqrt{k}}$.

### Part (b): $(1-x)^n \geq 1 - nx$ for $0 \leq x \leq 1$ and $n \in \mathbb{N}$

If $A_1, \ldots, A_n$ are independent events with $\mathbb{P}(A_i) = x$, $i = 1, \ldots, n$, then:

$$\text{LHS} = \mathbb{P}\!\left(\bigcap_{i=1}^n A_i^c\right) = \mathbb{P}\!\left(\left(\bigcup_{i=1}^n A_i\right)^c\right) = 1 - \mathbb{P}\!\left(\bigcup_{i=1}^n A_i\right) \geq 1 - \sum_{i=1}^n \mathbb{P}(A_i) = 1 - nx \quad \square$$

### Part (c): $\dbinom{n}{k} \leq \dfrac{n^k}{k!}$ for $1 \leq k \leq n$

$$\text{LHS} = \frac{n!}{k!(n-k)!} = \frac{n(n-1)\cdots(n-k+1)}{k!} \leq \frac{n^k}{k!} \quad \square$$

**Asymptotic:** If $k$ is fixed and $n \to \infty$:

$$\binom{n}{k} \frac{k!}{n^k} = \frac{n(n-1)\cdots(n-k+1)}{n \cdot n \cdots n} = \frac{n-1}{n} \cdot \frac{n-2}{n} \cdots \frac{n-k+1}{n} \to 1$$

so $\dbinom{n}{k} \sim \dfrac{n^k}{k!}$ as $n \to \infty$.

---

## Question 6: Spanning Trees of $K_n$

Let $T_n$ be a spanning tree of $K_n$ chosen uniformly at random.

**Find** $\mathbb{P}(\text{vertex 1 has exactly one neighbour in } T_n)$.

By Cayley's formula, there are $n^{n-2}$ spanning trees of $K_n$. Trees where vertex 1 is a leaf: choose which vertex it connects to ($(n-1)$ choices), then choose a spanning tree on the remaining $n-1$ vertices ($(n-1)^{n-1-2} = (n-1)^{n-3}$ trees).

$$\mathbb{P}(\text{vertex 1 is a leaf}) = \frac{(n-1)^{n-3} \cdot (n-1)}{n^{n-2}} = \frac{(n-1)^{n-2}}{n^{n-2}} = \left(1 - \frac{1}{n}\right)^{n-2}$$

$$= \left(1 - \frac{1}{n}\right)^n \left(1 - \frac{1}{n}\right)^{-2} \to e^{-1} \cdot 1 = e^{-1}$$

**Expected number of neighbours of vertex 1:**

$$\mathbb{E}[\text{\\# neighbours of 1}] = \frac{1}{n}\,\mathbb{E}\!\left[\sum_{k=1}^n \text{\\# neighbours of } k\right] = \cdots$$

(by symmetry, each vertex has the same expected degree, and the total degree of a tree on $n$ vertices is $2(n-1)$, giving expected degree $\frac{2(n-1)}{n}$).
