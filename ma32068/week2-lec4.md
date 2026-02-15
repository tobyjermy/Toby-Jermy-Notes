---
layout: default
title: "Lecture 4 — Pricing for N=1 & Hedging Portfolios"
---

<a href="{{ '/ma32068/' | relative_url }}" class="back-link">← MA32068 Probability & Finance</a>

# Lecture 4 — Pricing for N=1 & Hedging Portfolios

## Theorem 2.5

> Suppose for some derivative worth $C_N$ at time $N$ and $C_0$ at time 0, there is a hedging portfolio with initial value $V_0$. If $V_0 \neq C_0$, there is arbitrage.

**Proof:** Suppose $(\beta_n, \phi_n)_{0 \leq n \leq N}$ is the H.P. and $C_0 > V_0$. We have $V_0 = \beta_0 + \phi_0 S_0$.

Consider a new portfolio $(\beta_n, \phi_n, -1)_{0 \leq n \leq N}$ of (cash, asset, derivative). Worth $V_n'$ at time $n$. This is also S.F. and adapted.

$$V_N' = \beta_N + \phi_N S_N - C_N = V_N - C_N \stackrel{\text{H.P.}}{=} 0$$

$$V_0' = V_0 - C_0 < 0$$

By Lemma 2.4, there is arbitrage.

Now consider portfolio $(-\beta_n, -\phi_n, +1)_{0 \leq n \leq N}$ worth $V_n''$. This is also S.F. and adapted.

$$V_N'' = -V_N + C_N \stackrel{\text{H.P.}}{=} 0 \quad \text{and} \quad V_0'' = -V_0 + C_0 < 0$$

So by Lemma 2.4, there is arbitrage. $\square$

---

## §2.3: Pricing for $N = 1$

> **Theorem 2.6.** In the binary model with $d < 1 + r < u$, suppose a derivative has payoff at time $N = 1$:
>
> $$C_1 = \begin{cases} C_H & \text{if } S_1 = uS_0 \\ C_T & \text{if } S_1 = dS_0 \end{cases}$$
>
> If there is no arbitrage, the price of the derivative at time 0 is:
>
> $$C_0 = \alpha^{-1}\big(C_H \, q + C_T(1 - q)\big)$$
>
> where $\alpha = 1 + r$ and $q = \dfrac{\alpha - d}{u - d}$.
>
> Also, there is a H.P. $(\beta_n, \phi_n)_{0 \leq n \leq 1}$ with:
>
> $$\phi_0 = \frac{C_H - C_T}{S_0(u - d)} \qquad \text{(the delta of the H.P. at time 0)}$$

**Proof:** Find a H.P. $(\beta_n, \phi_n)_{n=0,1}$ with $V_1 = C_1$. Then by Theorem 2.5, if there is no arbitrage, $C_0 = V_0$.

For $(\beta_n, \phi_n)$ to be a H.P. we need $(\beta_0, \phi_0)$ with:

$$\alpha \beta_0 + \phi_0 \, u \, S_0 = C_H \qquad (1)$$

$$\alpha \beta_0 + \phi_0 \, d \, S_0 = C_T \qquad (2)$$

$(1) - (2)$: $\phi_0 S_0(u - d) = C_H - C_T$, so:

$$\phi_0 = \frac{C_H - C_T}{S_0(u - d)}$$

$u(2) - d(1)$: $\alpha \beta_0(u - d) = uC_T - dC_H$, so:

$$\beta_0 = \frac{uC_T - dC_H}{\alpha(u - d)}$$

Then:

$$V_0 = \beta_0 + S_0 \phi_0 = \frac{uC_T - dC_H}{\alpha(u - d)} + \frac{(C_H - C_T)\alpha}{\alpha(u - d)}$$

$$= \alpha^{-1}\left(\frac{(\alpha - d)C_H + (u - \alpha)C_T}{u - d}\right) = \alpha^{-1}\big(q \, C_H + (1 - q) \, C_T\big) \quad \square$$

---

## Example

$S_0 = 10$, $N = 1$, $u = \frac{3}{2}$, $d = \frac{4}{5}$, $r = \frac{1}{5}$.

A call option with $N = 1$, strike price $K = 11$.

**Find $C_0$ if there is no arbitrage, and find a H.P.**

$\alpha = 1 + r = \frac{6}{5}$ and:

$$q = \frac{6/5 - 4/5}{3/2 - 4/5} = \frac{2/5}{7/10} = \frac{4}{7}$$

$$C_1 = (S_1 - 11)^+ = \begin{cases} 4 & \text{if H (since } S_1 = 15\text{)} \\ 0 & \text{if T (since } S_1 = 8\text{)} \end{cases}$$

$$C_0 = \alpha^{-1}(q \, C_H + (1 - q) \, C_T) = \frac{5}{6}\left(\frac{4}{7} \times 4 + \frac{3}{7} \times 0\right) = \frac{40}{21}$$

and:

$$\phi_0 = \frac{C_H - C_T}{S_0(u - d)} = \frac{4 - 0}{15 - 8} = \frac{4}{7}$$

$$\beta_0 + \phi_0 S_0 = V_0 \stackrel{\text{H.P.}}{=} C_0 = \frac{40}{21} \quad \Rightarrow \quad \beta_0 = -\frac{80}{21}$$

**Exercise:** Check this works, i.e. $V_1 = C_1$ for both scenarios.

---

**Recall:** "There is no arbitrage" $\Rightarrow$ $C_0 = \alpha^{-1}(C_H \, q + C_T(1-q))$. We will later prove the reverse implication.

$C_0$ is the **no-arbitrage price of the derivative**.
