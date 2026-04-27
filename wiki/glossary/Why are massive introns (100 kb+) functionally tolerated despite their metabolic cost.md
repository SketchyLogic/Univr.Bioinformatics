---
tags:
  - __QUESTION
CreatedAt: 2026-04-26
LastUpdateAt: 2026-04-26
LastReviewAt:
ReviewerIds:
  - admin
OwnerIds:
  - admin
IssueNotes:
GeneratedById:
---
# Why are massive introns (100 kb+) functionally tolerated despite their metabolic cost?

**Strategy**: address three layers — what the cost actually is, what compensatory or regulatory benefits exist, and why selection pressure is insufficient to purge them.

1. **The cost is real but limited**: transcription of a 100 kb intron costs ATP and time. However, in multicellular eukaryotes the relevant unit of fitness is the whole organism's reproductive success, not the speed of a single transcription event. Slow transcription of one gene in one tissue does not necessarily impair fitness enough to be selected against.

2. **Intron size is itself functional**:
   - **Cotranscriptional splicing timing**: large introns slow RNA Pol II, giving upstream exons time to be spliced before downstream exons are synthesised — a form of kinetic proofreading that improves splicing fidelity.
   - **Regulatory elements embedded in the intron**: enhancers, silencers, lncRNA genes, miRNA precursors, and insulators are often located deep inside large introns. Deleting the intron would remove these cis-regulatory sequences.

3. **Tissue-specific expression dampens the cost**: genes with very large introns (e.g. *DSCAM* ~840 kb, *CNTNAP2* ~2.3 Mb) are often expressed in post-mitotic neurons where rapid cell division is not required. The metabolic cost of slow transcription is tolerable in long-lived, non-dividing cells.

4. **Population genetics perspective**: in organisms with small effective population sizes ($N_e$) — such as large multicellular animals — genetic drift dominates selection. A slightly deleterious intron cannot be efficiently purged because $|s| < 1/N_e$. This is the **mutational hazard hypothesis**: eukaryotes with small $N_e$ accumulate non-essential DNA (introns, repeats) because selection is too weak to remove it.

**Key contrast**: bacteria, with enormous $N_e$ and strong selection for replication speed, have virtually no introns — consistent with the drift argument.

**Related**: [[eukaryotic-gene-structure]] · [[Alternative splicing]] · [[hidden-markov-models]]
