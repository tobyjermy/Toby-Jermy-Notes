---
layout: default
title: "Lecture 5 — Risk-Neutral Pricing & Extension to N Periods"
---

<a href="{{ '/ma32068/' | relative_url }}" class="back-link">← MA32068 Probability & Finance</a>

# Lecture 5 — Risk-Neutral Pricing & Extension to $N$ Periods

## Recall from Lecture 4

> **Recall:** "There is no arbitrage" $\Rightarrow$ $C_0 = \alpha^{-1}(C_H\,q + C_T(1-q))$.
>
> We will later prove the reverse implication.
>
> $C_0$ is the **no-arbitrage price of the derivative**.

---

## Risk-Neutral Probability Measure

This can be viewed as an expected value if we assume the probability of $H$ is $q$ rather than $p$. This is called the **risk-neutral probability measure**.

Write $\tilde{\mathbb{P}}(\cdot)$ and $\tilde{\mathbb{E}}[\cdot]$ under the risk-neutral probability measure where the probability of $H$ is $q$, not $p$. Then:

$$C_0 = \alpha^{-1}\,\tilde{\mathbb{E}}[C_1]$$

**Intuition:** $\alpha^{-1}$ corresponds to taking the present value ($t = 0$) of a future payment (at $t = 1$), i.e. the amount to put in the bank at $t = 0$ to have amount 1 at time $N = 1$.

This is called **discounting** the future payment, and the factor $\alpha^{-1} = (1+r)^{-1}$ is the **discount factor**.

> Thus, the arbitrage-free price of the derivative is the **expected discounted payoff** under the risk-neutral probability measure.

**Checking the risky asset:** The expected value of the risky asset at $t = 1$ under the risk-neutral measure is:

$$\tilde{\mathbb{E}}[S_1] = uS_0\,q + dS_0(1-q) = S_0\!\left(\frac{u(\alpha - d) + d(u - \alpha)}{u - d}\right) = S_0\alpha$$

So the discounted expected value of the risky asset at $t = 1$ is $\alpha^{-1}\tilde{\mathbb{E}}[S_1] = S_0$.

> A person is **risk-neutral** (as opposed to **risk-averse** or **risk-loving**) if a given random payment $X$ has the same value to them as a fixed payment equal to the expectation of $X$.
>
> The risk-neutral measure makes the discounted (random) value of the asset at $t = 1$ equal to that of the asset at $t = 0$, for the risk-neutral person.

---

## §2.4: Extension to $N \geq 1$

**Multiple period markets.** If $N \geq 1$, compute the price of the derivative at time $N - 1$ given info up to time $N - 1$, reducing the problem to a one-period model.

Suppose we are at time $N - 2$; now we know what the price must be at time $N - 1$. Repeat to compute the arbitrage-free price at time $N - 2$.

---

> **Theorem 2.8.** For the binary/binomial model with $N = 2$ and $d < 1 + r < u$, suppose a derivative has payoff:
>
> $$C_2 = \begin{cases} Z_2 & \text{if } S_2 = S_0 u^2 \\ Z_1 & \text{if } S_2 = S_0 ud \\ Z_0 & \text{if } S_2 = S_0 d^2 \end{cases}$$
>
> Assuming no arbitrage, the price of this derivative is given by:
>
> $$C_0 = \alpha^{-2}\!\left(Z_2\,q^2 + 2Z_1\,q(1-q) + Z_0(1-q)^2\right)$$
>
> where $\alpha = 1 + r$ and $q = \dfrac{\alpha - d}{u - d}$.

### Example

A European call option maturing at time $N = 2$ with strike price $K$ has:

$$Z_2 = (S_0 u^2 - K)^+, \qquad Z_1 = (S_0 ud - K)^+, \qquad Z_0 = (S_0 d^2 - K)^+$$

### Proof

**Step 1.** Value of the derivative at time 1.

If the first coin toss is $H$, this is the same as for a one-step derivative paying $Z_2$ if the next step is $u$ and $Z_1$ if the next step is $d$. By Theorem 2.6:

$$C_1(H) = \alpha^{-1}(Z_2\,q + Z_1(1-q))$$

If the first toss is $T$, pay $Z_1$ if the next step is $u$ and $Z_0$ if the next step is $d$:

$$C_1(T) = \alpha^{-1}(Z_1\,q + Z_0(1-q))$$

**Step 2.** The value at time 0 is the same as for a 1-step derivative paying $C_1(H)$ if the next step is $u$ and $C_1(T)$ if the next step is $d$. By Theorem 2.6:

$$C_0 = \alpha^{-1}(C_1(H)\,q + C_1(T)(1-q))$$

$$= \alpha^{-2}\!\left((Z_2\,q + Z_1(1-q))\,q + (Z_1\,q + Z_0(1-q))(1-q)\right)$$

$$= \alpha^{-2}\!\left(Z_2\,q^2 + 2Z_1\,q(1-q) + Z_0(1-q)^2\right) \quad \square$$

Thus the arbitrage-free price of the derivative is the expected discounted payoff under the risk-neutral probability measure. The risk-neutral measure assigns probability $q$ to the event of getting $H$ in each of the 2 steps **independently**.

---

## Risk-Neutral Probability Measure for General $N$

Define:

$$\Omega_N = \{H,T\}^N = \{(\omega_1, \ldots, \omega_N) : \omega_i \in \{H,T\},\ \forall\, i \leq N\}$$

In the original model, the probability of an outcome $\omega = (\omega_1, \ldots, \omega_N)$ with $k$ heads and $N - k$ tails, i.e. $\displaystyle\sum_{i:\,\omega_i = H} 1 = k$, is:

$$\mathbb{P}[\{\omega\}] = p^k(1-p)^{N-k}$$

Define the **risk-neutral probability measure** $\tilde{\mathbb{P}}$ by:

$$\tilde{\mathbb{P}}[\{\omega\}] = q^k(1-q)^{N-k}$$

Under $\tilde{\mathbb{P}}$, different coin tosses are **independent**.

---

> **Proposition 2.9.** Suppose in the binary model there is a traded derivative having payoff $C_N$ at time $N$, where $C_N$ is determined by $S_0, S_1, \ldots, S_N$. Then:
>
> $$C_0 = \alpha^{-N}\,\tilde{\mathbb{E}}[C_N]$$
>
> implies there is no arbitrage.

### Proof

By Theorem 2.5, prove $\forall N$ that if the payoff is $C_N$ at time $N$, there exists a hedging portfolio with initial value $V_0 = \alpha^{-N}\tilde{\mathbb{E}}[C_N]$ and final value $V_N = C_N$.

**Induction on $N$:**

- **$N = 1$:** Theorem 2.6.
- **Assume true for $N = k$**, $k \in \mathbb{N}$.
- **$N = k + 1$:** Consider a one-step derivative with payoff $\psi(S_1)$ at time 1, where for $x \in \{uS_0,\, dS_0\}$:

$$\psi(x) = \alpha^{-(N-1)}\,\tilde{\mathbb{E}}[C_N \mid S_1 = x]$$

so that $\psi(S_1) = \alpha^{-(N-1)}\tilde{\mathbb{E}}[C_N \mid S_1]$.

By the base case, there is a one-step hedging portfolio with:

$$V_0 = \alpha^{-1}\,\tilde{\mathbb{E}}[\psi(S_1)] = \alpha^{-1} \cdot \alpha^{-(N-1)}\,\tilde{\mathbb{E}}\!\left[\tilde{\mathbb{E}}[C_N \mid S_1]\right] = \alpha^{-N}\,\tilde{\mathbb{E}}[C_N]$$

Thus we can invest $V_0$ at time 0 into a 1-step portfolio worth $\psi(S_1)$ at time 1. By the induction hypothesis, for either possible value of $S_1$, reinvest into a 2nd self-financing portfolio from time 1 to $N$ worth $C_N$ at time $N$, yielding a self-financing portfolio. $\square$
