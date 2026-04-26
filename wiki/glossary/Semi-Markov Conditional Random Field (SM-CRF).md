---
tags:
  - __DEFINITION
  - Module1
---
# Semi-Markov Conditional Random Field (SM-CRF)

A **discriminative**[^1] sequence labeling model for gene prediction that directly models P(annotation | sequence), in contrast to generative models like [[Generalized Hidden Markov Model (GHMM)|GHMMs]] which model the joint P(sequence, annotation).

**Key advantages over GHMMs**:
1. **Arbitrary overlapping features**: can use any function of the input sequence (e.g., total CpG count over an exon, SVM score at a splice site) — not just local emission probabilities.
2. **No input model required**: does not need a probabilistic model of the DNA sequence itself.
3. **Discriminative training**: parameters are optimised directly to maximise annotation accuracy (not sequence likelihood).

**Trade-off**: requires labelled training data; harder to train than generative models; less interpretable.

**Implementations**: CRAIG, CONRAD.

See [[hidden-markov-models]], [[gene-prediction-tools]], [[gene-prediction]].

# TLDR
Instead of modelling how sequences are generated (like a GHMM), it models which annotation is most accurate given the sequence — allowing arbitrary features and direct accuracy optimisation.

---

[^1]: **Discriminative vs. generative**: a generative model learns P(sequence, annotation) — how data is produced. A discriminative model learns P(annotation | sequence) — given the data, what is the correct label. Discriminative models often achieve higher accuracy because they optimise the classification boundary directly, without wasting capacity on modelling the input distribution.
