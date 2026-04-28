---
tags:
  - __CONCEPT
  - Module1
CreatedAt: 2026-04-27
LastUpdateAt: 2026-04-27
LastReviewAt:
ReviewerIds:
  - admin
OwnerIds:
  - admin
IssueNotes:
GeneratedBy:
---

# Definition

Signal sensors and content sensors each score *local* features independently — a splice site, a hexamer window, a start codon. But a gene has a rigid global structure:

$$5'\text{UTR} \to \text{start} \to \text{exon}_1 \xrightarrow{\text{intron}_1} \text{exon}_2 \to \cdots \to \text{stop} \to 3'\text{UTR}$$

with hard biological constraints: reading frame must be consistent end-to-end, intron phases at adjacent exon boundaries must match, GT-AG rule must hold at every splice site.

The **integration framework** is the algorithm that combines all local scores into the globally best *valid* gene structure. Without it you have a list of candidate signals with scores; with it you get a coherent gene model.

## Frameworks compared

| Framework | Core idea | Example tools |
|-----------|-----------|---------------|
| Exon chaining | Score candidate exons; dynamic programming finds the highest-scoring non-overlapping chain with compatible phases | GeneID, Fgeneh |
| Generalized HMM (GHMM) | Probabilistic state machine; each state is a gene component (exon, intron, UTR…); Viterbi finds the most likely path | GENSCAN, AUGUSTUS |
| Generalized Pair HMM | Simultaneously aligns and annotates two syntenic genomes | SLAM, TWAIN |
| Phylo-HMM | GHMM with evolutionary rate model across a species tree | N-SCAN, SHADOWER |
| Semi-Markov CRF | Like a GHMM but trained discriminatively — directly maximises annotation accuracy | CRAIG, CONTRAST |
| Combiner | Merges predictions from multiple independent tools to reduce uncorrelated errors | GLEAN, EuGène |

The GHMM is the dominant approach: signal and content sub-models are plugged in as emission distributions for each state, and a single Viterbi pass over the chromosome performs integration.

# TLDR

Integration takes independent local scores from sensors and finds the combination that forms the globally best valid gene structure — the algorithm that does this is the integration framework.

See [[gene-prediction]], [[hidden-markov-models]], [[viterbi-algorithm]], [[signal-sensors]], [[content-sensors]].
