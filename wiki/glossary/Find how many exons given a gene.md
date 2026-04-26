---
tags:
  - __EXECUTABLE
  - Module1
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
# Find how many exons given a gene

**Key rule**: `#exons = #introns + 1`

Choose the approach based on what you are given:

**Given a genomic sequence and its mRNA / cDNA**
Align the two. Each contiguous matching block is one exon. Count the blocks.

**Given annotated coordinates (e.g., exon start/end positions)**
Count the exon entries directly.

**Given a gene structure diagram or splice-site positions**
Count GT…AG pairs — each pair brackets one intron. Then apply the key rule.

**Given only the genomic sequence**
1. Scan for canonical donor sites (GT) and acceptor sites (AG).
2. For each candidate intron (GT…AG pair in the correct orientation), check that flanking regions are consistent with exon content (reading frame, codon bias).
3. Count confirmed introns → exons = introns + 1.

**Edge cases to watch**
- A **single-exon gene** has 0 introns → 1 exon.
- **Alternative splicing**: the same gene can yield different exon counts depending on the isoform; specify which transcript you are counting.
- **U12 (AT-AC) introns**: rare (~1% in humans); use AT…AC instead of GT…AG.

See [[eukaryotic-gene-structure]] for the anatomy of splice sites and intron phases.