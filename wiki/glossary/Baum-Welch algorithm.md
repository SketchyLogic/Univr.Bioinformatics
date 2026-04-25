---
tags:
  - __DEFINITION
  - Module1
---
# Baum-Welch algorithm

An **Expectation-Maximisation (EM)** algorithm that solves the learning problem for [[Hidden Markov Model (HMM)|HMMs]]: estimating the transition matrix A, emission matrix B, and initial distribution π from observed sequences, when the true state path is unknown.

**Two steps per iteration**:
1. **E-step**: compute the expected number of times each transition (i → j) and emission (state i, symbol k) occurred, using the [[Forward algorithm]] and its symmetric Backward algorithm.
2. **M-step**: re-estimate A, B, π to maximise the expected log-likelihood (closed-form update equations).

**Convergence**: guaranteed to converge to a **local** maximum of the likelihood (not necessarily global).

**Use in gene prediction**: trains HMM parameters from unlabelled genomic sequences when annotated training data is unavailable (unsupervised / self-training). Enables de novo gene prediction on newly sequenced genomes.

See [[hidden-markov-models]], [[Forward algorithm]].
