---
tags:
  - __CONCEPT
  - Module1
---
# Combiner program

A gene prediction strategy that integrates the outputs of **multiple independent gene finders** — rather than relying on a single tool — to produce a consensus annotation with higher accuracy.

**Why combiners outperform individual tools**:
- Different tools make partially uncorrelated errors (one tool may miss an exon boundary that another correctly predicts).
- Combining predictions increases the signal-to-noise ratio: correct predictions reinforce each other while errors cancel out.
- Combiners typically improve **specificity** substantially, with modest gains in sensitivity.

**Integration strategies**:
- Weighted voting (each tool vote weighted by its historical accuracy)
- Bayesian evidence combination
- Trained meta-classifier (uses tool outputs as features)

**Examples**: GLEAN, EuGène, JIGSAW, GAZE, Genomix. These reconcile ab initio predictions, EST alignments, and protein homology into a single annotation.

See [[gene-prediction-tools]], [[gene-prediction]].
