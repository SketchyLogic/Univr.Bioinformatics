---
tags:
  - __CONCEPT
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

The computational process of **identifying positions in a genome where the sequenced sample differs from a reference genome**. Variants can be single nucleotide polymorphisms (SNPs), small insertions/deletions (indels), or larger structural variants (SVs).

## Types of variants detected

| Type                                         | Description                                  | Size    |
| -------------------------------------------- | -------------------------------------------- | ------- |
| **[[SNP (Single Nucleotide Polymorphism)]]** | Single base substitution                     | 1 bp    |
| **Indel**                                    | Insertion or deletion                        | 1–50 bp |
| **CNV** (Copy Number Variant)                | Duplicated or deleted chromosomal segments   | kb–Mb   |
| **SV** (Structural Variant)                  | Inversions, translocations, large insertions | > 50 bp |

## How it is done (standard pipeline)

1. **Sequencing**: re-sequence one or more individuals with [[NGS (Next Generation Sequencing)]]
2. **Alignment**: map short reads to the reference genome (tools: BWA, Bowtie2)
3. **Duplicate marking**: remove PCR duplicates that would inflate variant counts
4. **Variant calling**: compare the aligned bases at each position to the reference; flag positions where a significant fraction of reads carries a different base (tools: GATK HaplotypeCaller, FreeBayes, SAMtools)
5. **Filtering**: apply quality filters (read depth, base quality, mapping quality) to remove false positives
6. **Annotation**: link called variants to known genes, regulatory regions, or population databases (dbSNP, gnomAD)

## Output format

Variants are stored in **VCF (Variant Call Format)** — a tab-separated file with one variant per line, recording chromosome, position, reference allele, alternate allele, quality score, and sample genotype.

## Relationship to GWAS and disease

Called variants are the input to [[GWAS (Genome-Wide Association Studies)]] — GWAS asks which of these variants are statistically associated with a trait. Variant calling is also used in cancer genomics (somatic mutations), population genetics, and clinical diagnostics.

# TLDR
Comparing re-sequenced reads to a reference genome to list every position where the sample differs; output is a VCF file of SNPs, indels, and structural variants.
