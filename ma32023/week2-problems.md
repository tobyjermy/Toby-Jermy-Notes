---
layout: default
title: "Problem Class 1 — Beta-Binomial Posterior & Mice Genetics"
---

<a href="{{ '/ma32023/' | relative_url }}" class="back-link">← MA32023 Bayesian Statistics</a>

# Problem Class 1 — Beta-Binomial Posterior & Mice Genetics

---

## Question 1: Mice Genetics

**Setup:** Mouse colour depends on genes $B, b$:

- **Black:** BB or Bb (homozygous BB, heterozygous Bb)
- **Brown:** bb

The offspring of a pair of mice have two genes, one from each parent. If the parent is heterozygous, the inherited gene is equally likely to be $B$ or $b$.

### Part (a)

**Generation 0:** Two Bb parents. **Generation 1:** Black offspring.

Find $\mathbb{P}(G_1 \text{ is homozygous} \mid G_0 \text{ both Bb}, G_1 \text{ Black})$.

Since $G_1$ is black, it must be BB or Bb (not bb). So:

$$= \mathbb{P}(G_1 = BB \mid G_0 = Bb, G_1 \text{ Black})$$

$$= \frac{\mathbb{P}(G_1 = BB \mid G_0 = Bb)}{\mathbb{P}(G_1 \text{ Black} \mid G_0 = Bb)}$$

From the Punnett square (Bb × Bb):

| | B | b |
|---|---|---|
| **B** | BB | Bb |
| **b** | Bb | bb |

- $\mathbb{P}(\text{BB}) = \frac{1}{4}$, $\mathbb{P}(\text{Bb}) = \frac{1}{2}$, $\mathbb{P}(\text{bb}) = \frac{1}{4}$
- $\mathbb{P}(\text{Black}) = \frac{3}{4}$

Therefore:

$$\mathbb{P}(G_1 = BB \mid G_0 = Bb, G_1 \text{ Black}) = \frac{1/4}{3/4} = \frac{1}{3}$$

**Heterozygous:** $\mathbb{P}(G_1 = Bb \mid G_0 = Bb, G_1 \text{ Black}) = \frac{1/2}{3/4} = \frac{2}{3}$ (or by complement).

### Part (b)

Now suppose this black mouse ($G_1$) is mated with a **brown mouse** ($M = bb$), resulting in **7 offspring, all black**.

Find $\mathbb{P}(G_1 = BB \mid M = bb, G_2 = \text{7 Black}, G_0 = Bb)$.

Let $H_1$ denote the background: $M = bb$ and $G_0 = Bb$.

$$= \frac{\mathbb{P}(G_2 = \text{7BLO} \mid G_1 = BB, H_1) \cdot \mathbb{P}(G_1 = BB \mid H_1)}{\mathbb{P}(G_2 = \text{7BLO} \mid H_1)}$$

- If $G_1 = BB$: all offspring are Bb (black), so $\mathbb{P}(G_2 = \text{7BLO} \mid G_1 = BB, H_1) = 1$.
- If $G_1 = Bb$: each offspring is black w.p. $\frac{1}{2}$, so $\mathbb{P}(G_2 = \text{7BLO} \mid G_1 = Bb, H_1) = \left(\frac{1}{2}\right)^7$.
- $\mathbb{P}(G_1 = BB \mid H_1) = \frac{1}{3}$, $\mathbb{P}(G_1 = Bb \mid H_1) = \frac{2}{3}$.

The denominator (total probability):

$$\mathbb{P}(G_2 = \text{7BLO} \mid H_1) = \mathbb{P}(\text{7BLO} \mid G_1 = BB, H_1) \cdot \mathbb{P}(BB \mid H_1) + \mathbb{P}(\text{7BLO} \mid G_1 = Bb, H_1) \cdot \mathbb{P}(Bb \mid H_1)$$

$$= 1 \cdot \frac{1}{3} + \left(\frac{1}{2}\right)^7 \cdot \frac{2}{3} = \frac{1}{3} + \frac{2}{3 \cdot 128} = \frac{1}{3} + \frac{1}{192}$$

Therefore:

$$\mathbb{P}(G_1 = BB \mid H_1, G_2 = \text{7BLO}) = \frac{1 \times \frac{1}{3}}{\frac{1}{3} + \left(\frac{1}{2}\right)^7 \cdot \frac{2}{3}}$$

---

## Question 2: Beta-Binomial Posterior

### Part (a): Posterior for $\theta$ given fewer than 3 heads

**Setup:**

$$\pi(\theta \mid \text{heads} < 3) \propto \mathbb{P}(\text{heads} < 3 \mid \theta) \cdot \pi(\theta)$$

- Prior: $\pi(\theta) = \text{Beta}(4, 4)$
- Likelihood: $\mathbb{P}(\text{Heads} < 3 \mid \theta) = \sum_{x=0}^{2} \mathbb{P}(X = x \mid \theta)$ where $X \sim B(10, \theta)$

**Likelihood × Prior:**

$$\left(\sum_{x=0}^{2} \binom{10}{x} \theta^x (1-\theta)^{10-x}\right) \left(\theta^{4-1}(1-\theta)^{4-1}\right) \propto \pi(\theta \mid x < 3)$$

The normalising constant $K$ satisfies:

$$K = \sum_{x=0}^{2} \int_0^1 \binom{10}{x} \theta^{4+x-1} (1-\theta)^{14-x-1} \, d\theta$$

Using the Beta function identity $\int_0^1 \theta^{a-1}(1-\theta)^{b-1} d\theta = \frac{\Gamma(a)\Gamma(b)}{\Gamma(a+b)}$:

$$K = \sum_{x=0}^{2} \binom{10}{x} \frac{\Gamma(4+x)\,\Gamma(14-x)}{\Gamma(18)}$$

**Facts to use:** $\binom{10}{0} = 1$, $\binom{10}{1} = 10$, $\binom{10}{2} = 45$, and $\Gamma(n) = (n-1)!$ for $n \in \mathbb{Z}^+$.

$$K = \frac{1}{\Gamma(18)} \left[1 \cdot \Gamma(4) \cdot \Gamma(14) + 10 \cdot \Gamma(5) \cdot \Gamma(13) + 45 \cdot \Gamma(6) \cdot \Gamma(12)\right]$$

$$= \frac{1}{\Gamma(18)} \left[\Gamma(4) \cdot 13 \cdot 12 \cdot \Gamma(12) + 10 \cdot \Gamma(5) \cdot \Gamma(13) + 45 \cdot \Gamma(6) \cdot \Gamma(12)\right]$$

$$= \frac{\Gamma(4)\,\Gamma(12)}{\Gamma(18)} \left[(13 \times 12) + (10 \times 4 \times 12) + (45 \times 5 \times 4)\right]$$

$$= \frac{\Gamma(4)\,\Gamma(12)}{\Gamma(18)} \cdot 1536$$

Therefore:

$$\pi(\theta \mid \text{heads} < 3) = \frac{\Gamma(18)}{\Gamma(4)\,\Gamma(12) \cdot 1536} \sum_{x=0}^{2} \binom{10}{x} \theta^{4+x-1} (1-\theta)^{14-x-1}$$

### Part (b): Posterior Mean

$$\mathbb{E}[\theta \mid \text{heads} < 3] = \int_0^1 \theta \, \pi(\theta \mid n < 3) \, d\theta$$

$$= \frac{1}{K} \sum_{x=0}^{2} \binom{10}{x} \int_0^1 \theta^{5+x-1} (1-\theta)^{14-x-1} \, d\theta$$

$$= \frac{1}{K} \sum_{x=0}^{2} \binom{10}{x} \frac{\Gamma(5+x)\,\Gamma(14-x)}{\Gamma(19)}$$

$$= \frac{1}{K} \cdot \frac{\Gamma(5)\,\Gamma(12)}{\Gamma(19)} \left[13 \cdot 12 + 10 \cdot 5 \cdot 12 + 45 \cdot 5 \cdot 6\right]$$

$$= \frac{1}{K} \cdot \frac{\Gamma(5)\,\Gamma(12)}{\Gamma(19)} \left[156 + 600 + 1350\right]$$

$$= \frac{\Gamma(18) \cdot \Gamma(5) \cdot \Gamma(12) \cdot 2106}{\Gamma(19) \cdot \Gamma(4) \cdot \Gamma(12) \cdot 1536}$$

$$= \frac{1}{18} \times 4 \times \frac{2106}{1536} = \boxed{\frac{39}{128}}$$
