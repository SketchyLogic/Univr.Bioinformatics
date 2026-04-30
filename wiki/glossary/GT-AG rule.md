---
tags:
  - __DEFINITION
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
# TLDR

In euk most introns that are spliced out start with GT & ends with AG
# Mnemonic

**G**ood**T**imes - **A**nd**G**oodbyes
# GT-AG rule

The canonical dinucleotides found at the boundaries of virtually all spliceosomal introns in eukaryotes:

- **Donor site** (5′ end of intron): **GT** (GU in RNA)
- **Acceptor site** (3′ end of intron): **AG**

Full consensus: `exon | GT … intron … AG | exon`

**Role in gene prediction**: the GT-AG rule provides a **necessary but not sufficient** filter. Only GT…AG pairs are considered as candidate introns. Alone it generates far too many false positives (GT and AG occur very frequently by chance); it must be combined with [[signal-sensors|full splice site models]] (PWM, WAM, MDD) and [[content-sensors|content sensors]] to score and rank candidates.

**Exception**: U12-type (AT-AC) introns constitute ~1% of human introns and use AT…AC boundaries instead.

See [[eukaryotic-gene-structure]], [[signal-sensors]].