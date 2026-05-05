# Study Path

**Summary**: The suggested order for working through this wiki. Designed to build concepts progressively — each page relies on understanding from the pages before it.

**Last updated**: 2026-04-24

---

## How to use this guide

Follow the paths below in order. Each step links to a wiki page. After reading each page, try the "Test yourself" questions before moving on. When you feel comfortable with a module, consolidate with [[exam_prep]].

---


## Module 0 — Course Introduction

**Goal**: Understand what bioinformatics and genomics are, and what genome annotation means in practice.

1. [[introduction-to-bioinformatics]] — What bioinformatics is, the omics landscape (Genomics → Transcriptomics → Proteomics → Metabolomics), and the tasks of genomics.

2. [[genome-annotation-pipeline]] — The complete annotation workflow: experimental evidence types (cDNA, EST, RNA-Seq, homologous proteins), *ab initio* prediction, hybrid approaches, EVM final annotation, accuracy metrics (Sn/Sp/AC at three levels), and the *Vitis vinifera* case study. **Read this early** to see the big picture before diving into individual components.

---

## Module 1 — Foundations of Gene Structure

**Goal**: Understand what a eukaryotic gene looks like and why predicting them is hard.

3. [[eukaryotic-gene-structure]] — Learn the anatomy: exons, introns, splice sites, UTRs, the GT-AG rule, intron phases. This is the biological foundation for everything that follows.

4. [[gene-prediction]] — Understand the computational problem, the two classes of information, the evaluation metrics (sensitivity/specificity), and why training is species-specific.

---

## Module 2 — Information Sources for Gene Prediction

**Goal**: Understand what evidence is used and how it is modelled statistically.

5. [[extrinsic-vs-intrinsic-information]] — cDNA gold standard vs. ab initio methods; ESTs, protein homology, the stepwise vs. integrated pipeline.

6. [[signal-sensors]] — PWMs, WAMs, MDD; how splice sites and other signals are detected statistically. **Key concept**: log-likelihood ratio scoring.

7. [[content-sensors]] — Codon bias, hexamer frequencies, the 5th-order inhomogeneous Markov model. **Key concept**: why 3-periodic and why 5th-order.

8. [[evolutionary-conservation]] — Conservation as an orthogonal signal for both gene prediction and protein function.

---

## Module 3 — The HMM Framework

**Goal**: Understand how signal + content + structure are integrated into a gene prediction model.

9. [[hidden-markov-models]] — The dishonest casino analogy; 5 HMM components; 3 fundamental problems; from 2-state toy model to realistic GHMMs; Phylo-HMMs; SM-CRFs. **Central page of the course**.

10. [[viterbi-algorithm]] — The decoding algorithm in detail. Trace through the worked example. Understand the role of transition vs. emission probabilities.

11. [[gene-prediction-tools]] — Reference survey of tools (GENSCAN, AUGUSTUS, GeneID, combiners, spliced aligners). Know which method class each belongs to.

---

## Module 4 — Protein Structure Prediction

**Goal**: Understand how protein 3D structure is predicted computationally and its limitations.

12. [[sequence-alignment]] — Pairwise (BLAST), profile-sequence (PSI-BLAST), profile-profile (HHpred); the sequence identity zones (safe, twilight, midnight). **Prerequisite** for homology modeling.

13. [[homology-modeling]] — Template search, alignment, model construction (MODELLER), the 5 error categories, model quality assessment tools. **Key concept**: SI determines reliability.

---

## Module 5 — Protein-Protein and Protein-Ligand Interactions

**Goal**: Understand how binding poses and interaction energies are predicted.

14. [[molecular-docking]] — Scoring functions, search methods (systematic vs. stochastic), HADDOCK (AIRs, 3-step protocol, scoring), Autodock vs. Vina.

---

## Module 6 — Biomolecular Dynamics

**Goal**: Understand how molecular motion is simulated.

15. [[molecular-dynamics]] — Force fields (AMBER, GROMOS, CHARMM, OPLS), Newton's equations, timestep, integrators (Verlet, Velocity Verlet, Leapfrog), PBC, solvation, thermostats, coarse-grained methods (MARTINI).

---

## Module 7 — Genetic Variation and Protein Function

**Goal**: Understand how single nucleotide variants affect proteins and how to predict their functional impact.

16. [[amino-acid-substitutions]] — nsSNPs, SIFT, PolyPhen, SNPs3D; conservation vs. structure approaches; Mendelian and complex disease applications; the β-globin E6V case study.

---

## Consolidation

After completing the modules:

1. Read [[exam_prep]] in full — work through all flashcards without looking at answers first.
2. Re-read pages where you got answers wrong.
3. Try to draw the complete gene prediction pipeline from memory (signals + content → HMM → Viterbi → gene models).
4. Try to explain the MODELLER workflow and HADDOCK protocol from memory.
5. Review the glossary for any terms that are still unclear.

---

## Quick reference — concept dependencies

```
introduction-to-bioinformatics
        ↓
eukaryotic-gene-structure
        ↓
  gene-prediction ←→ genome-annotation-pipeline
        ↓
  extrinsic-vs-intrinsic-information
        ↓
  signal-sensors + content-sensors + evolutionary-conservation
        ↓
  hidden-markov-models
        ↓
  viterbi-algorithm
        ↓
  gene-prediction-tools → genome-annotation-pipeline (EVM / MAKER / PASA)

sequence-alignment
        ↓
  homology-modeling
        ↓
  molecular-docking
  molecular-dynamics

evolutionary-conservation ←→ amino-acid-substitutions
sequence-alignment ←→ amino-acid-substitutions
```
