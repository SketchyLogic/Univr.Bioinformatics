# Study Path

**Summary**: The suggested order for working through this wiki. Designed to build concepts progressively — each page relies on understanding from the pages before it.

**Last updated**: 2026-04-24

---

## How to use this guide

Follow the paths below in order. Each step links to a wiki page. After reading each page, try the "Test yourself" questions before moving on. When you feel comfortable with a module, consolidate with [[exam_prep]].

---


## Module 1 — Foundations of Gene Structure (start here)

**Goal**: Understand what a eukaryotic gene looks like and why predicting them is hard.

1. [[eukaryotic-gene-structure]] — Learn the anatomy: exons, introns, splice sites, UTRs, the GT-AG rule, intron phases. This is the biological foundation for everything that follows.

2. [[gene-prediction]] — Understand the computational problem, the two classes of information, the evaluation metrics (sensitivity/specificity), and why training is species-specific.

---

## Module 2 — Information Sources for Gene Prediction

**Goal**: Understand what evidence is used and how it is modelled statistically.

3. [[extrinsic-vs-intrinsic-information]] — cDNA gold standard vs. ab initio methods; ESTs, protein homology, the stepwise vs. integrated pipeline.

4. [[signal-sensors]] — PWMs, WAMs, MDD; how splice sites and other signals are detected statistically. **Key concept**: log-likelihood ratio scoring.

5. [[content-sensors]] — Codon bias, hexamer frequencies, the 5th-order inhomogeneous Markov model. **Key concept**: why 3-periodic and why 5th-order.

6. [[evolutionary-conservation]] — Conservation as an orthogonal signal for both gene prediction and protein function.

---

## Module 3 — The HMM Framework

**Goal**: Understand how signal + content + structure are integrated into a gene prediction model.

7. [[hidden-markov-models]] — The dishonest casino analogy; 5 HMM components; 3 fundamental problems; from 2-state toy model to realistic GHMMs; Phylo-HMMs; SM-CRFs. **Central page of the course**.

8. [[viterbi-algorithm]] — The decoding algorithm in detail. Trace through the worked example. Understand the role of transition vs. emission probabilities.

9. [[gene-prediction-tools]] — Reference survey of tools (GENSCAN, AUGUSTUS, GeneID, combiners, spliced aligners). Know which method class each belongs to.

---

## Module 4 — Protein Structure Prediction

**Goal**: Understand how protein 3D structure is predicted computationally and its limitations.

10. [[sequence-alignment]] — Pairwise (BLAST), profile-sequence (PSI-BLAST), profile-profile (HHpred); the sequence identity zones (safe, twilight, midnight). **Prerequisite** for homology modeling.

11. [[homology-modeling]] — Template search, alignment, model construction (MODELLER), the 5 error categories, model quality assessment tools. **Key concept**: SI determines reliability.

---

## Module 5 — Protein-Protein and Protein-Ligand Interactions

**Goal**: Understand how binding poses and interaction energies are predicted.

12. [[molecular-docking]] — Scoring functions, search methods (systematic vs. stochastic), HADDOCK (AIRs, 3-step protocol, scoring), Autodock vs. Vina.

---

## Module 6 — Biomolecular Dynamics

**Goal**: Understand how molecular motion is simulated.

13. [[molecular-dynamics]] — Force fields (AMBER, GROMOS, CHARMM, OPLS), Newton's equations, timestep, integrators (Verlet, Velocity Verlet, Leapfrog), PBC, solvation, thermostats, coarse-grained methods (MARTINI).

---

## Module 7 — Genetic Variation and Protein Function

**Goal**: Understand how single nucleotide variants affect proteins and how to predict their functional impact.

14. [[amino-acid-substitutions]] — nsSNPs, SIFT, PolyPhen, SNPs3D; conservation vs. structure approaches; Mendelian and complex disease applications; the β-globin E6V case study.

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
eukaryotic-gene-structure
        ↓
  gene-prediction
        ↓
  extrinsic-vs-intrinsic-information
        ↓
  signal-sensors + content-sensors + evolutionary-conservation
        ↓
  hidden-markov-models
        ↓
  viterbi-algorithm
        ↓
  gene-prediction-tools

sequence-alignment
        ↓
  homology-modeling
        ↓
  molecular-docking
  molecular-dynamics

evolutionary-conservation ←→ amino-acid-substitutions
sequence-alignment ←→ amino-acid-substitutions
```
