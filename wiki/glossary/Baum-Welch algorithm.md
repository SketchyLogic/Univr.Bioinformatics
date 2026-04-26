---
tags:
  - __DEFINITION
  - Module1
CreatedAt: 2026-04-25
LastUpdateAt: 2026-04-25
LastReviewAt: null
ReviewerIds:
  - admin
OwnerIds:
  - admin
IssueNotes: null
GeneratedById: claude-sonnet-4-6
---
# Baum-Welch algorithm

An **Expectation-Maximisation (EM)**[^1] algorithm that solves the learning problem for [[Hidden Markov Model (HMM)|HMMs]]: estimating the transition matrix A, emission matrix B, and initial distribution π from observed sequences, when the true state path is unknown.

**Two steps per iteration**:
1. **E-step**: compute the expected number of times each transition (i → j) and emission (state i, symbol k) occurred, using the [[Forward algorithm]] and its symmetric Backward algorithm.
2. **M-step**: re-estimate A, B, π to maximise the expected log-likelihood (closed-form update equations).

**Convergence**: guaranteed to converge to a **local** maximum of the likelihood (not necessarily global).

**Use in gene prediction**: trains HMM parameters from unlabelled genomic sequences when annotated training data is unavailable (unsupervised / self-training). Enables de novo gene prediction on newly sequenced genomes.

See [[hidden-markov-models]], [[Forward algorithm]].

# TLDR
Learns HMM parameters from unlabelled sequences: repeatedly estimate which state paths were likely (E-step), then update transition/emission probabilities to fit those estimates better (M-step).

---

[^1]: **Expectation-Maximisation (EM)**: a general iterative optimisation strategy for models with hidden variables. E-step computes the expected value of hidden variables given current parameters; M-step maximises likelihood given those expectations. Repeating guarantees convergence to a local maximum.
