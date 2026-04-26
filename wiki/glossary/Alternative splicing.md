---
tags:
  - __CONCEPT
  - Module1
depth: -1
prerequisites:
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
# Alternative splicing

The process by which different combinations of exons from a single pre-mRNA transcript are joined to produce multiple distinct mRNA **isoforms**. A single gene can thus encode multiple protein variants with different functions, localizations, or regulation.

**Major types**:
- **Exon skipping**: one or more internal exons are omitted — the most common type in vertebrates
- **Alternative 5′/3′ splice site**: different donor or acceptor sites within an exon/intron boundary
- **Intron retention**: an intron is included in the mature mRNA
- **Mutually exclusive exons**: exactly one of two adjacent exons is included

**Scale**: ~95% of human multi-exon genes undergo alternative splicing; a single gene can produce hundreds of isoforms (e.g., Dscam in Drosophila: >38,000 isoforms).

**Implication for gene prediction**: standard ab initio tools predict a **single best transcript** per locus. Accurate isoform-level annotation requires [[extrinsic-vs-intrinsic-information|RNA-seq data]] and specialized tools (e.g., StringTie, AUGUSTUS with hints). See [[gene-prediction-tools]].

# TLDR
One gene, many proteins: by mixing and matching exons, a single genomic locus can produce dozens or hundreds of different mRNA isoforms. ~95% of human multi-exon genes do this.
