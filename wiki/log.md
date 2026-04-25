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
