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

An automated genome annotation pipeline that integrates *ab initio* gene prediction, EST/protein alignment, and repeat masking in a single configurable workflow. Widely used for annotating newly sequenced eukaryotic genomes.

**What MAKER does**:
1. Runs a repeat masker to soft-mask transposable elements
2. Aligns EST and protein evidence to the genome
3. Runs one or more *ab initio* predictors (e.g., SNAP, AUGUSTUS)
4. Uses [[Evidence Modeller (EVM)]]-like logic to produce a consensus annotation
5. Outputs [[GFF3 format]] annotation files

**Advantage**: relatively simple to configure and run for a new genome.

**Disadvantage**: limited visibility into intermediate steps; automatic decisions may not be optimal for all organism types (see [[PASA annotation pipeline]] for transcript-focused alternative).

See [[genome-annotation-pipeline]] for context on how automated pipelines fit into the full annotation workflow.
