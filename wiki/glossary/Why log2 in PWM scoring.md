---
tags:
  - __CONCEPT
  - Module1
CreatedAt: 2026-04-29
LastUpdateAt: 2026-04-30
LastReviewAt: null
ReviewerIds:
  - admin
OwnerIds:
  - admin
IssueNotes: null
GeneratedBy: claude-sonnet-4-6
---

# Why log₂ in PWM scoring

## The starting point: probability of a sequence

Assume the positions of a signal are independent (Why log2 in PWM). Then the probability of observing a specific window of sequence $s_1 s_2 \ldots s_l$, given the signal model, is the **product** of per-position probabilities:

> [!Info]
> **$M_{s_j,\, j}$ notation**: 
> - $M$ is the PWM — a table with 4 rows (one per base: A, C, G, T) and $l$ columns (one per position). 
> - $j$ is the column index (current position in the window); 
> - $s_j$ is the base you actually observed at that position. 
> 
> So $M_{s_j,\, j}$ means: go to column $j$, look up the row for the observed base, return that frequency. It is a single cell lookup per position.

$$P(\text{window} \mid \text{signal}) = \prod_{j=1}^{l} M_{s_j,\, j}$$

And under the background model (uniform: each base = 0.25):

$$P(\text{window} \mid \text{background}) = \prod_{j=1}^{l} 0.25 = 0.25^l$$

To decide whether the window looks like signal or noise, you form the **likelihood ratio**:

$$\text{LR} = \frac{P(\text{window} \mid \text{signal})}{P(\text{window} \mid \text{background})} = \prod_{j=1}^{l} \frac{M_{s_j,\, j}}{0.25}$$

LR > 1 means "more likely signal than noise." This is already the right quantity. So why take the log?

---

## Problem 1: products of small numbers vanish

Each per-position probability is a number between 0 and 1. Multiply enough of them together and the result approaches zero faster than floating-point arithmetic can represent it.

Example: a window of length 20, each frequency ≈ 0.3:

$$0.3^{20} \approx 3.5 \times 10^{-11}$$

For longer windows (splice site models routinely use 20–40 positions) the product underflows to 0 in a computer, making all candidates score identically — useless.

Taking the log turns the product into a sum, which stays in a numerically safe range:

$$\log_2 \prod_{j} \frac{M_{s_j,j}}{0.25} = \sum_{j} \log_2 \frac{M_{s_j,j}}{0.25}$$

---

## Problem 2: the neutral point is 1, not 0

With raw ratios, "no information" means LR = 1 (signal and background equally likely). A position where all four bases appear at frequency 0.25 contributes a factor of $0.25/0.25 = 1$ — it neither raises nor lowers the score. Multiplying by 1 does nothing, which is correct, but makes it harder to reason about what each position contributes.

After the log:
- $\log_2(1) = 0$ → neutral, carries no information
- $\log_2(x) > 0$ (when $x > 1$) → base is enriched at this position → positive vote
- $\log_2(x) < 0$ (when $x < 1$) → base is depleted at this position → penalty

Zero becomes the natural centre. Contributions are visible as positive or negative numbers you can inspect and sum.

---

## Worked example

Four-position window, scoring it as a candidate donor site:

| pos | base observed | $M_{s_j,j}$ (signal freq.) | background | ratio | $\log_2$  |
| --- | ------------- | -------------------------- | ---------- | ----- | --------- |
| 1   | G             | 0.95                       | 0.25       | 3.80  | **+1.93** |
| 2   | T             | 0.90                       | 0.25       | 3.60  | **+1.85** |
| 3   | A             | 0.30                       | 0.25       | 1.20  | **+0.26** |
| 4   | C             | 0.05                       | 0.25       | 0.20  | **−2.32** |

**Raw likelihood ratio** (multiplying):
$$3.80 \times 3.60 \times 1.20 \times 0.20 = 3.28$$

**Log score** (adding):
$$1.93 + 1.85 + 0.26 + (-2.32) = +1.72 \text{ bits}$$

Both give the same verdict (this window looks somewhat like a donor site), but the log version:
- Is a simple sum instead of a product
- Shows you immediately that position 4 is the weak link (−2.32 penalty)
- Stays numerically well-behaved for long windows

---

## Why base 2 specifically?

Using $\log_2$ gives scores in **bits**, the unit of information from information theory.

A position where one base appears 100% of the time is perfectly informative:

$$\log_2 \frac{1.0}{0.25} = \log_2 4 = 2 \text{ bits}$$

This is exactly the information gained by knowing that one specific base (out of 4 equally likely possibilities) must appear — $\log_2 4 = 2$ bits. A position where all four bases are equally common contributes 0 bits. This connection to information theory makes scores interpretable: you can ask "how many bits of information does this signal carry?" and compare different models or signal types on the same scale.

Any other log base would work mathematically — base 2 is a convention that keeps scores human-readable and information-theoretically meaningful.

# Connections
see [[Refresher on conditional probabilities]].

# TLDR

Log₂ is taken because: 
	1. it converts a product of probabilities into a numerically stable sum; 
	2. It moves the neutral point from 1 to 0, making each position's contribution directly readable; 
	3. Base 2 gives scores in bits, connecting them to information theory.
