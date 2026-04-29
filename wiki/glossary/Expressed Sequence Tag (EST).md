---
tags:
  - __CONCEPT
  - Module1
CreatedAt: 2026-04-29
LastUpdateAt: 2026-04-29
LastReviewAt: null
ReviewerIds:
  - admin
OwnerIds:
  - admin
IssueNotes: null
GeneratedBy: claude-sonnet-4-6
---

# Expressed Sequence Tag (EST)

## Definition

A short, single-pass[^1] cDNA sequence (typically 200–800 bp) produced by sequencing one or both ends of a randomly selected cDNA clone from a library. Because the cDNA was derived from mRNA, an EST is direct evidence that a genomic region is transcribed — it "tags" an expressed gene.

ESTs are **partial**: they cover only a fragment of the full transcript (usually the 5′ or 3′ end), so they rarely capture the complete exon–intron structure on their own. Multiple overlapping ESTs from the same gene must be assembled into a consensus to approximate a full-length transcript.

## Why it was relevant

Before high-throughput sequencing, ESTs were the primary large-scale source of transcriptional evidence. Their value:

- **Confirmed gene existence**: an EST proves a locus is transcribed in at least one tissue/condition.
- **Guided gene finders**: EST alignments to the genome anchor exon boundaries more reliably than ab initio prediction alone.
- **Populated databases**: dbEST (NCBI) accumulated >70 million entries across hundreds of species, providing annotation evidence for genomes long before RNA-seq existed.
- **Species breadth**: ESTs were generated for organisms where full genome sequencing was not yet feasible.

## What is replacing them

**RNA-seq** (short-read, e.g. Illumina) has largely replaced EST sequencing because it is cheaper, higher throughput, and quantitative. It provides transcript evidence at genome scale in a single experiment.

**Long-read RNA-seq** (PacBio IsoSeq, Oxford Nanopore cDNA sequencing) goes further: it sequences full-length transcripts in a single read, combining the coverage of RNA-seq with the completeness of the old full-length cDNA approach — effectively becoming the new [[gold standard for gene annotation]].

ESTs remain relevant as a historical archive: the millions of deposited sequences are still used in genome annotation pipelines for species where no RNA-seq data exists.

# TLDR

ESTs are short, partial cDNA sequences used as transcriptional evidence in gene annotation. RNA-seq has replaced them for new experiments, but their database legacy still feeds annotation pipelines.

[^1]: single-pass refers to sequencing method, read the sequence once end to end. Is cheaper that multiple reads.
