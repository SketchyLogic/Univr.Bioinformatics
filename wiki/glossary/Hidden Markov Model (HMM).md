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
# Hidden Markov Model (HMM)

A probabilistic model with **5 components**:

| Component | Symbol | Meaning |
|-----------|--------|---------|
| Hidden states | Q = {q₁, …, qN} | Unobserved biological states (e.g., exon, intron, intergenic) |
| Observable alphabet | Σ | Observed symbols (e.g., nucleotides A, C, G, T) |
| Transition matrix | A = {aᵢⱼ} | P(state j at t+1 \| state i at t) |
| Emission matrix | B = {bᵢ(k)} | P(observing symbol k \| being in state i) |
| Initial distribution | π = {πᵢ} | P(starting in state i) |

**Three fundamental problems**:

| Problem | Question | Algorithm |
|---------|----------|-----------|
| **Evaluation** | P(sequence \| model) | Forward algorithm |
| **Decoding** | Most likely state path | Viterbi algorithm |
| **Learning** | Estimate A, B, π from data | Baum-Welch (EM) |

In gene finding, hidden states = biological annotations (exon, intron, intergenic); observed symbols = DNA nucleotides. The Viterbi path gives the complete gene annotation in one pass.

See [[hidden-markov-models]], [[Viterbi algorithm]], [[Baum-Welch algorithm]], [[Forward algorithm]].
