---
tags:
  - __CONCEPT
  - GenePrediction
CreatedAt: 2026-04-27
LastUpdateAt: 2026-04-28
LastReviewAt: null
ReviewerIds:
  - admin
OwnerIds:
  - admin
IssueNotes: null
GeneratedBy: claude-sonnet-4-6
---

The **gold standard** for gene annotation is a **full-length cDNA sequence that has been aligned to the genome and whose intron boundaries land on canonical splice sites**.

Each term carries weight:

| Term                       | What it means                                                                                                                                                                                                                                                 |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Full-length cDNA**       | The cDNA was synthesised from a complete mRNA molecule (5′ cap to poly-A tail). Both the start and end of the transcript are captured, so the 5′ UTR, coding sequence, and 3′ UTR boundaries are all known.                                                   |
| **Aligned to the genome**  | A spliced aligner maps the cDNA back to the genomic sequence. Every gap in the alignment corresponds to an intron that was spliced out during mRNA processing.                                                                                                |
| **Canonical splice sites** | The first two bases of each intron are GT (donor site) and the last two are AG (acceptor site). This GT–AG rule holds for >99 % of eukaryotic introns. When a gap lands exactly on GT…AG, it is almost certainly a real intron and not an alignment artefact. |

Because all three conditions are met, the exon coordinates can be read directly off the alignment — **no computational inference is required**[^inference]. This makes the evidence effectively ground truth, which is why it is called the gold standard.

[^inference]: **What inference would otherwise be needed**: without a cDNA, a gene finder must *predict* where exons start and stop by scoring statistical signals (splice site models, codon usage, ORF length) and running a dynamic-programming decoder like Viterbi over millions of candidate positions. Each of those steps introduces uncertainty — a predicted splice site may be a false positive, a predicted ATG may not be the real start. With a full-length cDNA alignment, all of that is bypassed: the exon boundaries are wherever the aligner placed the gaps, and the GT–AG check is just a sanity filter confirming the gaps are real introns. The annotation is read off the experimental data, not computed from sequence statistics.
## Why it matters in practice

Most gene prediction pipelines use cDNA alignments as anchors. When a full-length cDNA is available for a locus, the annotation for that gene is considered reliable. For loci where only partial evidence exists (ESTs, RNA-seq reads, protein homology), the annotation is necessarily less certain and must be supplemented by [[signal-sensors]] and [[content-sensors]].

## Limitation: identical exon sequences

The gold standard assumes the cDNA can be placed unambiguously on the genome. This fails when two or more exons share the same sequence. Consider a gene with two exons (x1, x2) separated by an intron, where x1 and x2 are sequence-identical. If only one copy of that sequence appears in the mature mRNA (i.e. one exon is alternatively skipped), the cDNA carries a single copy of x and the aligner faces a tie: x1 and x2 are equally valid placements.

The full-length cDNA partially rescues this because the aligner places the *entire* cDNA — the unique 5′ UTR and 3′ UTR sequences anchor the alignment and the position of x falls out as a consequence. However, if the flanking context is also duplicated (e.g. the gene sits in a segmental duplication), the ambiguity is genuine and the annotation is unreliable.

In such cases, additional evidence is needed to break the symmetry:
This is a real problem in repeat-rich genomes and a reminder that the gold standard is necessary but not always sufficient.

# TLDR

A full-length cDNA aligned to the genome with GT–AG intron boundaries gives exon coordinates directly from the experiment, requiring no computational guesswork.
