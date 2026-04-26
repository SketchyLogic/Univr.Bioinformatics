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
# Viterbi algorithm

A **dynamic programming** algorithm that solves the decoding problem for [[Hidden Markov Model (HMM)|HMMs]]: finding the most likely sequence of hidden states given an observed sequence.

**Recurrence**:

```
V_k(i) = max_j [ V_{k-1}(j) × a_{j→i} ] × b_i(x_k)
```

where a_{j→i} is the transition probability from state j to i, and b_i(x_k) is the emission probability of symbol x_k in state i.

**Initialisation**: V₁(i) = πᵢ × bᵢ(x₁)

**Traceback**: a backpointer table stores the argmax at each step, enabling reconstruction of the full optimal state path.

**Why dynamic programming is necessary**: naïvely evaluating all possible state paths takes O(N^T) time (N states, T positions). DP reduces this to O(N² × T) by caching and reusing partial results.

**In gene finding**: the Viterbi path gives the complete exon/intron/intergenic annotation of an entire genomic sequence in a single pass.

See [[viterbi-algorithm]], [[hidden-markov-models]].

# TLDR
Given an observed sequence and an HMM, find the single most likely hidden-state path (e.g., the full exon/intron annotation) in O(N²T) time instead of O(N^T).
