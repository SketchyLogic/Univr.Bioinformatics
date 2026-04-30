---
CreatedAt: 2026-04-24
LastUpdateAt: 2026-04-28
LastReviewAt: null
ReviewerIds:
  - admin
OwnerIds:
  - admin
IssueNotes: null
GeneratedById: claude-sonnet-4-6
---
# Extrinsic vs. Intrinsic Information in Gene Prediction

**Summary**: Gene prediction methods use two fundamentally different classes of evidence — extrinsic information derived from outside the target sequence, and intrinsic (ab initio) information derived from the sequence itself.

**Sources**: [[2.1.gene_prediction_v15.pdf]]

---
## The division

| <br>Class             | Definition                                     | Examples                                      |
| --------------------- | ---------------------------------------------- | --------------------------------------------- |
| Extrinsic             | Evidence not from the target genome sequence   | cDNA, ESTs, protein homology, RNA-seq         |
| Intrinsic / ab initio | Derived solely from the target genome sequence | Signal sensors, content sensors, conservation |

Methods using no extrinsic information are called **de novo** methods. 
The term **ab initio** is used strictly for de novo methods that also do not use [[informant genome]].

## Extrinsic information

### Full-length cDNA (gold standard)

A full-length cDNA aligned to the genome with canonical splice sites defines the [[gold standard for gene annotation]]. It directly gives transcript boundaries and exon coordinates.

> [!How is cDNA obtained?]-
> **How it is obtained**: total RNA is extracted from a tissue or cell line, and poly-A-tailed mRNAs are isolated. Reverse transcriptase converts each mRNA into a single-stranded cDNA using the poly-A tail as a priming site; a second strand is then synthesised to produce double-stranded cDNA. The result is then sequenced and matched against a database (e.g. NCBI RefSeq, EMBL) to align it with a genome.

Tools for spliced alignment: **BLAST** (rough), then dedicated spliced aligners:
- Procrustes, EST_GENOME, sim4, BLAT, GMAP, Exonerate, Genewise

These use either simple terminal dinucleotide models or position weight matrices for splice junction scoring.

### ESTs and short reads

[[Expressed Sequence Tag (EST) |EST 101]]
Expressed Sequence Tags (ESTs) are partial cDNA sequences. Their alignments are useful but incomplete. RNA-seq reads provide similar evidence at scale.

Extrinsic evidence is rarely complete: an EST may cover only two of five exons, or a cDNA may be missing the 5′ end. When the available alignments leave parts of a gene model unsupported, pipelines such as ENSEMBL and UCSC fill the gaps with ab initio prediction — running a gene finder over the uncovered region and grafting its output onto the exons already anchored by extrinsic evidence. The final gene model is a hybrid: experimentally grounded where evidence exists, computationally inferred where it does not.

### Protein homology

Protein sequences from related organisms can be aligned to the genome with tools like Genewise (aligns proteins accounting for introns). Useful when:
- Full cDNA is unavailable
- A well-characterized protein family exists in another species

## Intrinsic information

Intrinsic approaches use three types of signals in the sequence:

### 1. Signal sensors
Short, recognizable sequence motifs at functional boundaries:

**Splicing signals** (mark intron boundaries):
- Donor splice sites ([[GT-AG rule|GT]]) — 5′ end of intron
- Acceptor splice sites ([[GT-AG rule|AG]]), [[Branch point (splicing)|Branch point]], [[Polypyrimidine tract]] — 3′ end of intron

**Translation signals** (mark coding sequence boundaries):
- Start codon (ATG), [[Kozak consensus sequence|Kozak context]]
- Stop codon (TAA, TAG, TGA)

**Transcription signals** (mark gene boundaries):
- Promoter elements ([[TATA box]]), poly-A signal (AATAAA)

Modelled by [[signal-sensors]] (PWMs, WAMs, Markov chains, SVMs).

### 2. Content sensors
Statistical properties of coding vs. non-coding sequence:
- Codon usage bias
- Hexamer (6-mer) frequencies with codon position dependency
- 5th-order inhomogeneous Markov model (3-periodic)
- Di-codon usage

See [[content-sensors]].

### 3. Evolutionary conservation
Coding sequences evolve more slowly than non-coding. When an informant genome is available:
- Conservation pattern is an orthogonal measure of coding potential
- Methods: SGP2, TWINSCAN (1 informant), CONTRAST (27 informants)
- Phylo-HMMs model evolutionary history explicitly

See [[evolutionary-conservation]].

## Combining extrinsic and intrinsic

Modern gene prediction pipelines integrate both:
- **Stepwise pipelines** (ENSEMBL, UCSC): spliced alignment → ab initio extension
- **Direct incorporation**: Twinscan, Augustus (hints framework)
- **Combiners**: GLEAN, EuGène — take predictions from multiple tools and merge

The integration matters: extrinsic evidence is more reliable when available but sparse; intrinsic methods scale to the entire genome.

## Related pages

- [[gene-prediction]]
- [[signal-sensors]]
- [[content-sensors]]
- [[evolutionary-conservation]]
- [[sequence-alignment]]
- [[gene-prediction-tools]]

## Other sources

## Test yourself

**Q**: What is the difference between "de novo" and "ab initio" gene prediction?
**A**: De novo methods use only the target genome sequence (no external evidence). Ab initio is a stricter subset that also excludes informant genome alignments. Not all sources use these terms consistently.

**Q**: Why is a full-length cDNA alignment considered the gold standard for gene annotation?
**A**: Because it provides direct experimental evidence of the transcript. If the cDNA is full-length and aligns to the genome at canonical splice sites, the exon coordinates are essentially ground truth — no inference required.

**Q**: What are ESTs and how are they used in gene prediction?
**A**: Expressed Sequence Tags are short, single-pass cDNA sequences. They are aligned to the genome as partial evidence of transcription. Because they are partial, they must be combined with other evidence (ab initio or other ESTs) to define full gene models.

