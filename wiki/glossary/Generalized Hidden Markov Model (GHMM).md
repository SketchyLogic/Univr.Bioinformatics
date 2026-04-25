---
tags:
  - __DEFINITION
  - Module1
---
# Generalized Hidden Markov Model (GHMM)

An extension of the standard [[Hidden Markov Model (HMM)]] that models **explicit length distributions** for each hidden state, rather than the implicit geometric distribution of basic HMMs.

**Problem with standard HMMs**: state durations follow a **geometric distribution** (memoryless). Real exon/intron lengths do not — exons cluster around 100–300 nt, and introns have a very different (often log-normal) distribution. A geometric model puts excessive probability on very short or very long features.

**GHMM solution**: on entering state q, draw a duration d from a state-specific length distribution D_q (Poisson, negative binomial, or empirical histogram), then emit exactly d symbols. This allows biologically realistic exon/intron length modeling.

**Trade-off**: the Viterbi recurrence must consider all possible durations for each state, increasing computational cost. Mitigated by capping maximum duration.

Used by [[genscan|GENSCAN]]. See [[hidden-markov-models]], [[Explain why GHMM improves on standard HMM for gene finding]].
