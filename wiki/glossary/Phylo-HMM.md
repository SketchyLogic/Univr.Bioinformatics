---
tags:
  - __DEFINITION
  - Module1
---
# Phylo-HMM

A [[Hidden Markov Model (HMM)]] that jointly models **gene structure** and **evolutionary history** along a phylogenetic tree of multiple aligned genomes.

**Key idea**: at each genomic position, a nucleotide substitution model (e.g., HKY) governs how the sequence evolved from an ancestral state along the tree. Coding and non-coding regions evolve at different rates (coding is more conserved). The Phylo-HMM therefore uses evolutionary conservation as an **additional orthogonal signal** for gene prediction, on top of intrinsic sequence features.

**Advantage over single-genome GHMM**: detects genes that lack strong intrinsic signals (e.g., GC-poor genomes, short exons) by exploiting multi-species conservation.

**Implementations**: TWINSCAN (pairwise informant genome), N-SCAN (multi-genome), SLAM, CONTRAST.

See [[hidden-markov-models]], [[evolutionary-conservation]], [[gene-prediction-tools]].
