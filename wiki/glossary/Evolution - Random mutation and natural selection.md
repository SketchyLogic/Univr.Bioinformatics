---
tags:
  - __CONCEPT
CreatedAt: 2026-04-24
LastUpdateAt: 2026-04-24
LastReviewAt: null
ReviewerIds:
  - admin
OwnerIds:
  - admin
IssueNotes: null
GeneratedById: claude-sonnet-4-6
---
# Evolution: random mutation and natural selection

Evolution proceeds through two coupled mechanisms:

**1. Random mutation** — errors in DNA replication, chemical damage, radiation, and mobile elements continuously introduce new variants into a population. Mutations are random with respect to fitness: they do not arise because they would be beneficial.

**2. Natural selection** — individuals whose variants improve reproductive success leave more offspring; their alleles increase in frequency. Three modes:

| Mode | Effect on mutation | Outcome |
|------|--------------------|---------|
| **Purifying (negative) selection** | Removes harmful mutations | Functional sequences stay conserved across species |
| **Positive (directional) selection** | Promotes beneficial mutations | Rapid change at adaptive sites |
| **Neutral drift** | Acts on mutations with no fitness effect | Random fixation or loss over time |

**Key consequence for bioinformatics**: purifying selection is why coding sequences and functionally important protein positions are more conserved than non-functional regions across related species. This conservation is the observable signal exploited by [[evolutionary-conservation|comparative gene prediction]] and sequence-based [[amino-acid-substitutions|AAS prediction methods]] like SIFT.

> "If a position has been conserved across millions of years of evolution, a change there is likely to be deleterious." — the core logic of SIFT and similar tools.