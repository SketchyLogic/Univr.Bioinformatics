---
tags:
  - __DEFINITION
  - Module2
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
# E-value (Expect value)

A statistical measure used in sequence database searches (BLAST, HMMER, HHpred) that gives the **expected number of alignments with a score ≥ S arising by chance** when searching a database of a given size.

**Formula**: E = K × m × n × e^(−λS), where m is query length, n is database size, and K, λ are scoring-system constants derived from the substitution matrix and gap penalties.

**Interpretation**:

| E-value | Meaning |
|---------|---------|
| 1e-50 | Essentially impossible by chance — highly significant |
| 1e-5 | Very likely significant |
| 0.001 | Commonly used cutoff (1 false hit per 1,000 searches) |
| 10 | 10 false positives expected — not significant |

**Practical thresholds**:
- Sequence homology: E < 0.001 (conservative) or E < 1e-6 (strict)
- Homology modeling template acceptance: E < 1e-20 recommended for safe zone

**Important**: E-value depends on database size — the same score gives a smaller E-value (more significant) in a smaller database.

See [[sequence-search-tools]], [[sequence-alignment]].

# TLDR
The number of false hits you'd expect by chance in a database search. Lower is better; E < 0.001 is the common significance cutoff.
