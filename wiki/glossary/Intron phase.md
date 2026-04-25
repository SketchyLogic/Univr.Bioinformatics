---
tags:
  - __DEFINITION
  - Module1
---
# Intron phase

The position within a codon at which an intron interrupts the coding sequence:

| Phase | Intron inserts after... | Consequence |
|-------|------------------------|-------------|
| **0** | 3rd base of a codon | Intron falls between complete codons |
| **1** | 1st base of a codon | Intron splits a codon after position 1 |
| **2** | 2nd base of a codon | Intron splits a codon after position 2 |

**Reading frame conservation**: for the protein reading frame to be preserved after splicing, the **donor phase** of an intron must match the **acceptor phase** required by the downstream exon. Mismatched phases produce frameshifts.

**Role in gene prediction**: [[hidden-markov-models|GHMMs]] and [[genscan|GENSCAN]] model intron phases explicitly as separate HMM states (e.g., "intron-phase-0", "intron-phase-1", "intron-phase-2"), with transition probabilities that enforce valid phase combinations at exon junctions.

See [[eukaryotic-gene-structure]], [[genscan]].
