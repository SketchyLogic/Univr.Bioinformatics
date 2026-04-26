---
tags:
  - __DEFINITION
  - Module3
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
# Ortholog

A gene in one species that is evolutionarily related to a gene in another species by **vertical descent** (a speciation event), not by gene duplication. Orthologs typically retain the **same function** across species.

**Contrast with [[Paralog]]**: paralogs arise from gene duplication within a genome and often diverge in function.

**Why orthologs matter for AAS prediction**: [[SIFT algorithm|SIFT]] and similar tools build multiple sequence alignments from orthologs (not paralogs) because:
- Orthologs are under selection to maintain the same function, so conserved positions reflect functional importance.
- Including paralogs introduces spurious variation: a position variable across paralogs (different functions) may be essential in the query protein, leading to false "tolerated" predictions.
- Using orthologs instead of mixed homologs improves SIFT accuracy by ~8%.

**Example**: β-globin in human, mouse, and zebrafish are orthologs — aligned positions reflect conservation required for O₂ transport function.

See [[amino-acid-substitutions]], [[evolutionary-conservation]], [[SIFT algorithm]].
