---
tags:
  - __DEFINITION
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

# TATA box

A conserved promoter element with consensus sequence **TATAAA** located approximately **25–30 bp upstream of the transcription start site (TSS)** in eukaryotic protein-coding genes. It is the primary binding site for the **TATA-binding protein (TBP)**, a subunit of the general transcription factor TFIID, which initiates assembly of the RNA Polymerase II pre-initiation complex.

## Role in transcription

1. TBP binds the TATA box and bends the DNA ~80°.
2. Other general transcription factors (TFIIA, TFIIB, …) assemble around TBP.
3. RNA Pol II is recruited and positioned at the TSS.
4. Transcription initiates.

The TATA box does not encode a protein — it is a *regulatory signal* in the DNA that positions the transcription machinery.

## Relevance to gene prediction

The TATA box is one of the [[signal-sensors]] used by ab initio gene finders to identify candidate promoters and TSS positions. However:

- Only ~24 % of human promoters contain a canonical TATA box; most use TATA-less promoters with other core elements (Initiator, DPE, BREu/BREd).
- The TATAAA hexamer occurs frequently by chance in AT-rich genomic sequence, generating many false positives.
- For these reasons, TATA box detection alone is a weak predictor of gene starts and is always combined with other signals.

# TLDR

The TATA box (TATAAA, ~−28 bp from TSS) recruits the transcription machinery via TBP. It is a promoter signal sensor in gene finders, but present in only ~24 % of human genes and prone to false positives.
