# Signal Sensors

**Summary**: Signal sensors detect short, functionally important sequence motifs such as splice sites, start codons, and promoters; they are one of two core components of ab initio gene prediction alongside content sensors.

**Sources**: [[2.1.gene_prediction_v15.pdf]]

**Last updated**: 2026-04-24

---

## What are signals?

Signals are nucleic acid sequence motifs recognised by the cellular machinery responsible for transcribing, processing, and translating mRNA. The minimal set needed to describe a coding sequence (CDS) includes:

| Signal | Location | Canonical sequence |
|--------|----------|--------------------|
| Start codon | Beginning of CDS | ATG (+ Kozak context) |
| Stop codon | End of CDS | TAA, TAG, TGA |
| Donor splice site | Exon-intron 5' boundary | GT (GU in RNA) |
| Acceptor splice site | Intron-exon 3' boundary | AG |
| Branch point | ~20–50 nt upstream of acceptor | Intronic A |
| Polypyrimidine tract | Between branch point and acceptor | Py-rich |
| TSS / Promoter | Upstream of gene | TATA box, Inr, DPE |
| Poly-A signal | Downstream of stop | AATAAA |

## Position Weight Matrices (PWMs)

The simplest model for a signal of length *l*. Given *n* aligned sequences:

$$M_{ij} = \frac{1}{n} \sum_{k=1}^{n} I_i(S_{kj}), \quad i \in \{A,C,G,T\}, \quad j = 1 \ldots l$$

The matrix records the frequency of each nucleotide at each position. Scoring a new sequence: slide a window of size *l*, sum the log-likelihood ratios (signal vs. background). A score above zero means the window is more likely to be the signal than random sequence.

**Background model**: uniform (0.25 each) or true genomic frequencies or local context frequencies.

**Limitation**: assumes each position is independent.

## Weight Array Models (WAMs) — 1st-order Markov

Captures dependencies between *adjacent* positions. The probability of a sequence being a signal becomes:

$$P(S) = P(s_1) P(s_2|s_1) P(s_3|s_2) P(s_4|s_3) \cdots P(s_n|s_{n-1})$$

This is a **1st-order Markov chain** conditioned on the immediately preceding nucleotide. Donor and acceptor splice sites are commonly modelled this way, as are branch points.

Higher-order chains (2nd, 3rd) condition on more preceding positions at the cost of more parameters.

## Maximal Dependence Decomposition (MDD)

Used in GENSCAN for the donor site. Captures **non-adjacent** dependencies: a decision tree selects among several WAMs depending on observed nucleotides at the most informative positions. Outperforms PWMs and 1st-order WAMs for individual site detection.

## Support Vector Machines (SVMs)

SVMs trained on sequence features local to splice sites (SVM-splice, Rätsch et al.) substantially outperform PWMs when tested in isolation. However, gains often vanish when embedded in the full gene prediction framework — the additional complexity does not always translate to better complete gene structures.

## Sequence logos

A visual representation of a PWM. Column height = information content in bits; letter heights proportional to frequency. Useful for seeing the conserved positions of a signal (e.g., the GT at positions 1–2 of the donor site dominates with ~2 bits of information).

## From signals to gene structure

Signals alone cannot specify gene structure: potential start codons, splice sites, and stop codons occur throughout the genome by chance. The signals must be *combined* with [[content-sensors]] and assembled into consistent gene models by a [[hidden-markov-models]] or exon-chaining framework.

## Related pages

- [[gene-prediction]]
- [[eukaryotic-gene-structure]]
- [[content-sensors]]
- [[extrinsic-vs-intrinsic-information]]
- [[hidden-markov-models]]

## Other sources

- Burge & Karlin (1997) GENSCAN — canonical use of MDD for donor site
- Rätsch et al. (2006) — SVM splice site predictors

## Test yourself

**Q**: What is a PWM and what assumption does it make?
**A**: A Position Weight Matrix tabulates the frequency of each nucleotide at each position of an aligned set of functional sequences. It assumes positions are **independent** — the nucleotide at position *j* does not depend on position *j-1*. This is biologically false but often a useful approximation.

**Q**: How does a WAM improve on a PWM?
**A**: A WAM (Weight Array Model) uses conditional probabilities so that the probability of a nucleotide at position *j* depends on the nucleotide at *j-1*. This captures first-order dependencies between adjacent positions.

**Q**: Why is the GT-AG rule useful but insufficient for splice site prediction?
**A**: GT-AG is a necessary constraint (filters ~99% of spurious sites) but is not sufficient — GT and AG occur millions of times in a mammalian genome, but only thousands are true splice sites. The surrounding sequence context (PWM/WAM score) is needed to rank candidates.
