---
CreatedAt: 2026-05-02
LastUpdateAt: 2026-05-02
LastReviewAt: null
ReviewerIds:
  - admin
OwnerIds:
  - admin
IssueNotes: null
GeneratedById: claude-sonnet-4-6
---

# Genome Annotation Pipeline

**Summary**: Protein-coding gene annotation combines four families of methods — experimental evidence alignment, *ab initio* prediction, hybrid approaches, and comparative genomics — then integrates all evidence into a final weighted consensus using a combiner such as EVM; accuracy is evaluated at three levels (gene locus, exonic regions, exon-intron junctions).

**Sources**: [[0_Introduzione.01_02_Bioinformatica_e_annotazione_genomi.pdf]]

---

## What genome annotation means

Annotating a genome means determining the **localization, structure, and function** of every element it contains. The focus of this course is on **protein-coding gene annotation**, which is itself divided into two sub-problems:

| Sub-problem | Goal |
|-------------|------|
| **[[Structural gene annotation]]** (gene annotation) | Define the localization, exon/intron structure (CDS, UTR), and alternative transcripts of each gene |
| **[[Functional annotation]]** | Assign a biological function to each protein encoded by the gene |

The [[eukaryotic-gene-structure]] page describes the gene model components (exon, intron, CDS, UTR) in detail.

## The GFF3 annotation format

Annotation results are stored in **[[GFF3 format]]** — a tab-separated file with one feature per line. Each line specifies: chromosome, source, feature type (`gene`, `transcript`, `exon`, `CDS`), start, end, score, strand, frame, and a free-text attributes field.

Features are hierarchical: a `gene` record is the parent of one or more `transcript` records, which are in turn parents of `exon` and `CDS` records.

[[0_Introduzione.01_02_Bioinformatica_e_annotazione_genomi.pdf#page=12|GFF3 format example with Vitis vinifera data — slide 12]]

## Four families of annotation methods

[[0_Introduzione.01_02_Bioinformatica_e_annotazione_genomi.pdf#page=13|Methods overview — slide 13]]

### 1. Experimental evidence alignment

Experimental sequences are aligned to the genome; regions with strong alignment coverage are candidate coding regions. The main evidence types are:

| Evidence | Description |
|----------|-------------|
| **[[cDNA full-length]]** | Full mature mRNA sequences reverse-transcribed to cDNA; includes complete 5′ UTR, CDS, and 3′ UTR |
| **[[Expressed Sequence Tag (EST)]]** | Short partial fragments (400–800 bp) of reverse-transcribed mRNA |
| **Homologous proteins** | Amino acid sequences from proteins in evolutionarily related organisms; back-translated to locate the CDS |
| **Tiling arrays** | Microarrays with evenly spaced probes across the genome; detect expressed regions via hybridisation |
| **MPSS** | Massively Parallel Signature Sequencing; identifies 17–20 bp signatures from mRNAs |
| **[[RNA-Seq]]** | Short reads (50–150 bp) from shotgun sequencing of the whole transcriptome |

RNA-Seq reads that span an exon-intron boundary split across the intron when aligned to genomic DNA, directly revealing splice junctions with high precision.

[[0_Introduzione.01_02_Bioinformatica_e_annotazione_genomi.pdf#page=14|Experimental evidence types — slide 14]]
[[0_Introduzione.01_02_Bioinformatica_e_annotazione_genomi.pdf#page=16|RNA-Seq workflow — slide 16]]

### 2. Ab initio gene prediction

*Ab initio* predictors use only **intrinsic sequence information** — statistical models trained on the organism being annotated — to identify coding regions without any external experimental data. They combine:

- **[[signal-sensors]]** — detect exon-intron junctions and gene boundaries (GT-AG splice sites, ATG start, stop codons)
- **[[content-sensors]]** — measure whether a region's sequence statistics are consistent with coding DNA (codon usage bias, hexamer frequencies)

Predictors require **training data** (to learn the organism's sequence statistics) and **test data** (to evaluate prediction accuracy). See [[gene-prediction]] and [[hidden-markov-models]] for the underlying models.

Key programs: AUGUSTUS, GeneID, SNAP, GeneMark-ES, GENSCAN, FGenesh.

[[0_Introduzione.01_02_Bioinformatica_e_annotazione_genomi.pdf#page=17|Ab initio method overview — slide 17]]

### 3. Hybrid: ab initio guided by experimental evidence

Neither approach alone is sufficient:
- *Ab initio* training data may not represent all gene classes in the genome.
- Experimental evidence never covers the entire genome, so it cannot produce a complete annotation.

The best gene finders therefore combine both: the *ab initio* statistical model defines the gene structure, while aligned experimental evidence (cDNA, EST, proteins, RNA-Seq) provides **hints** that bias the model toward experimentally supported boundaries.

AUGUSTUS and GeneID both support this hybrid mode.

### 4. Comparative genomics

Sequence conservation across related genomes is an independent signal for identifying functional elements. Phylo-HMMs and cross-species alignment tools (TwinScan/N-Scan) exploit this signal. See [[evolutionary-conservation]].

## Automated annotation pipelines

Full annotation pipelines automate the above steps:

| Pipeline | Notes |
|----------|-------|
| **[[PASA annotation pipeline]]** | Focuses on aligning transcript evidence; excels at building UTR models and detecting alternative splicing |
| **[[MAKER annotation pipeline]]** | Integrates ab initio predictors, EST/protein alignments, and repeat masking in a single configurable workflow |

Advantage: easy to run. Disadvantage: limited control over intermediate steps.

## Final annotation: evidence integration

The final step combines all evidence into a single annotation using a **weighted combiner**:

- Each evidence source receives a numerical weight; experimental evidence outweighs *ab initio* predictions.
- The combiner resolves conflicts by taking the highest-weighted consistent gene model.

Main integration programs: **[[Evidence Modeller (EVM)]]**, JIGSAW, GAZE.

[[0_Introduzione.01_02_Bioinformatica_e_annotazione_genomi.pdf#page=22|Final annotation / EVM — slide 22]]

## Accuracy evaluation

General statistics (number of predicted genes, average gene length) are insufficient to compare predictors. Rigorous evaluation requires measuring **sensitivity** and **specificity** against a reference annotation (gold standard).

$$Sn = \frac{TP}{TP + FN} = \frac{|i \cap j|}{|j|}$$

$$Sp = \frac{TP}{TP + FP} = \frac{|i \cap j|}{|i|}$$

$$AC = \frac{Sn + Sp}{2}$$

where $i$ = predicted set, $j$ = reference set, and $|i \cap j|$ = their intersection (overlap).

### Three evaluation levels

Accuracy is measured at three increasing levels of resolution:

[[0_Introduzione.01_02_Bioinformatica_e_annotazione_genomi.pdf#page=33|Accuracy levels diagram — slide 33]]

| Level | What it measures |
|-------|-----------------|
| **Gene locus** | Whether the predictor detects the correct genomic locus (coarse) |
| **Exonic regions** | Whether the exon/intron boundaries are correctly placed (nucleotide level) |
| **Exon-intron junctions** | Whether each individual splice junction is exactly correct (most stringent) |

A predictor may score well at one level but poorly at another; only junction-level accuracy confirms the correct gene structure.

## Case study: *Vitis vinifera*

The lecture presents a benchmark study optimising the annotation protocol for *Vitis vinifera* (grapevine), a complex eukaryote.

**Reference genome**: V1 PN40024 12X, 487 Mb (French-Italian Grapevine Consortium).

**Reference dataset**: 3,436 full-length cDNA sequences with complete ORFs (936 training / 2,500 test).

### Experimental evidence aligned

| Source | Non-redundant models | Mean nucleotide overlap with reference |
|--------|---------------------|---------------------------------------|
| EST | 56,630 | 88.11 % |
| Homologous proteins (SWISSPROT) | 5,808 | 62.60 % |
| RNA-Seq (114 M reads, 45 samples) | 17,444 | **94.35 %** |

### Ab initio predictions (after filtering single-exon and <200 bp exonic regions)

| Predictor | Genes predicted | Mean exons/gene |
|-----------|----------------|----------------|
| Augustus *ab initio* | 30,510 | 4.44 |
| GeneID *ab initio* | 48,751 | 4.34 |
| SNAP *ab initio* | 64,431 | 6.14 |

### Accuracy at gene locus level (key results)

| Evidence / Predictor | Sn | Sp | AC |
|---------------------|----|----|----|
| RNA-Seq alignment | 0.614 | **0.736** | **0.675** |
| EST alignment | 0.568 | 0.643 | 0.605 |
| Augustus *ab initio* | 0.461 | 0.564 | 0.513 |
| Augustus + RNA-Seq hints | 0.566 | 0.673 | 0.619 |

### Accuracy at exon-intron junction level (key results)

| Evidence / Predictor | Sn | Sp | AC |
|---------------------|----|----|----|
| **RNA-Seq alignment** | **0.872** | **0.951** | **0.912** |
| Augustus + RNA-Seq hints | 0.788 | 0.911 | 0.849 |
| Augustus *ab initio* | 0.626 | 0.835 | 0.730 |

RNA-Seq dramatically outperforms all other evidence at the junction level, because short reads that span splice sites directly reveal exact junction positions.

### Final annotation (EVM)

Three weight combinations were tested. Best result (Annotation 2: EST weight 3, proteins weight 5, Augustus+RNA-Seq weight 2, GeneID *ab initio* weight 1, SNAP *ab initio* weight 1):

- **~26,200 predicted genes** in *Vitis vinifera*
- Junction-level AC: **0.843**

### Conclusions from the case study

1. General statistics do not differentiate predictors — accuracy metrics are essential.
2. RNA-Seq (cheap, fast) as predictor hints substantially improves *ab initio* performance.
3. A final annotation using few accurate predictions saves significant compute time.
4. Evaluating every intermediate step of the pipeline enables an optimised final annotation.

## Related pages

- [[gene-prediction]]
- [[eukaryotic-gene-structure]]
- [[extrinsic-vs-intrinsic-information]]
- [[signal-sensors]]
- [[content-sensors]]
- [[hidden-markov-models]]
- [[gene-prediction-tools]]
- [[evolutionary-conservation]]
- [[introduction-to-bioinformatics]]

## Other sources

- Holt & Yandell (2011) — MAKER annotation pipeline paper
- Haas et al. (2003) — PASA pipeline paper
- Haas et al. (2008) — Evidence Modeller (EVM) paper
- Giorgetti A. — lecture slides, Università degli Studi di Verona

## Test yourself

**Q**: What is the difference between structural and functional gene annotation?
**A**: Structural annotation defines the physical location and structure of a gene (exons, introns, CDS, UTR, alternative transcripts). Functional annotation assigns a biological role to the protein product.

**Q**: Why is RNA-Seq the most accurate evidence for exon-intron junction prediction?
**A**: RNA-Seq reads that span a splice junction are split across the intron when aligned to genomic DNA, directly and precisely revealing the junction coordinates. In the *Vitis vinifera* study, RNA-Seq achieved AC = 0.91 at junction level vs. 0.52 for EST.

**Q**: Why is neither *ab initio* prediction nor experimental evidence alone sufficient for complete annotation?
**A**: Ab initio training data may not represent all gene classes; experimental evidence never covers the entire genome. Only their combination gives both coverage and structural precision.

**Q**: What are the three levels at which gene prediction accuracy is evaluated, and which is most stringent?
**A**: Gene locus (coarse: is the locus detected?), exonic regions (nucleotide-level exon/intron classification), and exon-intron junctions (exact splice site coordinates). Junction level is most stringent.

**Q**: Write the formulas for sensitivity, specificity, and accuracy in gene prediction.
**A**: $Sn = |i \cap j| / |j|$; $Sp = |i \cap j| / |i|$; $AC = (Sn + Sp) / 2$, where $i$ = predicted set and $j$ = reference set.
