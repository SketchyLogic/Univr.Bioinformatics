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
