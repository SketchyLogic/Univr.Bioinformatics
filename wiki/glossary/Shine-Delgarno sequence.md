---
tags:
  - __DEFINITION
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
# Shine-Dalgarno sequence

A purine-rich sequence in the **5' UTR of prokaryotic mRNA**, located ~5–10 nucleotides upstream of the start codon (AUG). It base-pairs with the complementary anti-Shine-Dalgarno sequence at the 3' end of the **16S rRNA** of the small ribosomal subunit (30S), positioning the ribosome correctly over the start codon to initiate translation.

**Consensus**: `5'–AGGAGG–3'` (or partial matches thereof).

**Why it matters for gene prediction**: the presence of a Shine-Dalgarno sequence is a strong signal that an AUG immediately downstream is a genuine translation start site, not a spurious in-frame ATG. Prokaryotic gene finders (GLIMMER, GeneMark) use it as a [[signal-sensors|signal sensor]] to score candidate start codons. Because prokaryotic genomes are ~85–90% coding and genes are uninterrupted ORFs, combining Shine-Dalgarno detection with ORF length and codon bias achieves >90% accuracy.

**Not found in eukaryotes**: eukaryotic ribosomes use the cap-dependent scanning mechanism (Kozak sequence) instead. See [[eukaryotic-gene-structure]] for the contrast.