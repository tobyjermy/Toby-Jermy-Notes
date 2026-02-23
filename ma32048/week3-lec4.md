---
layout: default
title: "Lecture 4 — Threshold Functions & Moment Methods"
---

<a href="{{ '/ma32048/' | relative_url }}" class="back-link">← MA32048 Discrete Probability</a>

# Lecture 4 — Threshold Functions & Moment Methods

---

## Behavior at $p_n = 1/n^2$

At the threshold $p_n = 1/n^2$, the expected edge count satisfies:

$$\mathbb{E}[N_n] = \frac{n(n-1)}{2} \cdot \frac{1}{n^2} \xrightarrow{n \to \infty} \frac{1}{2}.$$

In fact $N_n$ converges in distribution to $\mathrm{Poisson}(1/2)$: for all $k \in \mathbb{N}_0$,

$$\mathbb{P}[N_n = k] \xrightarrow{n \to \infty} e^{-1/2}\, \frac{(1/2)^k}{k!}.$$

**Triangles.** Let $N_n(3) = \#$ triangles in $G(n, p_n)$. Then:

$$\mathbb{E}[N_n(3)] = \binom{n}{3} p_n^3 = \frac{n(n-1)(n-2)}{6}\, p_n^3 \longrightarrow 0 \text{ if } p_n \ll \tfrac{1}{n}, \quad \longrightarrow \infty \text{ if } p_n \gg \tfrac{1}{n}.$$

---

> **Definition 2.4.** A collection $\mathcal{P}$ of graphs is called **monotone increasing** if for all $G, G'$ with $G$ a spanning subgraph of $G'$: if $G \in \mathcal{P}$ then $G' \in \mathcal{P}$.
>
> ($\mathcal{P}$ stands for "Property", as it is usually defined as all graphs having a certain property.)

**Examples:**
- The class of graphs containing a $k$-clique is monotone increasing.
- The class of connected graphs is monotone increasing.

---

> **Theorem 2.5.** Suppose $\mathcal{P}$ is a monotone increasing class of graphs. Then:
>
> **(a)** For all $n \in \mathbb{N}$ and $0 \leq p \leq q \leq 1$:
>
> $$\mathbb{P}(G(n,p) \in \mathcal{P}) \leq \mathbb{P}(G(n,q) \in \mathcal{P}) \leq \mathbb{P}(G(n,p) \in \mathcal{P}) + \binom{n}{2}(q-p).$$
>
> **(b)** The map $p \mapsto \mathbb{P}(G(n,p) \in \mathcal{P})$ is continuous on $[0,1]$.

**Proof.** *Idea:* Construct $G(n,p)$ and $G(n,q)$ on the same probability space so that $G(n,p)$ is a spanning subgraph of $G(n,q)$.

Sample $U_e$, $e \in E_n = E(K_n)$, independently as Unif$[0,1]$ RVs. Let

$$E_1 = \{e \in E_n : U_e \leq q\}, \qquad E_2 = \{e \in E_n : U_e \leq p\}.$$

Since $\mathbb{P}(U_e \leq q) = q$, we have $G_1 := ([n], E_1) \sim G(n,q)$ and $G_2 := ([n], E_2) \sim G(n,p)$.

Since $p \leq q$ we have $E_2 \subseteq E_1$, so $G_2$ is a spanning subgraph of $G_1$.

**Thus:** $\mathbb{P}(G(n,p) \in \mathcal{P}) = \mathbb{P}(G_2 \in \mathcal{P}) \leq \mathbb{P}(G_1 \in \mathcal{P}) = \mathbb{P}(G(n,q) \in \mathcal{P})$.

For the upper bound on the gap:

$$\mathbb{P}(G(n,q) \in \mathcal{P}) - \mathbb{P}(G(n,p) \in \mathcal{P}) = \mathbb{P}(G_1 \in \mathcal{P}) - \mathbb{P}(G_2 \in \mathcal{P})$$

$$= \mathbb{P}\!\left(\{G_1 \in \mathcal{P}\} \setminus \{G_2 \in \mathcal{P}\}\right) \leq \mathbb{P}(G_1 \neq G_2)$$

$$= \mathbb{P}\!\left(\bigcup_{e \in E_n} \{e \in E_1 \setminus E_2\}\right) \leq \sum_{e \in E_n} \mathbb{P}(U_e \in (p, q]) = \binom{n}{2}(q-p).$$

Part (b) follows from (a). $\square$

---

> **Definition 2.6.** Suppose $\mathcal{P}$ is a monotone increasing class of graphs. A function $f: \mathbb{N} \to (0,1)$ is a **threshold function** for $G(n,p)$ to lie in $\mathcal{P}$ if:
>
> - When $(p_n)_{n \in \mathbb{N}}$ with $p_n \ll f(n)$: $\quad\mathbb{P}(G(n,p_n) \in \mathcal{P}) \xrightarrow{n \to \infty} 0$.
> - When $(p_n)_{n \in \mathbb{N}}$ with $p_n \gg f(n)$: $\quad\mathbb{P}(G(n,p_n) \in \mathcal{P}) \xrightarrow{n \to \infty} 1$.

**Remark:** Threshold functions are not unique. If $g(n) = \Theta(f(n))$, then $g$ is also a threshold function.

---

**Recall:** $N_n(k) = \#$ $k$-cliques in $G(n, p_n)$.

> **Proposition 2.7.** Let $(N_n)_{n \geq 1}$ be non-negative RVs with $\mathbb{E}[N_n] > 0$.
>
> **(i) First moment method:** Suppose $N_n$ is integer-valued and $\mathbb{E}[N_n] \to 0$. Then $N_n = 0$ w.h.p.
>
> **(ii) Second moment method:** Suppose $\dfrac{\operatorname{Var}(N_n)}{\mathbb{E}[N_n]^2} \to 0$. Then $N_n > 0$ w.h.p.

**Remark:**

$$\frac{\operatorname{Var}(N_n)}{\mathbb{E}[N_n]^2} = \frac{\mathbb{E}[N_n^2]}{\mathbb{E}[N_n]^2} - 1,$$

so the condition for (ii) is equivalently $\mathbb{E}[N_n^2]/\mathbb{E}[N_n]^2 \to 1$. In applying (ii) we will typically have $\mathbb{E}[N_n] \to \infty$ and $\operatorname{Var}(N_n / \mathbb{E}[N_n]) \to 0$.

**Proof.**

**(i)** Since $N_n$ is integer-valued and non-negative:

$$\mathbb{P}(N_n \neq 0) = \mathbb{P}(N_n \geq 1) \leq \frac{\mathbb{E}[N_n]}{1} \xrightarrow{n \to \infty} 0. \quad \square$$

**(ii)** Define $X_n = N_n / \mathbb{E}[N_n]$. Then $\mathbb{E}[X_n] = 1$ and

$$\operatorname{Var}(X_n) = \operatorname{Var}\!\left(\frac{N_n}{\mathbb{E}[N_n]}\right) = \frac{\operatorname{Var}(N_n)}{\mathbb{E}[N_n]^2} \xrightarrow{n \to \infty} 0.$$

By Lemma 1.14, $X_n \xrightarrow{\mathbb{P}} 1$. Then:

$$\mathbb{P}(N_n = 0) = \mathbb{P}(X_n = 0) \leq \mathbb{P}(|X_n - 1| \geq 1) \xrightarrow{n \to \infty} 0.$$

Thus $\mathbb{P}(N_n > 0) \to 1$, so $N_n > 0$ w.h.p. $\square$

---

**N.B.** It is *not* enough to assume only $\mathbb{E}[N_n] \to \infty$ in (ii). Counter-example:

$$\mathbb{P}(N_n = n^2) = \frac{1}{n}, \qquad \mathbb{P}(N_n = 0) = 1 - \frac{1}{n}. \qquad \bigl(\mathbb{E}[N_n] = n \to \infty.\bigr)$$

---

## Application: Triangles

$N_n(3) = \#$ triangles in $G(n, p_n)$, with $\mathbb{E}[N_n(3)] = \binom{n}{3} p_n^3$.

If $p_n \gg 1/n$ then $\mathbb{E}[N_n(3)] \to \infty$. To apply the second moment method we need to bound $\operatorname{Var}(N_n(3))$.
