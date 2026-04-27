---
CreatedAt: 2026-04-24
LastUpdateAt: 2026-04-27
LastReviewAt: null
ReviewerIds:
  - admin
OwnerIds:
  - admin
IssueNotes: null
GeneratedById: claude-sonnet-4-6
---
# Gene Prediction

**Summary**: Computational gene prediction is the process of identifying the location and exon-intron structure of genes in a genomic DNA sequence; it is the first step in genome annotation and relies on statistical models of signals and coding content.

**Sources**: [[2.1.gene_prediction_v15.pdf]] · [[Modelli Nascosti di Markov-Gene pred.pdf]]

**Last updated**: 2026-04-24

---

## Why computational gene prediction?

Experimentally characterizing every gene in a genome is prohibitively expensive. Computational prediction is economical and is the starting point for any annotation pipeline. Each prediction is a **hypothesis** to be validated experimentally — the interplay between prediction and experiment drives biological discovery.

The formal problem: **given a DNA sequence (chromosome or genome), identify the precise boundaries and exonic structures of all genes**.

## Prokaryotic vs. eukaryotic difficulty

| Aspect              | Prokaryotes                            | Eukaryotes                                  |
| ------------------- | -------------------------------------- | ------------------------------------------- |
| Gene structure      | Continuous ORF                         | Exons interrupted by introns                |
| Genome size         | Small                                  | Orders of magnitude larger                  |
| % coding            | ~85–90%                                | ~3% (human)                                 |
| Key challenge       | Frame disambiguation, overlapping ORFs | Exon-intron structure, alternative splicing |
| Accuracy achievable | >90% (GLIMMER, GeneMark)               | Much lower; active research area            |

## Two classes of information

Gene prediction methods draw on two broad information classes (see [[extrinsic-vs-intrinsic-information]]):

1. **Extrinsic** — evidence external to the target genome: cDNA, ESTs, protein homology.
2. **Intrinsic "ab initio"** — derived from the target sequence alone: signal sensors + content sensors. No informant genome.
3. **Intrinsic "de novo"** — same as ab initio, but also uses conservation from an [[informant genome]] alignment.

## The prediction pipeline conceptually

```
Genomic sequence
      |
  [Signal sensors] — splice sites, start/stop, promoter, polyA
      +
  [Content sensors] — coding statistics, codon bias
      +
  [Conservation] — alignment to other genomes
      |
  [Integration framework] — exon chaining / HMM / CRF
      |
  Gene models
```

## Frameworks for integration

| Framework              | Key idea                                                 | Example tools          |
| ---------------------- | -------------------------------------------------------- | ---------------------- |
| Exon-chaining          | Score and chain candidate exons via dynamic programming  | GeneID, Fgeneh         |
| Generalized HMM (GHMM) | Probabilistic state machine over gene components         | GENSCAN, AUGUSTUS      |
| Generalized Pair HMM   | Simultaneous alignment + annotation of two genomes       | SLAM, TWAIN            |
| Phylo-HMM              | Models evolutionary history across multiple genomes      | N-SCAN, SHADOWER       |
| Semi-Markov CRF        | Discriminative conditional training on sequence features | CRAIG, CONTRAST        |
| Combiners              | Merge predictions from multiple tools                    | GLEAN, EuGène, Genomix |

Details in [[hidden-markov-models]] and [[gene-prediction-tools]].

## Training and evaluation

Gene prediction programs have separate model and parameter components. Parameters (splice site weight matrices, codon bias models, intron/exon length distributions) must be **trained per species**. Methods include:
- Maximum likelihood estimation from annotated genomes
- Baum-Welch EM for unlabelled data
- Discriminative training (maximising annotation accuracy directly)

Evaluation uses sensitivity (Sn) and specificity (Sp) at the nucleotide, exon, and gene levels:
- **Nucleotide Sn** = correctly predicted coding nucleotides / all true coding nucleotides
- **Exon Sp** = correctly predicted exons / all predicted exons
- **Gene-level** = fraction of complete gene structures correctly predicted end-to-end

## Key tools timeline

| Tool | Method | Year |
|------|--------|------|
| GLIMMER | Interpolated Markov Model | 1998 |
| GENSCAN | GHMM | 1997 |
| AUGUSTUS | GHMM with CRF features | 2006 |
| TWINSCAN/N-SCAN | Phylo-HMM | 2001/2006 |
| GLEAN | Combiner | 2007 |

## Related pages

- [[eukaryotic-gene-structure]]
- [[extrinsic-vs-intrinsic-information]]
- [[signal-sensors]]
- [[content-sensors]]
- [[hidden-markov-models]]
- [[viterbi-algorithm]]
- [[gene-prediction-tools]]
- [[evolutionary-conservation]]

## Other sources

- Burge & Karlin (1997) — original GENSCAN paper
- Stanke et al. (2006) — AUGUSTUS
- Eilbeck et al. (2005) — GFF3 format for annotations

## Test yourself

**Q**: What is the difference between sensitivity and specificity in gene prediction evaluation?
**A**: Sensitivity (recall) measures how many true features are correctly predicted. Specificity (precision) measures how many predictions are actually correct. A good predictor maximises both simultaneously.

**Q**: Why must gene prediction programs be trained per species?
**A**: Because the parameters (splice site sequences, codon bias, intron/exon length distributions) differ significantly between organisms. Using human parameters to predict fly genes, for example, leads to systematic mispredictions.

**Q**: What is a combiner program and why does it often outperform individual predictors?
**A**: A combiner integrates predictions from multiple gene finders. Because different predictors make partially uncorrelated errors, combining them increases signal-to-noise ratio and typically improves specificity substantially.
