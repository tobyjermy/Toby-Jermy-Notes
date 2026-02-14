---
layout: default
title: "Lecture 1 — Overview, Forward Contracts & Options"
---

<a href="{{ '/ma32068/' | relative_url }}" class="back-link">← MA32068 Probability & Finance</a>

# Lecture 1 — Overview, Forward Contracts & Options

## 1.1: Overview — Examples of Financial Risks

**Borrowing Costs** — e.g. mortgages: interest may be at a **fixed rate** or a **variable rate**. Variable rates may on average be lower, but certainty in a fixed rate may be preferred.

**Example: Airline Fuel** — Tickets sold in advance; fuel cost unknown at sale. **Solution:** Enter a **forward contract** with a speculator to provide fuel at a fixed future price.

---

> **Definition 1.1: Forward Contract.** A contract which obliges the first party to purchase an asset from the second party at a specified future date, at a fixed price — the **forward price**.

If maturity date is $N$, forward price is $K$, asset value at time $t$ is $S_t$, then:

**Value to the 1st party at time $N$:** $S_N - K$

---

> **Definition 1.2: European Call Option.** A **European call option** with **strike price** $K$ gives party A the option (no obligation) to buy the asset from B at time $N$ for price $K$. The payoff is:
>
> $$(S_N - K)^+ := \max\{0, S_N - K\}$$

**Question:** What is an appropriate upfront fee for A to pay B?

---

## Bank Account / Bond

Assume a bond with fixed interest rate $r \geq 0$ for borrowing and lending.

**Growth:** Time $n$: $x(1 + r)^n$

---

## Lemma 1.3: Fair Forward Price

> The **fair forward price** for an asset worth $S_0$ today, with delivery date $N$, is $(1 + r)^N S_0$.

**Proof:**

**Case 1** ($S_0(1+r)^N < K$): Short the contract, buy the asset by borrowing $S_0$. At time $N$, profit $K - S_0(1+r)^N > 0$.

**Case 2** ($S_0(1+r)^N > K$): Buy the contract, short-sell the asset, invest $S_0$ in bank. At time $N$, profit $S_0(1+r)^N - K > 0$.

Both cases achieve **arbitrage**. We assume arbitrage never occurs, so the only fair price is $(1+r)^N S_0$. $\square$
