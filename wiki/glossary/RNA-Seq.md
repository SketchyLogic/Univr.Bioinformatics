---
tags:
  - __DEFINITION
  - Module0
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

Short reads (50–150 bp) obtained by shotgun sequencing of an entire transcriptome — that is, by reverse-transcribing all RNA present in a cell at a specific moment to cDNA, fragmenting it, and sequencing the fragments with [[NGS (Next Generation Sequencing)]] technology.

**Workflow**:
1. Isolate all mRNA from a tissue/condition
2. Reverse-transcribe to cDNA
3. Fragment and sequence with NGS → millions of 50–150 bp reads
4. Align reads to reference genome (reads spanning a splice site are split across the intron) **or** assemble transcripts *de novo*

**Why it is a very powerful experimental evidence for splice junction prediction**:
A read that spans an exon-intron boundary is split when aligned to genomic DNA — one part maps to the upstream exon, the other to the downstream exon, with the intron sequence skipped. This directly and precisely reveals the exact splice junction coordinates.

```
Genome:  [EXON1]----[INTRON]----[EXON2]
                                        
Read:    [=====]                [========]
           ↑                      ↑
        maps here              maps here
        (no intron in the read itself)
```

>[!hint]
>RNA-Seq starts from mRNA, this implies the introns has been already spliced and exons joined.

In the *Vitis vinifera* case study (lecture 1), RNA-Seq achieved junction-level accuracy AC = 0.91, far above EST (AC = 0.52) and *ab initio* predictors.

**Contrast with [[Expressed Sequence Tag (EST)]]**: ESTs are 400–800 bp partial cDNA fragments from older technology; RNA-Seq reads are shorter (50–150 bp) but produced in vastly larger quantities and at much lower cost, making them the current standard for transcriptome-based annotation evidence.

# TLDR
Shotgun sequencing of the whole transcriptome; reads spanning splice junctions directly map intron boundaries with high accuracy.
