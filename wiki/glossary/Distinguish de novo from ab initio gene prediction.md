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
# Distinguish de novo from ab initio gene prediction

These terms are often used interchangeably but have distinct precise meanings:

| Term | Strict meaning |
|------|----------------|
| **Ab initio** | Prediction from sequence alone, using only computational models — no external biological evidence (no ESTs, no cDNA, no protein homology) |
| **De novo** | Prediction on a **newly sequenced genome** where no labelled training data exists for that species; requires unsupervised parameter estimation |

**Key distinction**: all de novo predictions are ab initio, but not all ab initio predictions are de novo. A tool trained on annotated human data and applied to human sequence is ab initio but not de novo.

**Practical implication**: GENSCAN trained on human data cannot be directly applied to Drosophila — codon usage, exon/intron length distributions, and signal sequences all differ. De novo tools like **GeneMark-ES** avoid this by self-training on the target genome using the **Baum-Welch algorithm** (unsupervised EM).

**Exam tip**: if asked whether it is possible to use a gene finder trained on one species on a different species, the answer is generally no — gene finders must be trained per species or retrained on the target genome.

See [[extrinsic-vs-intrinsic-information]], [[gene-prediction]], [[Baum-Welch algorithm]].
