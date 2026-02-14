---
layout: default
title: "Lecture 1 — The One-Period Binomial Model"
---

<a href="{{ '/ma32068/' | relative_url }}" class="back-link">← MA32068 Probability & Finance</a>

# Lecture 1 — The One-Period Binomial Model

## Setup

Consider a market with one risky asset $S$ and a risk-free bond $B$. Over one period:

$$
S_1 = \begin{cases} S_0 \, u & \text{with probability } p \\ S_0 \, d & \text{with probability } 1 - p \end{cases}
$$

where $u > 1 > d > 0$ are the up/down factors and $B_1 = (1 + r)B_0$ for risk-free rate $r$.

## No-Arbitrage Condition

> **Proposition.** The model is arbitrage-free if and only if $d < 1 + r < u$.

## Risk-Neutral Pricing

Under the **risk-neutral measure** $\mathbb{Q}$, the risk-neutral probability is:

$$
q = \frac{(1+r) - d}{u - d}
$$

The price of a derivative with payoff $V_1$ at time 1 is:

$$
V_0 = \frac{1}{1+r}\, \mathbb{E}^{\mathbb{Q}}[V_1] = \frac{1}{1+r}\bigl[q \, V_1^u + (1-q) \, V_1^d\bigr]
$$

### Example: European Call Option

For a call option with strike $K$, the payoff is $V_1 = (S_1 - K)^+$. With $S_0 = 100$, $u = 1.2$, $d = 0.9$, $r = 0.05$, $K = 100$:

$$
q = \frac{1.05 - 0.9}{1.2 - 0.9} = 0.5, \qquad V_1^u = 20, \quad V_1^d = 0
$$

$$
V_0 = \frac{1}{1.05}(0.5 \times 20 + 0.5 \times 0) = \frac{10}{1.05} \approx 9.52
$$

## Code: Binomial Option Pricing

```python
def binomial_call(S0, K, u, d, r, n):
    """Price a European call via n-period binomial model."""
    q = ((1 + r) - d) / (u - d)
    
    # Terminal payoffs
    payoffs = [max(S0 * u**j * d**(n - j) - K, 0) for j in range(n + 1)]
    
    # Backward induction
    for i in range(n - 1, -1, -1):
        payoffs = [
            (q * payoffs[j + 1] + (1 - q) * payoffs[j]) / (1 + r)
            for j in range(i + 1)
        ]
    
    return payoffs[0]

price = binomial_call(S0=100, K=100, u=1.2, d=0.9, r=0.05, n=50)
print(f"European call price: {price:.4f}")
```

---

*These are example notes — replace with your own lecture content.*
