---
layout: default
title: "Lecture 1 — Random Graphs"
---

<a href="{{ '/ma32048/' | relative_url }}" class="back-link">← MA32048 Discrete Probability</a>

# Lecture 1 — Random Graphs

**Logistics:** Hand in problem sheets fortnightly, end of Thursday in weeks 2, 4, 6, 8, 10. Odd weeks: both sessions are lectures. Even weeks: Tuesday lecture + Friday problem class.

---

**I: Random Graphs** — Concerned with connectivity between objects in networks. We consider large, but finite graphs. In random graphs, edges between vertices are random. The key model is the Erdős–Rényi random graph.

**II: Percolation** — Typically an infinite graph where each vertex has finitely many neighbours. Key question: is there a phase transition?

---

> **Definition 1.1.** A **graph** is a pair $(V, E)$ where $V$ is a set (vertices) and $E \subseteq \{\{i, j\} : i, j \in V, i \neq j\}$ (edges).

> **Definition 1.2.** The **complete graph** on $n$ vertices, $K_n$, is the graph with vertex set $\{1, \ldots, n\}$ and an edge between every pair. Total edges: $\binom{n}{2} = \frac{n(n-1)}{2}$.

> **Definition 1.3.** $G'$ is a **subgraph** of $G$ if $V' \subseteq V$ and $E' \subseteq E$. When $V' = V$, it is a **spanning subgraph**.

> **Definition 1.4.** The **random graph** $G(n,p)$ is a random spanning subgraph of $K_n$, defined by keeping each edge with probability $p$, independently:
>
> $$\mathbb{P}(E(G(n,p)) = S) = p^{|S|}(1-p)^{\binom{n}{2} - |S|}$$

> **Definition 1.5.** $G = (V, E)$ is **connected** if for any $u, v \in V$, there is a path from $u$ to $v$.

---

## Example 1.6: $\mathbb{P}[G(4,p) \text{ is connected}]$

- 3 edges: $\binom{6}{3} - 4 = 16$ connected graphs, each with probability $p^3(1-p)^3$.
- 4 edges: all $\binom{6}{4} = 15$ connected, probability $p^4(1-p)^2$.
- 5 edges: $\binom{6}{5} = 6$, probability $p^5(1-p)$.
- 6 edges: $K_4$ itself, probability $p^6$.

$$\mathbb{P}[G(4,p) \text{ is connected}] = p^6 + 6p^5(1-p) + 15p^4(1-p)^2 + 16p^3(1-p)^3$$
