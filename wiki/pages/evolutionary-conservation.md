# Evolutionary Conservation

**Summary**: Coding sequences are more conserved than non-coding sequences across related species; conservation is an orthogonal and powerful signal for both gene prediction and the detection of functionally important positions in proteins.

**Sources**: [[2.1.gene_prediction_v15.pdf]] · [[annurev.genom.7.Ng_Henikoff.pdf]]

**Last updated**: 2026-04-24

---

## The principle

Functional sequences are subject to **purifying selection** — mutations that disrupt function are removed from the population over evolutionary time. As a result:
- Protein-coding exons are more conserved than introns and intergenic sequence across related species.
- Functionally important positions within proteins (active sites, binding sites, structural cores) are more conserved than positions where substitutions are tolerated.

This conservation is observable in sequence alignments and can be quantified and used for prediction.

## Conservation in gene prediction

### Informant genome approaches

When the genome of one or more related species is available, conservation of a candidate exon is an **orthogonal** measure of coding potential — it is largely independent of intrinsic signals and content statistics.

**Approaches**:

1. **Direct scoring** (SGP2): BLAST alignment scores between target and informant genomes directly modify the log-odds that a candidate exon is coding.

2. **Alignment-informed prediction** (TWINSCAN): BLAST alignments define an extended nucleotide alphabet (aligned vs. unaligned versions of A/C/G/T); the GENSCAN GHMM is retrained on this extended alphabet.

3. **Simultaneous alignment + annotation** (SLAM, TWAIN): Generalized Pair HMMs produce a joint annotation of two syntenic genomes.

4. **Multi-genome phylo-HMMs** (N-SCAN, CONTRAST): model the evolutionary history of the sequence across many genomes. CONTRAST uses 27 aligned vertebrate genomes.

### Visualising conservation

The UCSC Genome Browser's "PhyloP Conservation" track shows evolutionary conservation at nucleotide resolution. The UCSC conservation track itself is a phylo-HMM. Comparing gene predictions at the human beta-globin locus: programs using conservation (CONTRAST, SGP2) outperform those that do not (GeneID).

## Conservation in amino acid substitution prediction

For protein function, conservation has a different but related role (see [[amino-acid-substitutions]]):

- A position that is **conserved across many species** is likely to be functionally important. Mutations at such positions tend to be **damaging**.
- A position that varies across species can tolerate substitutions — mutations there are more likely to be **neutral**.

This forms the basis of sequence-based AAS prediction methods like **SIFT** (Sorting Intolerant From Tolerant):
1. Collect a multiple sequence alignment of orthologous and paralogous proteins.
2. For each position, compute a position-specific scoring matrix (PSSM) — effectively the conservation profile.
3. Score an amino acid substitution by the probability of seeing that amino acid at that position in the alignment. Low probability → likely damaging.

Key finding from Ng & Henikoff (2006): disease-causing mutations are overrepresented at conserved sites (high relative entropy in alignment column), while neutral nsSNPs are uniformly distributed across conservation levels.

## Quantifying conservation

### Relative entropy (information content)

For a multiple alignment column, relative entropy (Kullback-Leibler divergence) measures how much the observed amino acid distribution at that position deviates from the background (random) distribution. High relative entropy = highly conserved = likely important for function.

### Evolutionary rate

Phylogenetic models (e.g., HKY substitution model) estimate the **rate of evolution** at each position. Slowly evolving positions are under stronger purifying selection.

## Conserved vs. variable positions: practical implications

| Observation | Interpretation |
|-------------|---------------|
| Substitution at highly conserved position | Likely to disrupt function — damaging |
| Substitution at variable position | Likely tolerated — neutral |
| Disease mutation at surface-accessible position | May involve intermolecular interaction missed by structure alone |

The E6V substitution in β-globin (sickle cell) illustrates the nuance: E6V is at a surface position → predicted neutral by structure-based methods, but correctly predicted **damaging** by sequence-based SIFT because the position is conserved in β-globin orthologs.

## Key caveat: orthologs vs. paralogs

For AAS prediction, the alignment quality matters enormously. Using **orthologs** (same gene in different species) rather than paralogs (related but diverged genes with potentially different function) improves prediction accuracy by ~8%, even with few sequences. Paralogs may have diverged function, causing positions important in one copy to be irrelevant (and thus variable) in another.

## Related pages

- [[gene-prediction]]
- [[hidden-markov-models]]
- [[sequence-alignment]]
- [[amino-acid-substitutions]]
- [[gene-prediction-tools]]

## Other sources

- Miller et al. (2007) — 28-way vertebrate alignment (UCSC)
- Siepel & Haussler (2004) — Phylo-HMMs
- Ng & Henikoff (2003) — SIFT original paper

## Test yourself

**Q**: Why are coding sequences more conserved than introns across related species?
**A**: Because mutations in coding sequences that disrupt protein function are removed by purifying selection. Introns can accumulate mutations more freely (as long as splice sites and branch point are preserved).

**Q**: How does TWINSCAN use conservation for gene prediction?
**A**: It takes BLAST alignments between the target genome and an informant genome, uses these to define an extended nucleotide alphabet (8 symbols: aligned or unaligned versions of A/C/G/T), and retrains the GENSCAN GHMM on this extended alphabet.

**Q**: How does SIFT use evolutionary conservation to predict whether an amino acid substitution is damaging?
**A**: SIFT aligns the protein to homologs, builds a PSSM, and looks up the probability of observing the new amino acid at the substituted position. If the probability is below 0.05, the substitution is predicted damaging — the position is too conserved to tolerate the change.
