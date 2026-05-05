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

**PASA (Program to Assemble Spliced Alignments)** — an automated pipeline focused on aligning transcript evidence (ESTs, full-length cDNA, RNA-Seq assemblies) to a genome and assembling them into gene models. Particularly strong at defining UTR boundaries and detecting alternative splice forms.

**What PASA does**:
1. Aligns transcripts/ESTs to the genome using spliced aligners (GMAP, BLAT)
2. Assembles overlapping alignments into transcript assembly clusters
3. Identifies alternative splicing events (exon skipping, alternative donors/acceptors, retained introns)
4. Produces [[GFF3 format]] models including UTR annotations

**Strength**: excellent UTR modelling and alternative transcript detection from transcript evidence.

**Limitation**: relies entirely on experimental evidence coverage; genes not covered by transcripts will be missed.

Often combined with *ab initio* results (e.g., from AUGUSTUS or [[MAKER annotation pipeline]]) and a final integrator such as [[Evidence Modeller (EVM)]].
