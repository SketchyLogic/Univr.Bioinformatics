---
tags:
  - __DEFINITION
  - Module0
CreatedAt: 2026-05-02
LastUpdateAt: 2026-05-03
LastReviewAt: null
ReviewerIds:
  - admin
OwnerIds:
  - admin
IssueNotes: null
GeneratedById: claude-sonnet-4-6
---

A statistical approach that scans the entire genome of large numbers of individuals to find genetic variants (typically SNPs) **associated with a trait or disease**.

**Core idea**: Imagine you line up 5,000 sick people and 5,000 healthy people, then look at one specific position in their DNA. At that position, every person has one of two letters — say `A` or `G`. If 80% of sick people have `G` but only 40% of healthy people do, that position is *statistically associated* with the disease. GWAS does this test simultaneously at **millions of positions** across the whole genome and asks the same question at each one: *"Is one letter more common in cases than controls?"* The positions that pass a strict statistical threshold are flagged as associated loci.

> **Terminology note**: at a SNP, the word *allele* just means *"which letter you have at this position"* (e.g. `A` or `G`). It does NOT mean a whole gene. "Allele frequency" = how often that single letter appears in the population. The word is borrowed from classical genetics where it referred to gene-level variants, but in GWAS it always refers to a single nucleotide.

**Key steps**:
1. Genotype thousands to millions of SNPs per individual using SNP arrays or whole-genome sequencing
2. Perform a statistical association test (e.g., chi-squared, logistic regression) at each SNP position
3. Apply a stringent significance threshold ($p < 5 \times 10^{-8}$) to correct for multiple testing across the genome
4. Identify associated loci and investigate nearby genes for biological interpretation

**Interpretation caveat**: GWAS identifies *association*, not causation. An associated SNP may be in linkage disequilibrium with the actual causal variant, not causal itself.

**Output**: a Manhattan plot — each dot is a SNP, positioned by chromosomal location (x-axis) and $-\log_{10}(p\text{-value})$ (y-axis); peaks above the significance threshold are GWAS hits.

Applications include complex disease mapping (type 2 diabetes, schizophrenia, height, BMI) and agronomic trait mapping in plants and livestock.

# TLDR
Scan millions of SNPs across thousands of individuals to find genomic positions statistically associated with a trait or disease.
