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
# Maximal Dependence Decomposition (MDD)

A decision-tree method for modeling sequence signals that captures **non-adjacent position dependencies**. Used in [[genscan|GENSCAN]] for the donor splice site model.

**How it works**:
1. Find the position most mutually dependent on all others (by χ² test or mutual information).
2. Partition the aligned training sequences by the nucleotide at that position.
3. Build a [[Weight Array Model (WAM)]] for each partition.
4. Recurse on each sub-partition until too few examples remain (fall back to a full [[Position Weight Matrix (PWM)]]).

The result is a **tree of WAMs**, each specialised to a subset of sequences sharing the same nucleotide at the most informative positions.

**Advantage over PWM / WAM**: captures long-range, non-adjacent correlations at the cost of requiring larger training sets.

See [[signal-sensors]], [[genscan]].
