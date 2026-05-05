---
tags:
  - __CONCEPT
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

Gene prediction accuracy is evaluated at three increasingly stringent levels. A predictor may score well at one level but poorly at another, so all three must be reported.

| Level | What is compared | Question answered |
|-------|-----------------|-------------------|
| **Gene locus** | Whether any predicted feature overlaps the reference gene locus | Does the predictor know a gene exists here? |
| **Exonic regions** | Nucleotide overlap between predicted exons and reference exons | Does the predictor correctly classify each nucleotide as exonic or intronic? |
| **Exon-intron junctions** | Whether each predicted splice site exactly matches a reference splice site | Does the predictor know the precise exon boundaries? |

The junction level is the most informative for downstream use: an annotation that correctly identifies a gene locus but places exon boundaries incorrectly will produce a wrong CDS and a wrong protein sequence.

### Example (from *Vitis vinifera* benchmark)

RNA-Seq alignments scored:
- Locus AC = 0.675 (good)
- Exon region AC = 0.687 (good)
- Junction AC = **0.912** (excellent — reads directly span junctions)

SNAP *ab initio* scored:
- Locus AC = 0.497
- Exon region AC = 0.607
- Junction AC = 0.519

Metrics: [[Sensitivity and Specificity in gene prediction]].
