---
tags:
  - __DEFINITION
  - Module1
CreatedAt: 2026-04-27
LastUpdateAt: 2026-04-27
LastReviewAt: null
ReviewerIds:
  - admin
OwnerIds:
  - admin
IssueNotes: null
GeneratedBy: claude-sonnet-4-6
---
# Definition

A **related species' genome** aligned to the target genome to supply evolutionary conservation evidence for gene prediction. Because coding sequences evolve more slowly than non-coding regions (purifying selection removes deleterious mutations), regions that are conserved between two diverged genomes are enriched for exons.

The informant genome is not the sequence being annotated — it is an auxiliary reference. Its alignments are computed (typically with BLAST) and the resulting conservation pattern is fed into the prediction model as an extra signal, orthogonal[^1] to intrinsic sequence features.

**Usage by tool**:

| Tool | Informant genomes used | How |
|------|------------------------|-----|
| SGP2 | 1 | BLAST score directly modifies exon log-odds |
| TWINSCAN | 1 | Alignments define an 8-symbol extended alphabet; GHMM retrained on it |
| N-SCAN / CONTRAST | up to 27 | Phylo-HMM models full evolutionary history across the tree |

**Taxonomic distance matters**: the informant should be close enough that homologous genes can be aligned, but distant enough that neutral (non-coding) sequence has diverged. Mouse is a common informant for human gene prediction.

Methods that use an informant genome are still classified as **de novo** (no experimental evidence), but are *not* **ab initio**, which denotes the stricter case of no informant genome at all.

# TLDR

An informant genome is a related-species genome whose alignment to the target genome reveals which positions are conserved — and therefore likely coding.

See [[evolutionary-conservation]], [[extrinsic-vs-intrinsic-information]], [[gene-prediction-tools]].

[^1]: *Orthogonal* here means statistically independent in origin: conservation evidence comes from comparing two genomes across species, while intrinsic signals (codon bias, splice-site weight matrices, etc.) come from the sequence of the target genome alone. Because their errors are uncorrelated, combining them improves prediction accuracy more than stacking two signals derived from the same source would.
