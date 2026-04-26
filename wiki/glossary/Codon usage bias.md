---
tags:
  - __CONCEPT
  - Module1
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
# Codon usage bias

The non-uniform use of synonymous codons (codons encoding the same amino acid) in a genome. Most amino acids are encoded by 2–6 synonymous codons, but organisms preferentially use a subset of them.

**Why it exists**: preferred codons match the most abundant tRNA species, increasing translational speed and accuracy. Bias is organism- and tissue-specific, and varies between highly expressed and lowly expressed genes.

**Role in gene prediction**: coding regions show a distinct codon usage signature relative to non-coding DNA. [[content-sensors|Content sensors]] — particularly the **5th-order, 3-periodic inhomogeneous Markov model** — exploit this bias to distinguish exons from introns and intergenic regions.

**3-periodic structure**: the three codon positions have very different nucleotide compositions. Position 3 (the wobble position) is the most degenerate. Three separate Markov chains — one per codon position — capture this periodicity. See [[content-sensors]].

**Also relevant to**: recombinant protein production (codon-optimized synthetic genes) and evolutionary analysis (dN/dS ratios).

# TLDR
Organisms prefer certain synonymous codons over others; coding regions have a distinctive preference signature that gene finders exploit to tell exons from non-coding sequence.
