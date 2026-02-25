---
layout: default
title: "Lecture 4 — Outer Measures, Carathéodory's Lemma & Premeasures"
---

<a href="{{ '/ma32061/' | relative_url }}" class="back-link">← MA32061 Measure Theory & Integration</a>

# Lecture 4 — Outer Measures, Carathéodory's Lemma & Premeasures

---

## §6: Outer Measures

**Idea:** Lebesgue outer measure → Lebesgue measure.

> **Definition 6.1 (Outer Measure).** Let $X \neq \emptyset$. $\mu^*$ is an **outer measure** on $X$ if $\mu^* : \mathcal{P}(X) \to [0, \infty]$ satisfies:
>
> **(i)** $\mu^*(\emptyset) = 0$
>
> **(ii) Monotonicity:** If $A, B \subseteq X$ and $A \subseteq B$, then $\mu^*(A) \leq \mu^*(B)$.
>
> **(iii) Countable subadditivity:** If $\{A_j\}_{j=1}^\infty$ is a family of subsets of $X$, then
> $$\mu^*\!\left(\bigcup_{j=1}^\infty A_j\right) \leq \sum_{j=1}^\infty \mu^*(A_j).$$

**Example:** On $X = \mathbb{R}$, the **Lebesgue outer measure** satisfies these properties, where, if $A \subseteq \mathbb{R}$:

$$\mu^*(A) = \inf\left\{\sum_{j=1}^\infty |I_j| \;\middle|\; \{I_j\}_{j=1}^\infty \text{ is a cover of } A \text{ by open intervals}\right\}$$

The Lebesgue outer measure also satisfies:
- $\mu^*$ is **translation invariant**: $\mu^*(A + h) = \mu^*(A)$, $A \subseteq \mathbb{R}$, $h \in \mathbb{R}$
- $\mu^*((a,b)) = b - a$

---

> **Definition 6.2 ($\mu^*$-measurable sets).** Let $X \neq \emptyset$, $\mu^*$ an outer measure on $X$. We say $A \subseteq X$ is **$\mu^*$-measurable** if:
>
> $$\forall E \subseteq X, \quad \mu^*(E) = \mu^*(E \cap A) + \mu^*(E \cap A^c)$$

**Remarks:**

1. $\emptyset, X$ are $\mu^*$-measurable.
2. $A$ is $\mu^*$-measurable iff $A^c = X \setminus A$ is $\mu^*$-measurable.
3. If $A, E \subseteq X$: since $E = (E \cap A) \cup (E \cap A^c)$, we have $\mu^*(E) \leq \mu^*(E \cap A) + \mu^*(E \cap A^c)$ by subadditivity. So $A$ is $\mu^*$-measurable iff
$$\forall E \subseteq X, \quad \mu^*(E) \geq \mu^*(E \cap A) + \mu^*(E \cap A^c).$$

---

> **Lemma 6.4.** Let $\mu^*$ be the Lebesgue outer measure on $\mathbb{R}$. Let $a < b$ and $I$ any of $(a,b)$, $(a,b]$, $[a,b)$, $[a,b]$. Then $I$ is $\mu^*$-measurable.

**Proof.** Let $E \subseteq \mathbb{R}$. To prove: $\mu^*(E) \geq \mu^*(E \cap I) + \mu^*(E \cap I^c)$.

Let $\{I_j\}_{j=1}^\infty$ be a cover of $E$ by open intervals. Then:
- $\forall j$, $I_j \cap I$ is empty or an interval.
- $\forall j$, $I_j \cap I^c$ is empty, an interval, or the union of two intervals.

Let $\varepsilon > 0$. For each $j$, choose open intervals $I_j'$, $I_j''$, $I_j'''$ with
$$I_j \cap I \subseteq I_j', \quad I_j \cap I^c \subseteq I_j'' \cup I_j'''$$
such that $|I_j'| + |I_j''| + |I_j'''| \leq |I_j| + \dfrac{\varepsilon}{2^j}$.

Since $I \cap E \subseteq I \cap \bigl(\bigcup_j I_j\bigr) = \bigcup_j(I \cap I_j) \subseteq \bigcup_j I_j'$, this implies

$$\mu^*(I \cap E) \leq \sum_{j=1}^\infty |I_j'|$$

Similarly, $\mu^*(I^c \cap E) \leq \sum_{j=1}^\infty |I_j''| + |I_j'''|$. So

$$\mu^*(I \cap E) + \mu^*(I^c \cap E) \leq \sum_{j=1}^\infty \left(|I_j| + \frac{\varepsilon}{2^j}\right) = \sum_{j=1}^\infty |I_j| + \varepsilon$$

Taking inf: $\mu^*(I \cap E) + \mu^*(I^c \cap E) \leq \mu^*(E)$. $\square$

---

> **Theorem 6.5 (Carathéodory's Lemma).** Let $X \neq \emptyset$ and $\mu^*$ an outer measure on $X$. Then:
>
> **(i)** $\mathcal{A} = \{A \subseteq X \mid A \text{ is } \mu^*\text{-measurable}\}$ is a $\sigma$-algebra.
>
> **(ii)** $\mu = \mu^*\!\big|_{\mathcal{A}}$ is a **complete** measure on $\mathcal{A}$.

**Proof (Non-Examinable, Sketch).**

**(i)** Check:
- $\emptyset, X \in \mathcal{A}$ ✓ · Closed under complement ✓
- $\mathcal{A}$ closed under countable unions: if $A, B \in \mathcal{A}$, then $A \cup B \in \mathcal{A}$.

To check: let $E \subseteq X$. Need $\mu^*(E) \geq \mu^*(E \cap (A \cup B)) + \mu^*(E \cap (A \cup B)^c)$.

Using $A \in \mathcal{A}$: $\mu^*(E) \geq \mu^*(E \cap A) + \mu^*(E \cap A^c)$

Using $B \in \mathcal{A}$: $\mu^*(E \cap A) \geq \mu^*(E \cap A \cap B) + \mu^*(E \cap A \cap B^c)$

Similarly $\mu^*(E \cap A^c) \geq \mu^*(E \cap A^c \cap B) + \mu^*(E \cap A^c \cap B^c)$. So

$$\mu^*(E) \geq \mu^*(E \cap A \cap B) + \mu^*(E \cap A \cap B^c) + \mu^*(E \cap A^c \cap B) + \mu^*(E \cap A^c \cap B^c)$$

Note $(A \cup B)^c = A^c \cap B^c$ and $A \cup B = (A \cap B) \cup (A \cap B^c) \cup (A^c \cap B)$. By subadditivity (iii):

$$\mu^*(E) \geq \mu^*(E \cap (A \cup B)) + \mu^*(E \cap (A \cup B)^c) \quad \square$$

---

## §6.1: The Lebesgue Measure

> **Definition 6.6.** The **Lebesgue measure** on $\mathbb{R}$ is defined as the restriction of the Lebesgue outer measure $\mu^*$ to the $\sigma$-algebra of $\mu^*$-measurable sets.

**Notation:** $\Sigma = \Sigma_1 =$ Lebesgue $\sigma$-algebra $=$ all $\mu^*$-measurable sets of $\mathbb{R}$; $\mu, m, \lambda, \lambda' =$ Lebesgue measure.

**Remarks:**
- All intervals $(a,b)$, $(a,b]$, $[a,b)$, $[a,b]$ are in $\Sigma$.
- The Borel $\sigma$-algebra of $\mathbb{R}$ is contained in $\Sigma$.
- Borel $\sigma$-algebra $\neq \Sigma$.
- The Lebesgue measure restricted to the Borel $\sigma$-algebra is a measure.

---

## §6.2: Premeasures and Carathéodory's Theorem

Let $X \neq \emptyset$ and $\mathfrak{S} \subseteq \mathcal{P}(X)$. Suppose:
- $\emptyset \in \mathfrak{S}$
- There exists $\{E_j\}_{j=1}^\infty \subseteq \mathfrak{S}$ such that $X \subseteq \bigcup_{j=1}^\infty E_j$

Suppose $\rho : \mathfrak{S} \to [0, \infty]$ with $\rho(\emptyset) = 0$. It is natural to define for $A \subseteq X$:

$$\mu^*(A) = \inf\left\{\sum_{j=1}^\infty \rho(E_j) \;\middle|\; \{E_j\}_{j=1}^\infty \subseteq \mathfrak{S},\; A \subseteq \bigcup_{j=1}^\infty E_j\right\}$$

$\mathfrak{S}$ is called a **covering class** of $\rho$.

> **Proposition 6.7.** Let $X$, $\mathfrak{S}$, $\rho$, $\mu^*$ be as above. Then $\mu^*$ is an outer measure.

**Proof.** We verify all three conditions:
- $\mu^*(\emptyset) = 0$ ✓
- $A \subseteq B \Rightarrow \mu^*(A) \leq \mu^*(B)$ ✓ (any cover of $B$ covers $A$)
- Countable subadditivity: if $\{A_j\} \subseteq \mathcal{P}(X)$, we may assume $\mu^*(A_j) < \infty$ for all $j$. Let $\varepsilon > 0$; for each $j$, choose $\{E_{jk}\}_{k=1}^\infty \subseteq \mathfrak{S}$ such that $A_j \subseteq \bigcup_k E_{jk}$ and $\mu^*(A_j) + \varepsilon/2^j \geq \sum_k \rho(E_{jk})$.

Since $\bigcup_j A_j \subseteq \bigcup_{j,k} E_{jk}$ and $\rho \geq 0$:

$$\mu^*\!\left(\bigcup_j A_j\right) \leq \sum_{j,k} \rho(E_{jk}) \leq \sum_j\left(\mu^*(A_j) + \frac{\varepsilon}{2^j}\right) \leq \sum_j \mu^*(A_j) + \varepsilon$$

Let $\varepsilon \to 0$: $\mu^*\!\left(\bigcup_j A_j\right) \leq \sum_j \mu^*(A_j)$. $\square$

**Example:** $X = \mathbb{R}$, $\mathfrak{S} = \{\emptyset, [0,2], [2,4], [1,3], \mathbb{R}\}$, with $\rho(\emptyset) = 0$, $\rho([0,2]) = 3$, $\rho([2,4]) = 1$, $\rho([1,3]) = 5$, $\rho(\mathbb{R}) = \infty$.

Compute $\mu^*([1,3]) = 4$ (achieved by the cover $\{[0,2], [2,4]\}$). But $\rho([1,3]) = 5$. Without additional hypotheses, $\mu^* \neq \rho(E)$ in general.

---

> **Definition 6.8 (Semi-ring / Semi-algebra).** Let $X$ be a set. $\mathfrak{S} \subseteq \mathcal{P}(X)$ is called a **semi-ring** (or **semi-algebra**) if:
>
> **(i)** $\emptyset \in \mathfrak{S}$
>
> **(ii)** $A, B \in \mathfrak{S}$ implies $A \cap B \in \mathfrak{S}$
>
> **(iii)** If $A, B \in \mathfrak{S}$, then $A \setminus B$ can be represented as a finite union of disjoint sets in $\mathfrak{S}$.

**Examples:**
1. $X = \mathbb{R}$, $\mathfrak{S} = \{\text{all intervals}\}$
2. $X = \mathbb{R}$, $\mathfrak{S} = \{(a,b] : a < b\} \cup \{(a, \infty) : a \in \mathbb{R}\}$

---

> **Definition (Premeasure).** Let $X \neq \emptyset$, $\mathfrak{S}$ a semi-ring, $\rho : \mathfrak{S} \to [0, \infty]$. $\rho$ is a **pre-measure** if:
>
> **(i)** $\rho(\emptyset) = 0$
>
> **(ii)** If $\{E_j\}_{j=1}^\infty \subseteq \mathfrak{S}$ is disjoint and $\bigcup_{j=1}^\infty E_j \in \mathfrak{S}$, then
> $$\rho\!\left(\bigcup_{j=1}^\infty E_j\right) = \sum_{j=1}^\infty \rho(E_j)$$
