---
layout: default
title: "Lecture 3 — Conditional Expectation & The Binary Model"
---

<a href="{{ '/ma32068/' | relative_url }}" class="back-link">← MA32068 Probability & Finance</a>

# Lecture 3 — Conditional Expectation & The Binary Model

## Remark 1.7 (continued)

Also, $|X + Y|^2 \leq (2\max(|X|, |Y|))^2 \leq 4(|X|^2 + |Y|^2)$.

**vi)** If $X_n \to X$ in $\mathcal{L}^p$ ($p = 1$ or $p = 2$), then we can find a strictly increasing subsequence $(n_k)_{k \geq 1}$ of $\mathbb{N}$ s.t. $X_{n_k} \to X$ a.s., i.e. $\mathbb{P}[\lim_{k \to \infty} X_{n_k} = X] = 1$.

**vii) The Riesz–Fischer Theorem (Completeness of $\mathcal{L}^2$):** If $(X_n)_{n \geq 1}$ is a Cauchy sequence in $\mathcal{L}^2$, then there exists a limit RV $Y \in \mathcal{L}^2$ s.t. $X_n \to Y$ in $\mathcal{L}^2$ as $n \to \infty$.

**viii) The Bounded Convergence Theorem:** If $X_n \to X$ a.s. and there is a constant $K$ s.t. $\mathbb{P}[|X_n| \leq K] = 1$ $\forall n$, then $\mathbb{E}[X_n] \to \mathbb{E}[X]$.

---

## Conditional Expectation

Suppose $X : \Omega \to \mathbb{R}$ is a RV in $\mathcal{L}^1$ and $\underline{Y} = (Y_1, \ldots, Y_k)$ a random vector. The **conditional expectation** $\mathbb{E}[X \mid \underline{Y}]$ is a RV $Z$ with:

- $Z$ is a measurable function of $\underline{Y}$
- For any RV $W$ that is a bounded, measurable function of $\underline{Y}$: $\mathbb{E}[ZW] = \mathbb{E}[XW]$
- Defined the same way if $\underline{Y}$ is an infinite random vector.

**Properties:**

- If $X \perp\!\!\!\perp \underline{Y}$, then $\mathbb{E}[X \mid \underline{Y}] = \mathbb{E}[X]$
- If $X$ is a measurable function of $\underline{Y}$, then $\mathbb{E}[X \mid \underline{Y}] = X$

If $\underline{Y}$ is discrete with possible values $\underline{y}_1, \underline{y}_2, \ldots$, then $\mathbb{E}[X \mid \underline{Y}]$ is the RV $Z = f(\underline{Y})$ where $f(\underline{y}) = \mathbb{E}[X \mid \underline{Y} = \underline{y}]$.

**TOWIK:** For any bounded, measurable function $h(\underline{Y})$:

$$\mathbb{E}[X h(\underline{Y}) \mid \underline{Y}] = h(\underline{Y}) \, \mathbb{E}[X \mid \underline{Y}]$$

**Tower Property:** If $\underline{U}, \underline{V}$ are random vectors, then:

$$\mathbb{E}\big[\mathbb{E}[X \mid \underline{U}, \underline{V}] \mid \underline{U}\big] = \mathbb{E}[X \mid \underline{U}]$$

**Further properties:**

- $\mathbb{E}[X + X' \mid \underline{Y}] = \mathbb{E}[X \mid \underline{Y}] + \mathbb{E}[X' \mid \underline{Y}]$ and $\mathbb{E}[aX \mid \underline{Y}] = a\,\mathbb{E}[X \mid \underline{Y}]$
- If $X \geq 0$ a.s., then $\mathbb{E}[X \mid \underline{Y}] \geq 0$ a.s.

**Conditional Jensen Inequality:** If $X \in \mathcal{L}^2$:

$$\big(\mathbb{E}[X \mid \underline{Y}]\big)^2 \leq \mathbb{E}[X^2 \mid \underline{Y}]$$

---

## §2: Derivative Pricing in Discrete Time

### 2.1: The Binary Model

Consider a single asset which can go **up** or **down** by a fixed percentage change, randomly. Call this the **risky asset** to distinguish from the bank account.

Suppose we have a fixed time horizon $N \in \mathbb{N}$, and at each time independently we flip a (possibly biased) coin with probability $p$ of heads, $p \in (0,1)$.

- **Heads:** $S_n \mapsto S_{n+1} = uS_n$
- **Tails:** $S_n \mapsto S_{n+1} = dS_n$

where $0 < d < u$.

E.g. if the asset goes up or down by 5%, then $u = 1.05$, $d = 0.95$.

Define $(S_n)_{n \geq 1}$ as a sequence of RVs on event space:

$$\Omega_N = \{H, T\}^N = \{\omega = (\omega_1, \ldots, \omega_N) : \omega_i \in \{H, T\} \ \forall i \in \{1, \ldots, N\}\}$$

Assign to elements the usual (biased) coin probabilities: if $\omega$ has $K$ heads and $N - K$ tails, $\mathbb{P}(\{\omega\}) = p^K(1-p)^{N-K}$. The flips are independent.

This is the **Binary / Binomial model** for asset prices.

To specify a market: specify $S_0$, $u$, $d$, interest rate $r$, time horizon $N$, and up probability $p$.

---

### 2.2: Derivative Pricing, Hedging & Arbitrage

The market may feature **derivatives** whose value is determined by that of the underlying asset. E.g. a European call option with strike price $K$:

$$C_N = (S_N - K)^+ = \max\{0, S_N - K\}$$

The final value of an option is its **payoff**. For earlier times $n < N$, let the value of the call option at time $n$ be $C_n$. What is $C_0$ — the current value of the option?

**Example:** A bank who sells a client an option is exposed to risk associated to the final value. They want to **hedge** this risk — mitigate uncertainty associated with potential future payout due to their **short position**. They may try trading in the underlying to "replicate" the payoff.

> **Definition 2.1.** A **hedging portfolio** for a derivative with payoff $C_N$ at time $N$ is an adapted, self-financing portfolio $(\beta_n, \phi_n)_{0 \leq n \leq N}$ satisfying $V_N = C_N$ for all possible outcomes.
>
> **Adapted:** For each $n \in \{1, \ldots, N\}$, $(\beta_n, \phi_n)$ is determined by $(S_k : k \leq n)$, while $\beta_0, \phi_0$ are constants.

The value of $\phi_0$ in a hedging portfolio is called the **delta** of the portfolio at time 0.

---

> **Definition 2.2: Arbitrage.** Suppose $(S_n^1, \ldots, S_n^K)_{n=0,\ldots,N}$ is a sequence of $K$ stochastic processes under some probability measure $\mathbb{P}$, the prices of $K$ risky assets. Let $\underline{\phi}_n = (\phi_n^0, \phi_n^1, \ldots, \phi_n^K)$ be a self-financing portfolio where $\phi_n^0 = \beta_n$, and $\phi_n^j$ depends only on asset values up to time $n$.
>
> If $V_0 = 0$, and $\mathbb{P}(V_N < 0) = 0$ and $\mathbb{P}(V_N > 0) > 0$, then $\underline{\phi}_n$ is called an **arbitrage**.

An arbitrage means we can make risk-free profit with strictly positive probability. If $\underline{\phi}$ is an arbitrage, then $a\underline{\phi}$ (constant $a > 0$) would yield huge profits!

**Assume there is no arbitrage.**

---

> **Theorem 2.3.** In the one-period binary model, consisting only of the asset and the bank account, with $p \in (0,1)$, there is **no arbitrage** iff $d < (1+r) < u$.

> **Proof (sketch):** $d < 1+r < u$ says investing 1 in the risky asset is never guaranteed to be better or worse than investing 1 in the bank account. $\square$

---

> **Lemma 2.4.** Suppose there exists an adapted self-financing portfolio $(\phi_n^0, \ldots, \phi_n^K)_{0 \leq n \leq N}$ with $V_0 < 0$ and $\mathbb{P}[V_N = 0] = 1$. Then there exists an arbitrage.

> **Proof:** Set $a = -V_0 > 0$. Consider a new portfolio $(\phi_n^0 + a(1+r)^n, \phi_n^1, \ldots, \phi_n^K)_{0 \leq n \leq N}$. This amounts to initially adding $a$ to the bank account and leaving that money (with accrued interest) through the life of the portfolio.
>
> The new portfolio is adapted and self-financing, and if $V_n'$ denotes its value: $V_n' = V_n + a(1+r)^n$.
>
> So $V_0' = 0$ and w.p. 1, $V_N' = a(1+r)^N > 0$. Thus we have arbitrage. $\square$
