---
tags:
  - __CONCEPT
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

# Homology

Two sequences are **homologous** if they descend from a common ancestral sequence. Homology is a statement about evolutionary history — it is binary (sequences either share an ancestor or they do not), not a matter of degree.

## Common misuse

"Percent homology" is technically incorrect. What is measurable is **percent sequence identity** or **percent similarity**. High sequence identity is *evidence* for homology, but homology itself is not a percentage.

## Types of homologs

| Type | Definition | Cause |
|------|-----------|-------|
| **[[Ortholog]]** | Homologs in different species that diverged by speciation | A single ancestral gene, one copy per lineage |
| **[[Paralog]]** | Homologs within the same genome that diverged by duplication | Gene duplication event |
| **Xenolog** | Homologs acquired by horizontal gene transfer | Transfer between organisms, not vertical inheritance |

Orthologs tend to retain the same function; paralogs often diverge in function after duplication.

# TLDR

Homology = shared evolutionary ancestry. In bioinformatics it is detected via sequence similarity but is not the same thing as similarity. Orthologs share function across species; paralogs diverged after duplication within a genome.
