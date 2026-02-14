---
layout: default
title: "Lecture 2 — Portfolios, Self-Financing & 𝓛ᵖ Spaces"
---

<a href="{{ '/ma32068/' | relative_url }}" class="back-link">← MA32068 Probability & Finance</a>

# Lecture 2 — Portfolios, Self-Financing & $\mathcal{L}^p$ Spaces

## 1.2: Financial Basics

A **portfolio** in discrete time is a sequence $(\beta_0, \phi_0, \beta_1, \phi_1, \ldots)$ where $\beta_n$ is cash held and $\phi_n$ is risky asset held at time $n$.

$$V_n = \beta_n + \phi_n S_n \quad \text{(portfolio value at time } n\text{)}$$

The portfolio is **self-financing (SF)** if:

$$V_{n+1} = (1+r)\beta_n + \phi_n S_{n+1}$$

"Not putting money in or out at time $n+1$!"

For $K$ risky assets: $V_n = \beta_n + \sum_{i=1}^K \phi_n^i S_n^i$, and SF means $V_{n+1} = (1+r)\beta_n + \sum_{i=1}^K \phi_n^i S_{n+1}^i$.

**We allow:** Short-selling ($\phi_n^i < 0$), borrowing ($\beta_n < 0$), no transaction costs, same buy/sell price, no dividends, $r \geq 0$.

---

## Example 1.6

$(S_0, S_1, S_2) = (100, 120, 110)$, $r = 0.1$. SF portfolio with $V_0 = 1000$, $\phi_0 = +20$, $\phi_1 = -20$.

$\beta_0 = 1000 - 20 \times 100 = -1000$ (borrowed).

$V_1 = -1100 + 20 \times 120 = 1300$.

$\beta_1 = 1300 + 20 \times 120 = 3700$.

$V_2 = 3700 \times 1.1 + (-20) \times 110 = £1870$.

---

## 1.3: Probability Background

Let $(\Omega, \mathcal{A}, \mathbb{P})$ be a probability space. For $p = 1$ or $p = 2$:

$$\mathcal{L}^p = \{X : \Omega \to \mathbb{R} : X \text{ is a RV and } \mathbb{E}[|X|^p] < \infty\}$$

"$X_n \to X$ in $\mathcal{L}^p$" means $\mathbb{E}[|X_n - X|^p] \to 0$.

"$(X_n)$ is **Cauchy** in $\mathcal{L}^p$" means $\mathbb{E}[|X_n - X_m|^p] \to 0$ as $n, m \to \infty$.

---

## Remark 1.7 ($\mathcal{L}^p$ Spaces and RVs)

1. $X \in \mathcal{L}^1$: $\mathbb{E}[|X|] = 0 \Leftrightarrow \mathbb{P}(X = 0) = 1$
2. $\text{Var}(X) = \mathbb{E}[X^2] - \mathbb{E}[X]^2 \geq 0$
3. $\mathcal{L}^2 \subset \mathcal{L}^1$ (since $\mathbb{E}[|X|]^2 \leq \mathbb{E}[X^2]$)
4. $X_n \to X$ in $\mathcal{L}^p \Rightarrow \mathbb{E}[X_n^p] \to \mathbb{E}[X^p]$
5. $X, Y \in \mathcal{L}^2 \Rightarrow X + Y \in \mathcal{L}^2$
6. $X_n \to X$ and $Y_n \to Y$ in $\mathcal{L}^2 \Rightarrow (X_n + Y_n) \to X + Y$ in $\mathcal{L}^2$
