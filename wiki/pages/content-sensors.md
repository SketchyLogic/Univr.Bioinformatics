---
CreatedAt: 2026-04-24
LastUpdateAt: 2026-04-30
LastReviewAt: null
ReviewerIds:
  - admin
OwnerIds:
  - admin
IssueNotes: null
GeneratedById: claude-sonnet-4-6
---
# Content Sensors

**Summary**: Content sensors measure the statistical properties of DNA sequence composition to discriminate coding from non-coding regions; the most powerful rely on codon position-dependent hexamer frequencies modelled as a 5th-order inhomogeneous Markov chain.

**Sources**: [[2.1.gene_prediction_v15.pdf]]

**Last updated**: 2026-04-24

---

## What is coding content?

Protein-coding regions have characteristic biases in DNA sequence composition absent from introns and intergenic sequence. Two main sources of bias:

1. **Amino acid usage bias** — not all amino acids are equally common in real proteins.
2. **Synonymous codon usage bias** — among synonymous codons (those encoding the same amino acid), organisms preferentially use a subset.

## Coding statistics

A **coding statistic** is a function that computes a real number related to the likelihood that a DNA sequence codes for a protein. Most coding statistics measure directly or indirectly:

- **Codon or di-codon usage bias** — which of the 64 codons (or adjacent codon pairs) are over- or under-represented relative to a null model.
- **Base compositional bias between the three codon positions** — the three positions inside a codon are not equivalent. Positions 1 and 2 are under strong selective pressure (changing them usually changes the amino acid). Position 3 is the "wobble" position: many amino acids tolerate any nucleotide there, so it accumulates very different nucleotide frequencies. As a result, the A/T/G/C proportions at codon position 1, 2, and 3 are measurably distinct from each other — and from non-coding sequence.

## 5th-order codon position-dependent Markov model

The most powerful coding statistic in practice. Implemented in GENSCAN, AUGUSTUS, and most modern gene finders.

- **5th-order**: the probability of a nucleotide depends on the 5 preceding nucleotides → hexamer (6-mer) frequencies.
- **Codon position-dependent (3-periodic / inhomogeneous)**: a separate Markov chain for each of the 3 codon positions.

This gives 3 separate hexamer tables — one per reading-frame position — capturing that the 3rd codon position has very different composition to the 1st.

In practice, implemented as a **three-periodic inhomogeneous Markov model**: one Markov chain per codon position. The model scores a candidate exon sequence and returns a log-likelihood ratio (coding vs. non-coding).

## Visual intuition

Figure 3 from Alioto & Guigó shows coding potential calculated by a 5th-order Markov model over the human beta-globin locus: the score is high and positive over true exons (shown in blue), and negative/fluctuating over introns and intergenic sequence. The boundary is not perfect but strongly informative.

## Other coding statistics

| Statistic | Principle |
|-----------|-----------|
| Hexamer frequencies | 6-mer counts in annotated exons vs. introns |
| Codon usage table | Frequency of each of the 64 codons in coding sequence |
| Di-codon usage | Frequency of adjacent codon pairs |
| Base composition bias | GC content difference between codon positions |
| Fourier analysis (period 3) | Power at frequency 1/3 as signal of coding |

## Why 5th-order?

Lower-order models (e.g., 3rd-order = tetramers) lose discriminatory power because they do not capture the full context of codon usage. Higher-order models (e.g., 7th) require exponentially more training data. 5th order (hexamers) empirically provides maximum discrimination power for typical training set sizes.

## Content sensors and signal sensors are complementary

Signals define precise **boundaries** of exons. Content statistics provide evidence that the sequence *between* boundaries is actually coding. Neither alone is sufficient:
- Signals without content: too many false positive splice site combinations.
- Content without signals: no precise boundaries, only vague coding regions.

The integration of both is the purpose of [[hidden-markov-models]] for gene finding.

## Related pages

- [[signal-sensors]]
- [[gene-prediction]]
- [[hidden-markov-models]]
- [[eukaryotic-gene-structure]]

## Other sources

- Fickett & Tung (1992), Gelfand (1995), Guigó et al. (2000) — foundational coding statistics
- Borodovsky & McIninch (1993) — 3-periodic Markov model (GeneMark)

## Test yourself

**Q**: Why does the 5th-order Markov model for coding regions use three separate tables?
**A**: Because codon positions have very different nucleotide composition. Position 3 of a codon (the "wobble" position) is the most degenerate and has the most extreme composition bias. Using three position-specific tables captures the 3-periodic nature of the genetic code.

**Q**: What is codon usage bias and why does it help distinguish coding from non-coding DNA?
**A**: Organisms use synonymous codons (those encoding the same amino acid) non-uniformly. This creates consistent, species-specific patterns in coding sequence that are absent from non-coding sequence, making hexamer frequencies a reliable discriminative signal.

**Q**: Can you use content sensors alone to predict gene boundaries?
**A**: No. Content sensors estimate the *likelihood* that a stretch of sequence is coding but do not give precise boundaries. Splice site and start/stop codon signals (signal sensors) are required to define exact exon boundaries.
