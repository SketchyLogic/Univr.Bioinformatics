---
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
# Gene Prediction Tools

**Summary**: A reference page for the major computational gene-finding programs, organised by methodology — from exon-chaining tools to HMM-based predictors, combiners, and RNA-based aligners.

**Sources**: [[2.1.gene_prediction_v15.pdf]]

**Last updated**: 2026-04-24

---

## Ab initio / de novo predictors

### [[genscan|GENSCAN]] (Burge & Karlin, 1997)
The landmark GHMM gene finder. Uses a Generalized HMM with:
- MDD (Maximal Dependence Decomposition) for donor site
- Standard Markov chain for acceptor site
- 5th-order inhomogeneous Markov model for coding content
- Geometric distribution for intron length (approximation)

Trained on human sequence; widely used as the baseline for eukaryotic prediction.

### AUGUSTUS (Stanke et al., 2006)
A GHMM-based predictor that models short introns explicitly and uses a geometric distribution for long introns. Supports extrinsic hints (RNA-seq, protein alignments) that can guide but not override the probabilistic model.

### GeneID (Guigó et al., 1992; Parra et al., 2000)
Uses an **exon-chaining** approach:
1. Predict and score candidate exons using splice site scores and 5th-order Markov content
2. Chain exons via dynamic programming to maximise the sum of exon scores

GeneID is fast (analyses large mammalian genomes in hours) and flexible (exons can be re-scored with extrinsic evidence). Limitation: exon/intron length distributions not explicitly modelled.

### GLIMMER (Salzberg et al., 1998)
Prokaryotic gene finder using **Interpolated Markov Models (IMM)** — blends Markov models of different orders depending on available training data. Accuracy >90% Sn/Sp for bacteria.

### GeneMark (Borodovsky & McIninch, 1993)
Pioneered the 3-periodic Markov model for exon recognition; widely used for prokaryotes and now eukaryotes (GeneMark-ES for self-training).

---

## Multi-genome / comparative predictors

### TWINSCAN / N-SCAN (Korf et al., 2001; Gross & Brent, 2006)
- TWINSCAN: modified GENSCAN using BLAST alignments to a single informant genome to modify exon coding scores.
- N-SCAN: phylo-HMM version using alignments to 27 genomes.

### SGP2 (Parra et al., 2003)
Uses BLAST scores to directly modify log-odds that a candidate exon is coding. Simple but effective comparative approach.

### CONTRAST (Gross et al., 2007)
A semi-Markov CRF that is "phylogeny-free" — works directly from features extracted from whole-genome multiple alignments. No need to assume a tree structure.

### SLAM / TWAIN (Alexandersson et al., 2003; Majoros et al., 2005)
Generalized Pair HMMs that simultaneously annotate and align two syntenic genomic sequences.

---

## Discriminative / machine learning approaches

### mSplicer / mGene (Rätsch et al., 2007)
SVM-based gene predictor: SVMs score signal and content sub-models; scores are combined with segment-length contributions and solved by dynamic programming (semi-Markov SVM).

### CRAIG (Bernal et al., 2007)
Semi-Markov CRF trained with an online large-margin multiclass SVM algorithm.

### CONRAD (DeCaprio et al., 2007)
Generic semi-Markov CRF gene calling engine; highly customisable.

---

## Spliced alignment tools (extrinsic)

| Tool | Purpose |
|------|---------|
| BLAST | Rough homology location; not splice-aware |
| BLAT (Kent, 2002) | Fast spliced alignment of cDNA/ESTs |
| GMAP (Wu & Watanabe, 2005) | High-accuracy cDNA-to-genome alignment |
| Exonerate (Slater & Birney, 2005) | General pairwise alignment with intron models |
| Genewise (Birney & Durbin, 2000) | Protein-to-genome alignment |
| sim4 (Florea et al., 1998) | EST-to-genome spliced alignment |

---

## Combiners

| Tool | Notes |
|------|-------|
| GLEAN (Elsik et al., 2007) | Widely used in genome projects; combines multiple gene callers |
| EuGène (Foissac & Schiex, 2005) | Integrates many evidence types via a flexible scoring framework |
| GAZE (Howe et al., 2002) | Evidence-directed annotation |
| Jigsaw (Allen & Salzberg, 2005) | Decision-tree based combiner |
| Genomix (Coghlan & Durbin, 2007) | Graph-based |

General principle: combiners perform better than any individual input because independent predictors make partially uncorrelated errors.

---

## Annotation pipelines

| Pipeline | Organisation | Approach |
|----------|-------------|----------|
| ENSEMBL | EBI/Sanger | Stepwise: protein homology → spliced alignment → ab initio |
| UCSC Genes | UCSC | mRNA/EST alignment + RefSeq |

---

## Related pages

- [[gene-prediction]]
- [[hidden-markov-models]]
- [[viterbi-algorithm]]
- [[extrinsic-vs-intrinsic-information]]
- [[evolutionary-conservation]]
- [[genscan]]
- [[sequence-search-tools]]

## Other sources

## Test yourself

**Q**: What is the difference between GENSCAN and AUGUSTUS?
**A**: Both are GHMM-based gene finders. AUGUSTUS extends GENSCAN's framework by supporting extrinsic evidence hints (RNA-seq, protein alignments) and models short intron lengths explicitly rather than using a purely geometric distribution.

**Q**: What does an exon-chaining approach do differently from an HMM approach?
**A**: Exon-chaining (e.g., GeneID) explicitly enumerates candidate exons, scores each independently, then assembles them into a gene via dynamic programming to maximise the sum of scores. An HMM integrates signal, content, and length modelling into a single probabilistic framework, making all decisions jointly rather than in stages.

**Q**: Why do combiners generally outperform individual gene finders?
**A**: Different predictors make partially uncorrelated errors (different training data, different methods). A combiner that merges their outputs benefits from a higher signal-to-noise ratio, typically improving specificity substantially.
