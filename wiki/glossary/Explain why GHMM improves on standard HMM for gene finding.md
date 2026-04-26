---
tags:
  - __EXECUTABLE
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
# Explain why GHMM improves on standard HMM for gene finding

**The problem with standard HMMs**: state durations follow a **geometric distribution** (a consequence of the Markov property: P(leave state at t+1) = constant). In gene finding, this predicts exponentially distributed exon and intron lengths.

**Why this is biologically wrong**:
- Real human exons cluster around **100–300 nt** — a geometric distribution greatly overestimates the probability of very short or very long exons.
- Intron lengths follow a different (log-normal-like) distribution, with a minimum ~60 nt and a long tail.
- Geometric duration modeling leads to fragmented exon predictions and missed long introns.

**What the [[Generalized Hidden Markov Model (GHMM)|GHMM]] adds**: on entering a state, explicitly draw a duration d from a state-specific distribution D_q (Poisson, empirical histogram, etc.), then emit exactly d nucleotides. This captures realistic length distributions.

**Trade-off**: the Viterbi recurrence must iterate over all possible durations at each position, increasing time from O(N²T) to O(N²T²) in the worst case. In practice this is handled by capping the maximum allowed duration.

**Summary**: GHMM = HMM + explicit length distributions. Used in GENSCAN, AUGUSTUS, and most state-of-the-art eukaryotic gene finders.

See [[hidden-markov-models]], [[Generalized Hidden Markov Model (GHMM)]], [[genscan]].
