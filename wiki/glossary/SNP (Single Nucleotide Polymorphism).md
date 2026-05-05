---
tags:
  - __DEFINITION
  - Module0
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
> [!Summary]
> - A single-base difference between individuals at a specific genomic position; 
> - It's an SNP rather than a mutation if fixed in at least 1% of population;
> - The most abundant type of genetic variant.

A position in the genome where a **single nucleotide differs between individuals** (or between a sample and a reference genome). The most common type of genetic variant in most species.

Example:
```
Individual A:  ...ACGT[G]TACG...
Individual B:  ...ACGT[A]TACG...
                       ↑
                      SNP
```

> [!warning] **Population criterion**: 
> by convention, a variant is called a SNP (rather than a rare mutation) when the less common allele appears in at least 1% of the population (minor allele frequency ≥ 1%).

**Synonymous vs. nonsynonymous**: when a SNP falls within a coding region, it may be:
- **Synonymous** (silent) — the amino acid is unchanged due to codon degeneracy
- **Nonsynonymous (nsSNP)** — the amino acid changes, potentially affecting protein function (see [[Nonsynonymous SNP (nsSNP)]])

SNPs are the primary input to [[GWAS (Genome-Wide Association Studies)]] and are identified computationally via [[Variant calling]].

> [!Info]
> The human genome contains ~4–5 million SNPs per individual relative to the reference.
