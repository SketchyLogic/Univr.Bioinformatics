---
tags:
  - __DEFINITION
  - Module1
---
# Generalized Hidden Markov Model (GHMM)

An extension of the standard [[Hidden Markov Model (HMM)]] that models **explicit length distributions** for each hidden state, rather than the implicit geometric distribution of basic HMMs.

**Problem with standard HMMs**: state durations follow a **geometric distribution**[^1] (memoryless). Real exon/intron lengths do not — exons cluster around 100–300 nt, and introns have a very different (often log-normal) distribution. A geometric model puts excessive probability on very short or very long features.

**GHMM solution**: on entering state q, draw a duration d from a state-specific length distribution D_q (Poisson, negative binomial, or empirical histogram), then emit exactly d symbols. This allows biologically realistic exon/intron length modeling.

**Trade-off**: the Viterbi recurrence must consider all possible durations for each state, increasing computational cost. Mitigated by capping maximum duration.

Used by [[genscan|GENSCAN]]. See [[hidden-markov-models]], [[Explain why GHMM improves on standard HMM for gene finding]].

# TLDR
Like an HMM but each state has its own realistic length distribution, so exon/intron durations are modelled as biologically observed (not as a memoryless coin flip).

---

[^1]: **Geometric distribution**: the probability that a state lasts exactly d steps is $(1-p)^{d-1} \cdot p$, where p is the probability of leaving the state at each step. It is memoryless — the time already spent in a state carries no information about how much longer it will last. Standard HMMs implicitly impose this through the self-transition probability.
