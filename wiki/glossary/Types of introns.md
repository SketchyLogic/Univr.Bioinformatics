---
tags:
  - __CONCEPT
  - Module1
CreatedAt: 2026-04-27
LastUpdateAt: 2026-04-27
LastReviewAt: null
ReviewerIds:
  - admin
OwnerIds:
  - admin
IssueNotes: null
GeneratedBy: claude-sonnet-4-6
---

# Types of introns

**Intron**: any non-coding intervening sequence that is transcribed into pre-mRNA (or a precursor RNA) and removed before the mature molecule is used. The word covers mechanistically distinct classes that share only the property of being spliced out.

| Class                       | Removal mechanism                                                                                       | Boundary signals                                              | Where found                                         |
| --------------------------- | ------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------- | --------------------------------------------------- |
| **Spliceosomal — U2-type**  | Major [[Spliceosome]] (U1/U2/U4/U5/U6 snRNPs), two-step transesterification via a lariat intermediate   | GT–AG (>99 %); see [[GT-AG rule]]                             | Nuclear pre-mRNA of virtually all eukaryotes        |
| **Spliceosomal — U12-type** | Minor spliceosome (U11/U12/U4atac/U6atac/U5)                                                            | AT–AC (~0.4 % of human introns)                               | ~700 introns in humans; subset of nuclear genes     |
| **Group I self-splicing**   | Ribozyme (the intron RNA itself); no protein required; guanosine cofactor initiates                     | Conserved internal RNA structure, no simple dinucleotide rule | Mitochondria, chloroplasts, some bacteria and phage |
| **Group II self-splicing**  | Ribozyme via lariat intermediate; mechanistically homologous to the spliceosome (evolutionary ancestor) | Conserved internal RNA structure                              | Mitochondria, chloroplasts, some bacteria           |
| **tRNA introns**            | Splicing endonuclease (cuts) + RNA ligase (joins); no lariat                                            | Specific tRNA fold (not a dinucleotide signal)                | Archaea and eukaryotes; only in tRNA genes          |

## Why the distinction matters for gene prediction

Computational gene finders model **spliceosomal U2-type introns** almost exclusively, because:

1. They dominate eukaryotic nuclear genomes.
2. They leave a predictable molecular footprint: GT–AG boundaries + branch point + polypyrimidine tract, all modellable with [[signal-sensors]] (PWMs, WAMs, MDD).
3. Their removal is required to produce functional mRNA — so every predicted gene structure must respect valid intron boundaries.

Group I/II and tRNA introns occur in organellar or non-protein-coding contexts and are handled by entirely separate tools. When course material or the literature refers to "introns" in the context of gene prediction, it means spliceosomal (U2-type) introns.

## About U12 Introns

 **~700 introns** refers to individual splice sites, not genes — the human genome has ~200,000 U2-type introns total, so U12 introns are a tiny fraction. **Subset of nuclear genes** means two things: (1) U12 introns only occur in nuclear DNA, not in mitochondrial or chloroplast genes; (2) not all nuclear genes have one — they cluster in specific, evolutionarily conserved gene families (e.g. genes involved in RNA processing, DNA replication, vesicle trafficking). A gene that does contain one typically has just that single U12 intron surrounded by normal U2-type introns, so the same pre-mRNA requires both spliceosomal machineries.

# TLDR

All spliceosomal introns are introns, but not all introns are spliceosomal. Gene prediction focuses on spliceosomal U2-type introns because they follow the [[GT-AG rule]] and can be detected computationally.
