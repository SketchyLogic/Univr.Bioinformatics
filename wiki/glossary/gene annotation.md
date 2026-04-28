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
# Gene annotation

The process of identifying the location, boundaries, and biological function of genes in a genome sequence.

**What it produces**: for each gene, a record of its chromosomal coordinates, exon–intron structure, transcript isoforms, coding sequence, and (where known) functional role (protein function, pathway membership, disease association).

**Why it is done**: a raw genome sequence is just nucleotides. Annotation converts it into a usable map. Without it, there is no way to know which stretches encode proteins, where transcription starts and ends, or how many genes exist. Downstream analyses — comparative genomics, drug target identification, variant interpretation, RNA-seq quantification — all depend on a reliable annotation.

**How it is produced**: through a combination of [[extrinsic-vs-intrinsic-information|extrinsic evidence]] (cDNA alignments, ESTs, RNA-seq, protein homology) and [[extrinsic-vs-intrinsic-information|intrinsic prediction]] (ab initio gene finders). The [[gold standard for gene annotation]] is a full-length cDNA aligned to the genome with canonical splice sites, because it requires no inference.

# TLDR

Gene annotation is the labelling of a genome sequence — marking where genes are, what their structure is, and what they do.
