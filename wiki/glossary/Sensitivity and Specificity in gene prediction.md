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

The standard pair of metrics used to evaluate the accuracy of a gene predictor against a reference (gold-standard) annotation.

Let $i$ = predicted set, $j$ = reference set, $|i \cap j|$ = their intersection (overlapping nucleotides/features).

$$Sn = \frac{|i \cap j|}{|j|} = \frac{TP}{TP + FN}$$

$$Sp = \frac{|i \cap j|}{|i|} = \frac{TP}{TP + FP}$$

$$AC = \frac{Sn + Sp}{2}$$

- **Sensitivity (Sn)** — what fraction of the reference is recovered by the predictor? A predictor that predicts everything coding has Sn = 1 but very low Sp.
- **Specificity (Sp)** — what fraction of the prediction is actually correct? A predictor that predicts very few, very precise genes has high Sp but low Sn.
- **Accuracy (AC)** — the arithmetic mean; the single number used to compare predictors overall.

### Three evaluation levels

These metrics are computed at three levels of resolution (see [[Annotation accuracy evaluation levels]]):

1. **Gene locus** — coarse: is the gene locus detected at all?
2. **Exonic regions** — nucleotide-level: are exon/intron boundaries correct?
3. **Exon-intron junctions** — exact splice site coordinates

A predictor should be evaluated at all three levels; performance can differ substantially across them.

# TLDR
$Sn$ = fraction of reference recovered; $Sp$ = fraction of prediction that is correct; $AC = (Sn + Sp) / 2$.
