---
tags:
  - __EXECUTABLE
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

**Strategy**: identify the intersection between the predicted set and the reference set, then apply the Sn/Sp formulas. Decide which evaluation level is being asked (locus, exonic region, or junction).

**Formulas**:

$$Sn = \frac{|i \cap j|}{|j|} \qquad Sp = \frac{|i \cap j|}{|i|} \qquad AC = \frac{Sn + Sp}{2}$$

where $i$ = prediction, $j$ = reference.

**Step-by-step**:
1. Identify $|j|$ — the total size of the reference (e.g., total reference nucleotides, or number of reference junctions)
2. Identify $|i|$ — the total size of the prediction
3. Compute $|i \cap j|$ — the overlap (e.g., nucleotides in both, or junctions found in both)
4. Apply the formulas

**Worked example** (nucleotide level — exonic regions):

Suppose:
- Reference exon set $j$ spans 250 nucleotides
- Predicted exon set $i$ spans 300 nucleotides
- Overlap $|i \cap j|$ = 200 nucleotides

$$Sn = \frac{200}{250} = 0.80 \qquad Sp = \frac{200}{300} = 0.67 \qquad AC = \frac{0.80 + 0.67}{2} = 0.735$$

**Common mistakes**:
- Confusing which denominator goes with Sn vs. Sp. Mnemonic: **Sn uses the reference** (how much of truth is recovered?); **Sp uses the prediction** (how much of the prediction is correct?).
- Using only one metric: a predictor that predicts the entire genome as coding achieves Sn = 1 but Sp ≈ 0.

See [[Sensitivity and Specificity in gene prediction]] and [[Annotation accuracy evaluation levels]].
