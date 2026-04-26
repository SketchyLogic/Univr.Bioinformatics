---
CreatedAt: 2026-04-24
LastUpdateAt: 2026-04-24
LastReviewAt: null
ReviewerIds:
  - admin
OwnerIds:
  - admin
IssueNotes: null
GeneratedById: claude-sonnet-4-6
---
# Hidden Markov Models

**Summary**: Hidden Markov Models (HMMs) are probabilistic state machines where observations (e.g., DNA nucleotides) are visible but the underlying states (e.g., exon/intron) are hidden; they are the dominant framework for ab initio gene prediction.

**Sources**: [[2.1.gene_prediction_v15.pdf]] · [[Modelli Nascosti di Markov-Gene pred.pdf]]

**Last updated**: 2026-04-24

---

## Biological motivation

Given a DNA sequence, we observe only nucleotides (A, C, G, T). We cannot directly observe the functional state of each position — whether it is an exon, intron, intergenic region, splice site, etc. The HMM provides a formal framework to **infer hidden functional states from observable sequence**.

### The dishonest casino analogy

An intuitive way to understand HMMs (from the Italian lecture slides):

| Casino | DNA / Gene finding |
|--------|--------------------|
| Fair die (O) | Intron (I) |
| Loaded die (T) | Exon (E) |
| Number rolled | Nucleotide (A, C, G, T) |
| Which die used | Hidden functional state |

The croupier secretly switches between dice; we only see the numbers. Can we infer which die was in use at each roll? Analogously: we see nucleotides; can we infer which genomic regions are exons?

## The 5 components of an HMM

1. **Hidden states** (Q): e.g., {Exon, Intron} or {start, donor, internal_exon, intron, acceptor, stop, intergenic}
2. **Observations** (Σ): the visible alphabet — {A, C, G, T}
3. **Transition probabilities** (A): P(q_j | q_i) — probability of moving from state i to state j
4. **Emission probabilities** (B): P(x | q) — probability of emitting symbol x from state q
5. **Initial distribution** (π): probability of starting in each state

## A simple 2-state example

States: E (Exon), I (Intron)

**Transition matrix** (from the lecture notes):
```
       → E    I
From E   0.8  0.2
From I   0.3  0.7
```
Interpretation: Exons tend to continue as exons (high self-transition); so do introns. This encodes the biological reality that exons and introns are contiguous regions, not alternating nucleotide by nucleotide.

**Emission probabilities** (from the lecture notes):
```
       A    C    G    T
Exon   0.2  0.3  0.3  0.2   (GC-rich)
Intron 0.4  0.1  0.1  0.4   (AT-rich)
```
Exons are GC-rich; introns are AT-rich. This matches the biological observation captured by [[content-sensors]].

## The three fundamental problems

| Problem | Question | Algorithm |
|---------|----------|-----------|
| **Evaluation** | P(sequence \| model) — how likely is this sequence given the model? | Forward algorithm |
| **Decoding** | What is the most likely state sequence given the observed sequence? | **Viterbi algorithm** |
| **Learning** | Given sequences, estimate the model parameters (A, B, π) | Baum-Welch (EM) |

For gene prediction, **decoding** (finding the most likely exon/intron assignment) is the primary task. See [[viterbi-algorithm]].

## From simple to realistic HMMs

The 2-state exon/intron model is a pedagogical abstraction. Real gene-finding HMMs are much more complex:

- Separate states for: start codon, first exon, internal exon, terminal exon, single-exon gene, donor site, intron (phase 0/1/2), acceptor site, stop codon, 5' UTR, 3' UTR, intergenic
- Three separate intron/exon states per reading frame to enforce phase compatibility
- Signal states modelled by their own sub-HMMs (PWMs, WAMs, MDD)
- Content states modelled by higher-order Markov chains (5th-order hexamer model)

The first HMM gene finders: Genie (Kulp et al. 1996), [[genscan|GENSCAN]] (Burge & Karlin 1997).

## Generalized HMMs (GHMMs)

Basic HMMs limit state duration to a geometric distribution (controlled by the self-transition probability). Real exons and introns have length distributions that deviate from geometric.

A **Generalized HMM** (GHMM) explicitly models length distributions:
- On entering state q, draw a duration d from a distribution specific to that state
- Emit d symbols according to the emission model
- Transition to the next state

This allows Poisson or empirical length distributions for exons and introns. AUGUSTUS uses GHMMs, explicitly modelling short introns while using a geometric approximation for long introns.

GHMMs are **modular**: sub-models (e.g., donor site, acceptor site) can be trained independently and plugged into the main model.

## Generalized Pair HMMs (GPHMMs)

An extension that simultaneously produces an **alignment and annotation** of two syntenic genomic sequences. The model emits gene features (e.g., exon pairs, intron pairs) one in each species. Programs: SLAM, TWAIN.

Advantage: predictions in both species simultaneously; higher accuracy.
Limitation: requires syntenic sequence; variability in exon number not tolerated.

## Phylo-HMMs

Models a combination of two Markov processes:
- Along the genome (like GHMM gene finding)
- Along the branches of a phylogenetic tree (evolutionary time)

Columns of a multiple alignment are emitted according to a phylogenetic model (e.g., HKY substitution model). Coding and non-coding regions have different evolutionary rates.

Examples: UCSC conservation track, N-SCAN (Gross & Brent 2006), SHADOWER (McAuliffe et al. 2004).

## Discriminative alternatives

HMMs are **generative**: they model the joint probability P(sequence, states). An alternative is **discriminative learning** which directly models P(states | sequence):

- **SVMs**: trained on sequence features to classify exon/intron; used in mSplicer, mGene
- **Semi-Markov CRFs (SM-CRFs)**: analogous to GHMMs but discriminatively trained; CRAIG, CONRAD, CONTRAST

SM-CRFs are promising because: (1) any feature of a segment can be used; (2) features can overlap; (3) discriminative training directly maximises annotation accuracy.

## Connection to modern deep learning

Classical gene finders (GENSCAN, AUGUSTUS) are complex HMMs trained on annotated genomes. Today, deep learning architectures (convolutional and recurrent neural networks) are used for splice site prediction and coding region detection — but the underlying probabilistic structure (sequence of labelled segments) is identical to the HMM framework. The principle is the same; the parameterisation is learned by gradient descent rather than EM.

## Related pages

- [[viterbi-algorithm]]
- [[gene-prediction]]
- [[signal-sensors]]
- [[content-sensors]]
- [[eukaryotic-gene-structure]]
- [[gene-prediction-tools]]

## Other sources

- Rabiner (1989) — classic HMM tutorial
- Burge & Karlin (1997) — GENSCAN (canonical GHMM gene finder)
- Stanke et al. (2006) — AUGUSTUS
- Eddy (2004) — "What is a hidden Markov model?" *Nature Biotechnology*

## Test yourself

**Q**: What are the 5 components of an HMM?
**A**: (1) Hidden states, (2) Observable alphabet, (3) Transition probability matrix, (4) Emission probability matrix, (5) Initial state distribution.

**Q**: Why are the three HMM problems (Evaluation, Decoding, Learning) important for gene finding?
**A**: Evaluation (Forward algorithm) tells us how well the model fits a sequence. Decoding (Viterbi) gives us the actual gene structure prediction. Learning (Baum-Welch) lets us train the model from data. In practice, gene finding is primarily a decoding problem.

**Q**: What is the main limitation of a basic HMM that GHMMs solve?
**A**: Basic HMMs model state duration as a geometric distribution (memoryless). Real exons and introns have empirical length distributions that differ substantially from geometric. GHMMs explicitly model these distributions, improving prediction accuracy especially for very short or very long features.

**Q**: What is the dishonest casino analogy for gene finding?
**A**: A croupier secretly switches between a fair die (= intron, AT-rich emission) and a loaded die (= exon, GC-rich emission). We observe the numbers (= nucleotides) but not which die (= functional state) was used. The Viterbi algorithm finds the most likely sequence of dice = most likely sequence of exonic/intronic states.
