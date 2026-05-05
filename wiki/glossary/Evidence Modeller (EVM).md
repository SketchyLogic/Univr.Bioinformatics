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

**EVM (Evidence Modeller / EVidenceModeler)** — a genome annotation combiner that integrates *ab initio* gene predictions and experimental evidence alignments into a single non-redundant set of gene structures by assigning **numerical weights** to each evidence type.

**How it works**:
1. Each input evidence track (EST, protein alignments, each *ab initio* predictor, RNA-Seq models) receives a user-defined integer weight.
2. At each genomic locus, EVM selects the gene model that maximises the sum of weighted support.
3. Experimental evidence consistently receives higher weights than *ab initio* predictions, reflecting its higher reliability.

**Key property**: EVM is a *combiner* (also called an integrator), not a predictor. It does not model the sequence itself; it chooses among pre-computed models.

**Weight scheme example** (from *Vitis vinifera* best annotation):

| Source | Weight |
|--------|--------|
| Homologous proteins | 5 |
| EST alignments | 3 |
| Augustus + RNA-Seq hints | 2 |
| GeneID *ab initio* | 1 |
| SNAP *ab initio* | 1 |

This produced ~26,200 genes with junction-level AC = 0.843.

Related combiners: JIGSAW, GAZE. See [[genome-annotation-pipeline]] and [[Combiner program]].
