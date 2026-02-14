---
layout: default
title: "Lecture 1 — Random Walks"
---

<a href="{{ '/ma32048/' | relative_url }}" class="back-link">← MA32048 Discrete Probability</a>

# Lecture 1 — Random Walks

## Simple Symmetric Random Walk

Let $X_1, X_2, \ldots$ be i.i.d. with $\mathbb{P}(X_i = +1) = \mathbb{P}(X_i = -1) = \tfrac{1}{2}$. The **simple symmetric random walk** is:

$$
S_n = \sum_{i=1}^{n} X_i, \qquad S_0 = 0.
$$

### Basic Properties

The walk has $\mathbb{E}[S_n] = 0$ and $\text{Var}(S_n) = n$.

The probability of being at position $k$ after $n$ steps (where $n$ and $k$ have the same parity):

$$
\mathbb{P}(S_n = k) = \binom{n}{\frac{n+k}{2}} \left(\frac{1}{2}\right)^n
$$

## Generating Functions

> **Definition.** The **probability generating function** (PGF) of a non-negative integer-valued random variable $X$ is:
>
> $$G_X(s) = \mathbb{E}[s^X] = \sum_{k=0}^{\infty} \mathbb{P}(X = k) \, s^k, \qquad |s| \leq 1.$$

Key property: if $X$ and $Y$ are independent, then $G_{X+Y}(s) = G_X(s) \cdot G_Y(s)$.

## Code: Simulating Random Walks

```python
import numpy as np
import matplotlib.pyplot as plt

np.random.seed(0)
n_steps = 500
n_walks = 5

fig, ax = plt.subplots(figsize=(10, 4))
for _ in range(n_walks):
    steps = np.random.choice([-1, 1], size=n_steps)
    walk = np.concatenate([[0], np.cumsum(steps)])
    ax.plot(walk, alpha=0.7)

ax.axhline(0, color='gray', lw=0.5)
ax.set_xlabel('Step')
ax.set_ylabel('$S_n$')
ax.set_title('Simple Symmetric Random Walks')
plt.tight_layout()
plt.show()
```

---

*These are example notes — replace with your own lecture content.*
