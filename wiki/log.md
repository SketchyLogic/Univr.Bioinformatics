# Wiki Log

Append-only record of all operations performed on this wiki.

---

## 2026-04-24 — Initial ingest of all raw sources

**Sources ingested**:
1. `raw/2.1.gene_prediction_v15.pdf` — "State of the art in eukaryotic gene prediction" (Alioto & Guigó)
2. `raw/Notes_Comp_Biology.pdf` — Computational Molecular Biology Methods (course notes; chapters: Homology Modeling, Molecular Docking, Molecular Dynamics)
3. `raw/Modelli Nascosti di Markov-Gene pred.pdf` — Italian lecture slides on HMMs for gene prediction (dishonest casino analogy, Viterbi)
4. `raw/annurev.genom.7.Ng_Henikoff.pdf` — "Predicting the Effects of Amino Acid Substitutions on Protein Function" (Ng & Henikoff, Annual Review of Genomics & Human Genetics 2006)

**Pages created**:
- `wiki/pages/gene-prediction.md`
- `wiki/pages/eukaryotic-gene-structure.md`
- `wiki/pages/extrinsic-vs-intrinsic-information.md`
- `wiki/pages/signal-sensors.md`
- `wiki/pages/content-sensors.md`
- `wiki/pages/hidden-markov-models.md`
- `wiki/pages/viterbi-algorithm.md`
- `wiki/pages/gene-prediction-tools.md`
- `wiki/pages/evolutionary-conservation.md`
- `wiki/pages/sequence-alignment.md`
- `wiki/pages/homology-modeling.md`
- `wiki/pages/molecular-docking.md`
- `wiki/pages/molecular-dynamics.md`
- `wiki/pages/amino-acid-substitutions.md`

**Infrastructure created**:
- `wiki/index.md`
- `wiki/glossary.md`
- `wiki/exam_prep.md`
- `wiki/study_path.md`
- `wiki/log.md`

**Notes**: First ingest from empty wiki. All 4 sources fully processed. Pages cover gene prediction (sources 1 and 3), computational structural biology (source 2), and nsSNP/protein function prediction (source 4). The `hidden-markov-models.md` page synthesises both the Alioto & Guigó review and the Italian HMM lecture slides.

---

## 2026-04-25 — Lint pass + graphic integration + new tool-reference pages

**Changes**:

- `wiki/pages/eukaryotic-gene-structure.md` — embedded `raw/graphics/eukaryotic-gene-structure.png` with explanatory caption (F1 lint fix)
- `wiki/pages/genscan.md` — new page: GENSCAN GHMM architecture, MDD donor model, inhomogeneous Markov content model, state graph, training, limitations, extensions (E1)
- `wiki/pages/sequence-search-tools.md` — new page: BLAST, PSI-BLAST, HMMER, HHpred, BLAT, GMAP — strategy, sensitivity comparison, use-case guide (E2)
- `wiki/pages/modeller.md` — new page: spatial restraints, objective function, VTF + MD/SA optimisation, multi-template modeling, quality assessment tools (E4)
- `wiki/pages/sequence-alignment.md` — added [[amino-acid-substitutions]] inline links on SIFT/PolyPhen mentions; added [[sequence-search-tools]] to Related pages (E3)
- `wiki/pages/gene-prediction-tools.md` — GENSCAN heading linked to [[genscan]]; [[genscan]] and [[sequence-search-tools]] added to Related pages
- `wiki/pages/homology-modeling.md` — MODELLER heading linked to [[modeller]]; [[modeller]] and [[sequence-search-tools]] added to Related pages
- `wiki/pages/hidden-markov-models.md` — GENSCAN mention linked to [[genscan]]
- `wiki/index.md` — added entries for genscan, sequence-search-tools, modeller

**Notes**: Lint identified 1 unreferenced graphic (now embedded) and 4 heavily-cited tools lacking dedicated pages (now created). No orphan pages, no broken links, no format violations found.

---

## 2026-04-25 — Glossary fill-in pass

**Entries created** (36 new files in `wiki/glossary/`):

**Module1 — Gene Prediction (signal sensors, content, HMM framework)**:
- `Position Weight Matrix (PWM).md` — __DEFINITION
- `Weight Array Model (WAM).md` — __DEFINITION
- `Maximal Dependence Decomposition (MDD).md` — __DEFINITION
- `GT-AG rule.md` — __DEFINITION
- `Kozak consensus sequence.md` — __DEFINITION
- `Poly-A signal.md` — __DEFINITION
- `Codon usage bias.md` — __CONCEPT
- `Open Reading Frame (ORF).md` — __DEFINITION
- `Intron phase.md` — __DEFINITION
- `Alternative splicing.md` — __CONCEPT
- `Hidden Markov Model (HMM).md` — __DEFINITION
- `Generalized Hidden Markov Model (GHMM).md` — __DEFINITION
- `Phylo-HMM.md` — __DEFINITION
- `Viterbi algorithm.md` — __DEFINITION
- `Baum-Welch algorithm.md` — __DEFINITION
- `Forward algorithm.md` — __DEFINITION
- `Semi-Markov Conditional Random Field (SM-CRF).md` — __DEFINITION
- `Combiner program.md` — __CONCEPT

**Module2 — Protein Structure, Docking, MD**:
- `Sequence identity zones.md` — __CONCEPT
- `Position-Specific Scoring Matrix (PSSM).md` — __DEFINITION
- `E-value.md` — __DEFINITION
- `Homology modeling.md` — __CONCEPT
- `DOPE score.md` — __DEFINITION
- `Cα RMSD.md` — __DEFINITION
- `Spatial restraints.md` — __CONCEPT
- `Ambiguous Interaction Restraint (AIR).md` — __DEFINITION
- `HADDOCK scoring function.md` — __DEFINITION
- `Force field.md` — __DEFINITION
- `Ergodic hypothesis.md` — __DEFINITION
- `Periodic boundary conditions (PBC).md` — __DEFINITION
- `Explicit vs. implicit solvent.md` — __CONCEPT
- `MARTINI coarse-grained force field.md` — __DEFINITION

**Module3 — Amino Acid Substitutions**:
- `Nonsynonymous SNP (nsSNP).md` — __DEFINITION
- `SIFT algorithm.md` — __CONCEPT
- `Ortholog.md` — __DEFINITION
- `Paralog.md` — __DEFINITION

**Executables (cross-module)**:
- `Distinguish de novo from ab initio gene prediction.md` — __EXECUTABLE (Module1)
- `Compare PWM WAM and MDD for splice site modeling.md` — __EXECUTABLE (Module1)
- `Explain why GHMM improves on standard HMM for gene finding.md` — __EXECUTABLE (Module1)
- `Predict whether an nsSNP is damaging using SIFT.md` — __EXECUTABLE (Module3)
- `Describe the HADDOCK docking protocol.md` — __EXECUTABLE (Module2)
- `Assess homology model quality from sequence identity.md` — __EXECUTABLE (Module2)

**Notes**: All entries cover the concepts directly tested in exam flashcards. Entries use wiki-links ([[page-name]]) to connect to related pages and to each other. Total glossary count: 39 files (3 pre-existing + 36 new).

---

## 2026-04-26 — New glossary entries

**Entry created**:
- `Why are massive introns (100 kb+) functionally tolerated despite their metabolic cost.md` — __QUESTION (Module1): covers metabolic cost vs. benefit, cotranscriptional splicing timing, embedded regulatory elements, tissue-specific expression, and the mutational hazard / drift argument.
- `Spliceosome.md` — __DEFINITION (Module1): composition (U1/U2/U4/U5/U6 snRNPs, ~150 proteins), two-step transesterification mechanism, assembly order, minor spliceosome, link to GT-AG rule and signal sensors.
- `Contrast the challenges of gene prediction in prokaryotes and eukaryotes.md` — __CONCEPT (Module1): comparative table (gene density, introns, start-site signals, repeats, operons, tools).
- `Relevance of matching intron phases.md` — __CONCEPT (Module1): what phase matching is, biological consequences of mismatch, why it constrains gene prediction search space, and four scenarios where mismatched phases can still yield a gene prediction.
- `Spurious ATG.md` — __DEFINITION (Module1): in-frame ATG that is not a genuine start site; how Shine-Dalgarno and Kozak signals distinguish real from spurious starts.

---

## 2026-04-26 — Lint-fix pass: YAML frontmatter metadata added to all files

**Changes**:

- All 17 `wiki/pages/` files — prepended full YAML frontmatter block (`CreatedAt`, `LastUpdateAt`, `LastReviewAt`, `ReviewerIds`, `OwnerIds`, `IssueNotes`, `GeneratedById`) before the `# Title` line. Dates assigned from log: 2026-04-24 for original 14 pages, 2026-04-25 for genscan, sequence-search-tools, modeller.
- All 51 `wiki/glossary/` files — inserted the same metadata fields inside the existing frontmatter block (after `tags:` lines, before closing `---`). Dates assigned from log: 2026-04-24 for 3 pre-existing entries, 2026-04-25 for 36 entries from the Glossary fill-in pass, 2026-04-26 for 6 entries from the New glossary entries pass. Extra pre-existing fields (`depth`, `prerequisites`) preserved in place.
- `wiki/pages/extrinsic-vs-intrinsic-information.md` — added empty `## Other sources` section between `## Related pages` and `## Test yourself`.
- `wiki/pages/gene-prediction-tools.md` — added empty `## Other sources` section between `## Related pages` and `## Test yourself`.
- `wiki/glossary/Why are massive introns (100 kb+) functionally tolerated despite their metabolic cost.md` — fixed broken link `[[alternative-splicing]]` → `[[Alternative splicing]]`.

---

## 2026-04-29 — New glossary entry (log2 in PWM)

**Entry created**:
- `Why log2 in PWM scoring.md` — __CONCEPT (Module1): why the likelihood ratio is logged — numerical stability, neutral point, worked 4-position example, and why base 2 gives bits.

---

## 2026-04-29 — Glossary updates

**Created**:
- `Branch point (splicing).md` — __DEFINITION (Module1): reactive adenosine forming the lariat, YNYURAY consensus, position diagram.
- `Polypyrimidine tract.md` — __DEFINITION (Module1): C/T-rich stretch recruiting U2AF65, relevance to acceptor PWMs.

**Updated**:
- `Position Weight Matrix (PWM).md` — upgraded from __DEFINITION to __CONCEPT; added worked example (frequency matrix, scoring formula), weighted-checklist intuition, and motivation for WAM/MDD.
- `extrinsic-vs-intrinsic-information.md` — signal sensors list reorganised into splicing / translation / transcription groups with wiki-links.

---

## 2026-04-29 — New glossary entries (splicing signals)

**Entries created**:
- `Branch point.md` — __DEFINITION (Module1): the reactive adenosine that forms the lariat, mechanism, consensus YNYURAY, position relative to acceptor.
- `Polypyrimidine tract.md` — __DEFINITION (Module1): C/T-rich stretch between branch point and AG, U2AF65 binding, relevance to acceptor PWMs.

**Page updated**:
- `extrinsic-vs-intrinsic-information.md` — signal sensors list reorganised into three labelled groups (splicing, translation, transcription) with wiki-links.

---

## 2026-04-29 — New glossary entry (TATA box)

**Entry created**:
- `TATA box.md` — __DEFINITION (Module1): consensus sequence, position relative to TSS, TBP binding and PIC assembly, role as a signal sensor in gene prediction, and why it is unreliable alone (~24 % of human promoters).

---

## 2026-04-30 — New glossary entry + update (conditional probability / PWM)

**Entry created**:
- `Refresher on conditional probabilities.md` — __CONCEPT (Module1): definition of conditional probability, the chain rule applied to P(window|signal), the positional independence assumption, how it collapses the chain rule to a product, and the connection to the PWM scoring formula.

**Entry updated**:
- `Why log2 in PWM scoring.md` — added "Conditional probability connection" section tracing the product formula back to the chain rule and the independence assumption; updated wiki-link in the starting-point section.

---

## 2026-04-29 — New glossary entries

**Entries created**:
- `Expressed Sequence Tag (EST).md` — __CONCEPT (Module1): definition, why ESTs were relevant, what is replacing them (RNA-seq, long-read RNA-seq).
- `Homology.md` — __CONCEPT (Module1): homology vs. similarity, ortholog/paralog/xenolog distinction, relevance to protein homology evidence and evolutionary conservation in gene prediction.

---

**Entry created**:
- `Expressed Sequence Tag (EST).md` — __CONCEPT (Module1): definition, why ESTs were relevant, what is replacing them (RNA-seq, long-read RNA-seq).

---

## 2026-04-27 — New glossary entry (types of introns)

**Entry created**:
- `Types of introns.md` — __CONCEPT (Module1): comparison table of all five intron classes (spliceosomal U2, U12, Group I, Group II, tRNA), removal mechanisms, boundary signals, and why gene prediction targets only spliceosomal U2-type introns.

---

## 2026-04-27 — New glossary entry (Structure of mRNA)

**Entry created**:
- `Structure of mRNA.md` — __CONCEPT (Module1): linear layout of mature eukaryotic mRNA (5′ cap, 5′ UTR, CDS, 3′ UTR, poly-A tail), relevance to full-length cDNA and gene annotation boundaries.

---

## 2026-04-27 — New glossary entry (gene annotation)

**Entry created**:
- `gene annotation.md` — __DEFINITION (Module1): what annotation produces, why it is needed, and how it is generated.

---

## 2026-04-27 — New glossary entry (gold standard)

**Entry created**:
- `gold standard for gene annotation.md` — __CONCEPT (GenePrediction): explains full-length cDNA, spliced alignment, canonical GT–AG splice sites, and why their combination makes the annotation ground truth.

---

## 2026-04-27 — New glossary entry

**Entry created**:
- `informant genome.md` — __DEFINITION (Module1): what an informant genome is, how taxonomic distance affects choice, usage comparison across SGP2 / TWINSCAN / N-SCAN, and the distinction from ab initio prediction.
- `integration framework.md` — __CONCEPT (Module1): why integration is needed (local sensor scores vs. global valid gene structure), comparison of all six framework types (exon chaining, GHMM, GPHM, Phylo-HMM, SM-CRF, combiners).
- `wiki/pages/gene-prediction.md` — fixed incorrect classification: conservation moved from ab initio to de novo in the "Two classes of information" section.

---

## 2026-05-02 — Ingest of lecture 1: Bioinformatics introduction and genome annotation pipeline

**Source ingested**: `raw/0_Introduzione.01_02_Bioinformatica_e_annotazione_genomi.pdf` — Giorgetti Alejandro, Università degli Studi di Verona. First lecture of the course (38 slides). Covers: (1) bioinformatics definition and omics landscape, (2) complete protein-coding gene annotation pipeline — experimental evidence alignment, ab initio, hybrid methods, EVM, automated pipelines (PASA, MAKER), accuracy metrics (Sn/Sp/AC at three levels), and a *Vitis vinifera* benchmark case study.

**Pages created**:
- `wiki/pages/introduction-to-bioinformatics.md` — bioinformatics definition, omics hierarchy, types of biological information, what genomics studies
- `wiki/pages/genome-annotation-pipeline.md` — full annotation workflow, all four method families, GFF3, experimental evidence types, hybrid methods, EVM, PASA/MAKER, accuracy metrics, *Vitis vinifera* case study with result tables

**Glossary entries created** (13 new files):
- `Bioinformatics.md` — __DEFINITION (Module0)
- `Genomics.md` — __DEFINITION (Module0)
- `Omics landscape.md` — __CONCEPT (Module0): four-layer hierarchy with table
- `NGS (Next Generation Sequencing).md` — __DEFINITION (Module0)
- `RNA-Seq.md` — __DEFINITION (Module0/1): shotgun transcriptome sequencing; why it excels at splice junction detection
- `cDNA full-length.md` — __DEFINITION (Module1): complete mRNA retrotranscript; why it is the gold standard
- `GFF3 format.md` — __DEFINITION (Module1): 9 columns, feature hierarchy, example
- `Functional annotation.md` — __DEFINITION (Module1): assigning biological function to gene products
- `Structural gene annotation.md` — __DEFINITION (Module1): localization + structure + alternative transcripts
- `Sensitivity and Specificity in gene prediction.md` — __CONCEPT (Module1): Sn/Sp/AC formulas, three evaluation levels
- `Annotation accuracy evaluation levels.md` — __CONCEPT (Module1): locus / exonic / junction levels with Vitis examples
- `Evidence Modeller (EVM).md` — __DEFINITION (Module1): weighted integration of predictions + evidence
- `MAKER annotation pipeline.md` — __DEFINITION (Module1)
- `PASA annotation pipeline.md` — __DEFINITION (Module1)
- `N50.md` — __DEFINITION (Module0): assembly/annotation summary statistic
- `Calculate sensitivity and specificity of a gene predictor.md` — __EXECUTABLE (Module1): worked example

**Infrastructure updated**:
- `wiki/index.md` — added Introduction section with `introduction-to-bioinformatics`; added `genome-annotation-pipeline` to Gene Prediction section
- `wiki/study_path.md` — inserted Module 0 with 2 new steps; renumbered all subsequent steps; updated dependency graph
- `wiki/exam_prep.md` — added Section 0 (Bioinformatics & Genome Annotation Overview) with 10 core concepts and 11 flashcards
