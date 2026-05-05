---
tags:
  - __DEFINITION
  - Module1
CreatedAt: 2026-05-02
LastUpdateAt: 2026-05-02
LastReviewAt: null
ReviewerIds:
  - admin
OwnerIds:
  - admin
IssueNotes: null
GeneratedById: claude-sonnet-4-6
---

Also simply called **gene annotation**. The process of defining, within a genome sequence, the exact:

1. **Localization** of each gene (chromosome, strand, start and end coordinates)
2. **Structure** of each gene — the exon-intron organisation, the CDS (from ATG start to stop codon), and the UTR regions (5′ and 3′)
3. **Alternative transcripts** — the set of splice variants produced by the gene

Structural annotation answers the question *where are the genes and how are they built?* It does not assign biological function (that is [[Functional annotation]]).

The output is typically a [[GFF3 format]] file listing `gene`, `transcript`, `exon`, and `CDS` features.

Structural annotation relies on:
- Alignment of experimental evidence (cDNA, [[Expressed Sequence Tag (EST)]], [[RNA-Seq]], homologous proteins) to the genome
- *Ab initio* gene prediction using [[signal-sensors]] and [[content-sensors]]
- Hybrid and comparative approaches

See [[genome-annotation-pipeline]] for the full workflow.
